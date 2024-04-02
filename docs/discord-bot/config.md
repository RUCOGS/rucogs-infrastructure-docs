# Config

The behavior of the discord bot is determined by config files located underneath `src/config`. Config files end in `.config.json`, and are automatically ignored by the repository's `.gitignore` to avoid leaking sensitive information into the git commit history.

There are two config files needed:

-   `auth.config.json`
-   `server.config.json`

The repository provides templates files ending in `.config.template.json` for the two types of config files. To make a real config file, duplicate a template and remove the `.template` part of the config file's name.

## Auth config

-   `type` - The type of server this config file is for. It can be set to either `"production"` or `"debug"`. If you are using `"debug"`, make sure to also name the config as `auth.debug.config.json`.
-   `backendRootUser` - The user credentials used to log into the backend for full API access
    -   `username` - Username of the root user
    -   `password` - Password of the root user
-   `bot` - Settings for the Discord bot
    -   `clientId` - Discord bot client ID. You can find this on the Discord developers dashboard on the COGS discord account.
    -   `guildId` - The id of the guild the bot is operating in. For the debug config this should be set to the COGS Test Server, while for the production config it should be set to the official COGS Server.
    -   `token` - Discord bot client secret. You ask an existing webmaster for the secret.

## Server Config

-   `type` - The type of server this config file is for. It can be set to either `"production"` or `"debug"`. If you are using `"debug"`, make sure to also name the config as `server.debug.config.json`.
-   `backendDomain` - The domain for the backend.
-   `cdnDomain` - The domain for the CDN.
-   `cdnHttpsPrefix` - Https prefix for the CDN domain. This can be set to `http://` or `https://`.
-   `httpsPrefix` - Https prefix for the backend domain. This can be set to `http://` or `https://`.
-   `wssPrefix` - WebSocket prefix for the backend domain. This can be set to `ws://` or `wss://`.
-   `cdnRelativePath` - The path of the CDN relative to the `cdnDomain`.
-   `dynamicCdnRelativePath` - The path for getting dynamically generated images from the CDN, relative to the `cdnDomain`.
-   `graphqlRelativePath` - The path to the GraphQL endpoint relative to the `backendDomain`.
-   `selfHostedPrefix` - Prefix for indicated an image is self-hosted. By default it's `cdn://`
-   `archiveCategoryId` - Id of the archive category of the discord server that the bot is operating in. The discord server the bot is operating in is specified by the Auth config.

### Examples

Since the server config doesn't contain any sensitive information, the configs used for production and debugging are shown below:

**server.config.json**

```json
{
    "type": "production",
    "backendDomain": "localhost:3000",
    "cdnDomain": "atlinx.net/rucogs/backend",
    "cdnHttpsPrefix": "https://",
    "httpsPrefix": "http://",
    "wssPrefix": "ws://",
    "cdnRelativePath": "/cdn",
    "dynamicCdnRelativePath": "/cdn/dynamic",
    "graphqlRelativePath": "/graphql",
    "selfHostedPrefix": "cdn://",
    "archiveCategoryId": "804127935987843083"
}
```

**server.config.debug.json**

```json
{
    "type": "debug",
    "backendDomain": "localhost:3000",
    "cdnDomain": "localhost:3000",
    "cdnHttpsPrefix": "http://",
    "httpsPrefix": "http://",
    "wssPrefix": "ws://",
    "cdnRelativePath": "/cdn",
    "dynamicCdnRelativePath": "/cdn/dynamic",
    "graphqlRelativePath": "/graphql",
    "selfHostedPrefix": "cdn://",
    "archiveCategoryId": "799858313835708446"
}
```
