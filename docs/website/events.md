# Managing Events

## Prerequisites

1. Make sure you have [Python](https://www.python.org/downloads/) installed on your computer.
2. Make sure you have [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) installed on your computer.
3. Clone the [website GitHub repository](https://github.com/rucogs/rucogs.github.io) locally if you don't have it already

    ```bash
    > git clone https://github.com/rucogs/rucogs.github.io
    ```

## Event Page Template

Event pages tend to follow the same template, with a count down, a signup form, and an itinerary. Settings for the event are stored on the event page's component itself. Events also might have an event banner associated with it, which is displayed on the homepage of the website. 

Event banners can be enabled/disabled by commenting/uncommentiing the `<app-event-header></app-event-header>` in `src\app\pages\home\home\home-page.component.html`. The contents of the event banner are found in the `src\app\modules\_core\event-header\event-header.component.html` file.

!!! note "Variables"

    - `startDate` - Start date of the event
    - `eventActive` - Whether the event is in progress or not.
        - If `false`, a timer will be shown that counts down to the kickoff date and time.
        - If  `true`, then the `itchioLink` will be displayed, and the signup form will be renamed to "Late Signup Form".

!!! note "Sections"

    - `Header` section
        - This is usually controlled by variables on the event page's component
    - `Itinerary` section
        - Displays the itinerary for the game jam.
        - Each itinerary entry is displayed as an `app-event-card`, and has a main section and a Google Maps embed.
        - Make sure the Google Maps `iframe` embed has it's `src` attribute filled out to the correct value.
            - This `src` value can be obtained by going to Google Maps
            - Finding the location of the event
            - Clicking on Share -> Embed a map
            - Copy the string from the `src` section of the `iframe` that Google Maps generates for you.
    - `FAQ` section
        - Displays frequently asked questions.
        - Feel free to add or remove questions as needed.

## Scarlet Game Jam

1.  Uncomment the `<app-event-header></app-event-header>` in `src\app\pages\home\home\home-page.component.html`
2.  Ensure `src\app\modules\_core\event-header\event-header.component.html` has the scarlet game jam `app-section` uncommented.
3.  Uncomment the Scarlet Game Jam PageLink in `src/_settings.ts`  
4.  Open `src\app\pages\scarlet-game-jam\scarlet-game-jam\scarlet-game-jam-page.component.ts`

    -   Edit the variables of the component to the correct values

    !!! note "Variables"

        - `startDate` - Start date of the event
        - `endDate` - End date of the event
        - `startDateTime` - Time interval of the kickoff event during the startDate
        - `endDateTime` - Time interval of the closing ceremony during the endDate
        - `merchLink` - Link to the merch store
        - `signupLink` - Link to the game jam signup form
        - `itchioLink` - Link to the game jam Itch.io page
        - `startDateEventPage` - GetInvolved event page for the kickoff event
        - `endDateEventPage` - GetInvolved event page for the closing ceremony
        - `eventActive` - Whether the event is in progress or not.
            - If `false`, a timer will be shown that counts down to the kickoff date and time.
            - If  `true`, then the `itchioLink` will be displayed, and the signup form will be renamed to "Late Signup Form".

5.  Tweak the `scarlet-game-jam-page.component.html` to your needs

    !!! note "Sections"

        - `Collaborations` section
            - Displays collaborations with other clubs and organizations if there is any.
            - Comment out collaborations that don't exist and feel free to comment out the entire section if there are no collaborations.
        - `Itinerary` section
            - Displays the itinerary for the game jam.
            - See [Event Page Template](#event-page-template).
        - `Merch` section
            - Displays the merch link.
        - `FAQ` section
            - Displays frequently asked questions.
            - See [Event Page Template](#event-page-template).

## Global Game Jam

1.  Uncomment the `<app-event-header></app-event-header>` in `src\app\pages\home\home\home-page.component.html`
2.  Ensure `src\app\modules\_core\event-header\event-header.component.html` has the global game jam `app-section` uncommented.
3.  Uncomment the Global Game Jam PageLink in `src/_settings.ts`
4.  Open `web\src\app\pages\global-game-jam\global-game-jam\global-game-jam-page.component.ts`

    -   Edit the variables of the component to the correct values

    !!! note "Variables"

        - `startDate` - Start date and time of the event
        - `eventActive` - Whether the event is in progress or not
            - If `false`, a timer will be shown that counts down to the kickoff date and time.
            - If  `true`, then the Itch.io Link will be displayed, and the signup form will be renamed to "Late Signup Form".
        - `signupLink` - Link to the Global Game Jam signup form
        - `siteLink` - Link to the Global Game Jam site link

5.  Tweak the `global-game-jam-page.component.html` to your needs

    !!! note "Sections"

        - `Itinerary` section
            - Displays the itinerary for the game jam.
            - See [Event Page Template](#event-page-template).
        - `FAQ` section
            - Displays frequently asked questions.
            - See [Event Page Template](#event-page-template).

## New Events

If you need to make a new event page feel free to base it off of the Scarlet Game Jam event page.
