# CI/CD

## Recommended Reading

-   [Understanding GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)

## Overview

Continuous integration and deployment is the process of automatically running unit tests and building/deploying software. We only use GitHub Actions at the moment to automate deployment of the website as well as perform weekly backups.

## Website

We use this for our website, since it's hosted on GitHub Pages. Inside our `rucogs.github.io` repository, we have `.github/workflows/gh-pages-deployment.yml` workflow show below. This workflow automatically builds and deploys the website to GitHub Pages any time there is a commit made to the `main` branch.

```yaml
name: Deploy to GitHub Pages

on:
    push:
        branches:
            - main

jobs:
    build:
        runs-on: ubuntu-latest
        steps:
            - name: Checkout
              uses: actions/checkout@v2 # If you're using actions/checkout@v2 you must set persist-credentials to false in most cases for the deployment to work correctly.
              with:
                  persist-credentials: false
            - name: Use Node.js (Latest)
              uses: actions/setup-node@v2
              with:
                  node-version: "14"
                  check-latest: true
            - name: Build
              run: |
                  npm install -g @angular/cli
                  npm install
                  npm run build
                  cp dist/index.html dist/404.html
            - name: Deploy
              uses: JamesIves/github-pages-deploy-action@v4.2.5
              with:
                  branch: gh-pages # The branch the action should deploy to.
                  folder: dist # The folder the action should deploy.
```

## Backups

We also use GitHub Actions to automate backups of both the database and users' uploaded files. Inside our `rucogs-infrastructure-backup` repository, we have `.github/workflows/actions.yml` workflow shown below. This workflows requires the URI connection string to the MongoDB database, as well as the

```yaml
name: 📦 Make Backups
on:
    # Schedule updates (once every week)
    schedule:
        - cron: "0 0 * * 0"
    push:
        branches: ["main"]
    workflow_dispatch:

env:
    MONGODB_TOOLS_DOWNLOAD: https://fastdl.mongodb.org/tools/db/mongodb-database-tools-ubuntu2204-x86_64-100.6.1.tgz
    BACKEND_UPLOADS_DIR: /root/rucogs.github.io-backend/uploads/

jobs:
    mongodb-backup:
        name: MongoDB Backup
        runs-on: ubuntu-22.04
        steps:
            - name: Install MongoDB database tools
              run: |
                  curl -fLo mongodb-tools.tgz ${{ env.MONGODB_TOOLS_DOWNLOAD }}
                  mkdir mongodb-tools
                  tar -zxvf mongodb-tools.tgz --strip-components 1 -C mongodb-tools
                  cd mongodb-tools/bin
                  cp * /usr/local/bin/

            - name: Make dump
              run: mongodump --uri="${{ secrets.MONGO_URI }}"

            - name: Zip dump
              run: 7z a mongodump.zip dump

            - name: Upload artifact
              uses: actions/upload-artifact@v3
              with:
                  name: mongodump
                  path: mongodump.zip

    uploads-backup:
        name: Uploads Backup
        runs-on: ubuntu-latest
        steps:
            - name: Download uploads folder
              run: sshpass -p "${{ secrets.BACKEND_ROOT_PASS }}" scp -o StrictHostKeyChecking=no -r "${{ secrets.BACKEND_URI }}:${{ env.BACKEND_UPLOADS_DIR }}" ./uploads

            - name: Zip uploads
              run: 7z a uploads.zip uploads

            - name: Upload artifact
              uses: actions/upload-artifact@v3
              with:
                  name: uploads
                  path: uploads.zip
                  retention-days: 1

    create-release:
        needs: [mongodb-backup, uploads-backup]
        name: Create Release
        runs-on: ubuntu-latest
        outputs:
            tag: ${{ steps.create-tag.outputs.tag }}
        steps:
            - name: Create date
              id: create-date
              run: echo "date=$(date +'%Y-%m-%d(%H-%M-%S)')" >> $GITHUB_OUTPUT

            - name: Create tag
              id: create-tag
              run: echo "tag=backup-${{ steps.create-date.outputs.date }}')" >> $GITHUB_OUTPUT

            - name: Create Release
              uses: softprops/action-gh-release@v1
              with:
                  token: ${{ secrets.GITHUB_TOKEN }}
                  tag_name: ${{ steps.create-tag.outputs.tag }}
                  name: Backup ${{ steps.create-date.outputs.date }}
                  body: |
                      Backed up to ready to go! 🚀
                  draft: false
                  prerelease: false

    upload-release-artifacts:
        needs: create-release
        name: Upload Release Artifacts
        runs-on: ubuntu-latest
        strategy:
            matrix:
                artifact_name: [mongodump, uploads]
        steps:
            - name: Download Artifact
              uses: actions/download-artifact@v3
              with:
                  name: ${{ matrix.artifact_name }}
                  path: ./

            - name: Upload Artifact to Release
              id: upload-release-asset
              uses: softprops/action-gh-release@v1
              with:
                  token: ${{ secrets.GITHUB_TOKEN }}
                  tag_name: ${{ needs.create-release.outputs.tag }}
                  files: ./${{ matrix.artifact_name }}.zip
```

## Configuration

### Environment Variables

Non-sensitive configuration can be done in the workflow file itself

-   `MONGODB_TOOLS_DOWNLOAD` - A environment variable that links to a download for `mongodump`, a tool that can dump the contents of the database into a file.
    We use this to create a backup of the MongoDB database hosted on MongoDB Atlas.
-   `BACKEND_UPLOADS_DIR` - A environment variable that holds the absolute path to directory of the uploads folder within the backend server.
-   ` cron: "0 0 * * 0"` - Sets up a the backup action to run every month using a cron expression. You can use [crontab.guru](https://crontab.guru/) to build a cron expression.
    At the moment it runs the action at 00:00 on Sundays.

### Secrets

Sensitive information is stored as a repository secret on our GitHub repository. Here is a list of the follow secrets that can be configured

-   `MONGO_URI` - The [MongoDB connection string](https://www.mongodb.com/docs/manual/reference/connection-string/) used to connect to our `MainDB` database
-   `BACKEND_URI` - The ssh connection string to the backend. It's typically `root@123.45.678` where `123.45.678` represents your server's IP address.
-   `BACKEND_ROOT_PASS` - The password of the backend for the user you specified in the `BACKEND_URI`.
