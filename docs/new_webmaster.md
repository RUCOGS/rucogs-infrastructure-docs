# New Webmaster Guide

## Overview

This documentation will assume you have prerequisite knowledge of frameworks being used, therefore teaching is out of the scope of this site. However, there will be recommended reading sections at the start of each section to give an entry point to learning a new topic.

For the ease of learning and consistency, all COGS infrastructure projects are written in Typescript. Please check out the [Typescript documentation](https://www.typescriptlang.org/docs/) if you are unfamiliar with the language.

## Tools

It's recommended to use [VSCode](https://code.visualstudio.com/download) to develop since many extensions are available to assist you.

### Code Formatting

We also use Prettier to automatically format our code. If you're using VSCode you can install the [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) extension. You should configure the extension to format your code on save, so the code always retains the same formatting. This can be done by turning on the `editor.formatOnSave` setting in VSCode.

### Version Control

We use Git for version control, with repositories hosted on GitHub. If you are unfamiliar with Git or GitHub you should check out the following tutorials:

- [Learning Git Branching](https://learngitbranching.js.org/?locale=en_US)
- [Introduction to Github](https://zarkom.notion.site/zarkom/Introduction-to-GitHub-202af6f64bbd4299b15f238dcd09d2a7#5177c6445c724460a400df2617e86bcd)

### RUCOGS Infrastructure

The [`rucogs-infrastructure`](https://github.com/rucogs/rucogs-infrastructure) repository is a mono-repo that contains all infrastructure projects as [submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules). We recommend git cloning the `rucogs-infrastructure` mono-repo and develop within the submodule folders of this mono-repo. This is because there are some scripts in each project that attempt to copy shared data from one project to another, and these scripts assume you are running the script in a submodule within the `rucogs-infrastructure` repository.

To clone the rucogs-infrastructure repository, run

```bash
> git clone https://github.com/rucogs/rucogs-infrastructure
```

Since Git doesn't download submodules when you clone it, you must then initialize the submodules using

```bash
> git submodule update --init
```

If you ever need to update the submodules to their latest versions from their source repositories, run

```bash
> git submodule update --remote
```

## Contributing

Please submit pull requests to the GitHub project for new changes. After submitting a pull request, you can await reviewing from an existing Webmaster. Once you are familiar with the code base, you will be given commit access to the repository. However, it's still recommended to get another set of eyes to review big changes such as new features, etc.

If the pull request changes features documented in the documentation, please also submit a pull request to the documentation repository to ensure it's up to date.

## Next Steps

You can start reading the various parts of the documentation, as well as do tutorials for the various frameworks to familiarize yourself with the codebase. The best way to learn is through small projects, so don't be afraid to create a tiny Angular project or Discord bot to play around with the frameworks used.
