# Structure

## Folder Structure

-   `src` - Contains
    -   `server.ts` - The entry point of the discord bot. It reads the command line arguments or environment variables to start a server in devlopment or production mode.
    -   `config` - Stores config files that change how the discord bot runs. See the [Config section](#config) for more information
    -   `commands` - Contains code for slash commands. Each slash command is represented by a script that exports a `Command` object, which defines the command and the handlers for it. Note that sub commands are handled manually by each command script.
    -   `_tools` - Contains code used by Node.JS scripts defined in our `package.json`.
    -   `generated` - Auto-generated code based on our GraphQL schema
    -   `misc` - Contains miscallenous helper code
    -   `shared` - Code that's shared between the backend and frontends
-   `dist` - Where the release version of the discord bot is stored once you build it.
-   `gulpfile.js` - Script that automates copying assets over when you build the discord bot.
-   `rucogs-discord.service` - Service file for hosting discord bot. See [DevOps/Hosting](../devops/hosting.md) for more information.
-   `tsconfig.json` - Configuration for Typescript

## NodeJS Scripts

-   `start` - Runs the built discord bot from the `dist` folder.
-   `start:recompile` - Compiles the discord bot and then runs it.
-   `start:rebuild` - Regenerates and recompiles the discord bot, and then runs it.
-   `compile:app` - Cleans the `dist` directory and recompiles the discord bot.
-   `compile:tools` - Cleans the `dist` directory and recompile the discord bot in tool mode, which basically includes the `src/_tools` folder in the final build.
-   `clean` - Deletes the `dist` directory.
-   `deploy-commands:production` - Deploys the slash commands to the server specified by the `auth.config.json` file. See the [Auth Config section](config.md#auth-config) for more information.
-   `deploy-commands:development` - Deploys the slash commands to the server specified by the `auth.debug.config.json` file. See the [Auth Config section](config.md#auth-config) for more information.
-   `build` - Cleans the `dist` directory, regenerates the autogenerated code, and then recompiles the discord bot.
-   `generate` - Assuming you are developing under the `rucogs-infrastructure` mono-repo, this copies the generated code from the backend submodule's folder.

!!! note

    To run a NodeJS script you have to run the follow code inside the repository's directory.

    ```bash
    > npm run script_name
    ```