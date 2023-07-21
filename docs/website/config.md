# Config

The behavior of the website is determined by `src/_settings.ts` file.

- `SettingsService`
  - `General` - General settings.
    - `pageLinks` - Array of page links that will be shown on the header navigation bar. Commenting out a page link hides it from the navigation bar.
    - `instagramLink` - Link to the COGS Instagram page.
    - `twitterLink` - Link to the COGS Twitter page.
    - `discordLink` - Invite link to the COGS Discord server.
    - `mailingListLink` - Link to signup for the COGS mailing list.
    - `icons` - Imported icons to be registered for use in `mat-icon` components.
    - `defaultAvatarSrc` - Link to the the default user avatar image.
    - `defaultCardImageSrc` - Link to the default project card image.
  - `Backend` - Backend settings.
    - `backendDomain` - Domain the backend is hosted on.
    - `backendRelativeBaseUrl` - Relative path to the backend from the `backendDomain`.
    - `graphQLRelativePath` - Relative to the GraphQL endpoint from the `backendDomain`.
    - `selfHostedPrefix` - Prefix that indicates whether a file is self-hosted on the backend or not.
    - `cdnRelativePath` - Relative path to the cdn from the `backendDomain`.
