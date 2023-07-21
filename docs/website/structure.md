# Structure

## Folder Structure

-   `src` - Contains
    -   `app` - Where the code is stored
        -   `classes` - Custom classes
        -   `modules` - Custom modules that each hold components
        -   `pages` - Pages on the site
        -   `services` - Services used by the site
        -   `settings` - Website specific settings
        -   `utils` - Utility code
    -   `assets` - Where images, articles, and other fixed assets are stored
        -   `blog-page-articles` - Stores articles by year
        -   `icons` - Stores COGS logo icons
        -   `images` - Stores images
        -   `js` - Stores Javascript
        -   `pictures-page-images` - Stores pictures page images by year and semester
    -   `_server_.ts` - The entry point of the website. It reads the command line arguments or environment variables to start a server in development or production mode.
-   `dist` - Where the release version of the website is stored once you build it.
-   `angular.json` - Configuration for Angular
-   `tsconfig.json` - Configuration for Typescript
-   `update_articles.py` - Used to add new articles to the blog page. See [Writing Blog Articles](blog.md).
-   `update_images.py` - Used to add new images to the pictures page. See [Uploading Pictures](pictures.md).

## NodeJS Scripts

-   `ng` - Runs the built website from the `dist` folder.
-   `start` - Starts a development server to serve the website locally.
-   `build` - Builds the website.
-   `watch` - Builds the website, and the watches for any file changes. If any files are changed the website is rebuilt.
-   `test` - Runs unit tests.
-   `generate` - Assuming you are developing under the `rucogs-infrastructure` mono-repo, this copies the generated code from the backend submodule's folder.
-   `selfhosted` - Scripts used for hosting the website on a server underneath the `rucogs/frontend` path.
    -   `selfhosted:build` - Builds the site with a base-href of `rucogs/frontend`.
    -   `selfhosted:copybuild` - Copies the built files to the `/var/www/rucogs`.
    -   `selfhosted:launch` - Runes `selfhosted:build` then `selfhosted:copybuild`.
-   `pretty` - Run the prettier formatter on the Typescript files within `src`.

!!! note

    To run a NodeJS script you have to run the follow code inside the repository's directory.

    ```bash
    > npm run script_name
    ```
