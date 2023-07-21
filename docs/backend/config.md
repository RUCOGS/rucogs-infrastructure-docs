# Config

The behavior of the server is determined by config files located underneath `src/config`. Config files end in `.config.json`, and are automatically ignored by the repository's `.gitignore` to avoid leaking sensitive information into the git commit history.

There are two config files needed:

- `auth.config.json`
- `server.config.json`

The repository provides templates files ending in `.config.template.json` for the two types of config files. To make a real config file, duplicate a template and remove the `.template` part of the config file's name.

## Auth config

- `type` - The type of server this config file is for. It can be set to either `"production"` or `"debug"`. If you are using `"debug"`, make sure to also name the config as `auth.debug.config.json`.
- `rootUsers` - An array of root users that can have complete access to the backend.
  - Users are objects with a `username` and a `password`.
- `jwt` - Settings for JSON web tokens. We use JSON web tokens for authentication
  - `secret` - A string used to sign a JSON web token. This can be set to anything, but must be kept a secret.
- `oauth` - Settings for authentication
  - `discord` - Settings for discord authentication.
    - `strategyConfig`
      - `clientID` - Discord OAuth client ID. You can find this on the Discord developers dashboard on the COGS discord account.
      - `clientSecret` - Discord OAuth client secret. You ask an existing webmaster for the secret.
  - `google` - Settings for google authentication. Even though Google login functionality is implemented in both the backend and the frontend, it is currently unused in favor of only having Discord authentication. Therefore, filling out the google settings is optional.
    - `strategyConfig`
      - `clientID` - Google OAuth client ID. You can find this on the Google developer dashboard on the COGS google account.
      - `clientSecret` - Google OAuth client secret. You ask an existing webmaster for the secret.

## Server Config

- `type` - The type of server this config file is for. It can be set to either `"production"` or `"debug"`. If you are using `"debug"`, make sure to also name the config as `server.debug.config.json`.
- `mongoDB` - MongoDB settings
  - `url` - Connection string to MongoDB database.
  - `dbName` - Name of the database. For production it should be `maindb`.
- `nodemailer` - Nodemailer settings. See the [Nodemailer section](#nodemailer) for more information.
- `backendDomain` - The domain for the backend.
- `frontendDomain` - The domain for the frontend.

### Nodemailer

For debugging purposes you can use a free platform like [mailtrap](https://mailtrap.io/) to preview emails.

```yaml
"nodemailer":
  {
    "host": "smtp.mailtrap.io",
    "auth": { "user": "", "pass": "" },
    "port": 2525,
  }
```

For the release config you can use Gmail transport settings, so the emails are sent using our noreply gmail account:

```yaml
"nodemailer":
  {
    "service": "Gmail",
    "auth": { "user": "rutgerscogsnoreply@gmail.com", "pass": "" },
  }
```
