# Discord-ICS-Sync-Bot

**tl;dr**: reads the scheduled events for a server and publishes an ICS calendar that contains them

_You'll need to feel confident with your terminal to deploy and use this project!_

## Setup

### Requirements

1. Ensure you have [the Serverless Framework installed](https://www.serverless.com/framework/docs/getting-started)
    - Ensure that you have [AWS credentials configured](https://serverless.com/framework/docs/providers/aws/guide/credentials/)
1. Ensure you have [Node.js](https://nodejs.org/en/download) and [NPM](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) in your local environment

### Process

1. Clone this repository
    - `cd` into the repository directory and run `npm install`
1. Create a Discord Application in the [Discord Developer Portal](https://discord.com/developers/applications)
   - Click the `BOT` button in the left-hand navigation menu (this page contains your bot token, which you will set the environment variable `BOT_TOKEN` with)
1. Create a file named `.env` in the repository directory, and define the following environment variables:
   - `CALENDAR_NAME` - this will be shown in applications that import the calendar
   - `BOT_TOKEN` - Get this from the [Discord Developer Portal](https://discord.com/developers/applications) `Bot` page
   - `GUILD_ID` - enable Developer Mode in your Discord client, and then right click the server you intend to add this application to. Click `Copy Server ID` at the bottom of the context menu
1. In the [Discord Developer Portal](https://discord.com/developers/applications) click the `OAuth2` button and then `URL GENERATOR`
    - Enable the `bot` scope and enable the `Manage Events` permission (this may not be necessary to read the events, I need to check)
    - Use the generated link in a browser that you are signed into Discord with. It will prompt you to grant server access to your application
1. In the repository directory, run `sls deploy` 
    - Once the deployment is created, serverless will output a URL ending in `/api/calendar` - **use this to import your Discord event calendar into a Calendar application!**


## Notes

- It can take 8-12 hours for an event to appear in Google Calendar after it is added to the ICS calendar ([third party site](https://help.cheqroom.com/en/articles/1502123-why-is-my-google-calendar-sync-slow-or-not-updating-at-all))

### Handy docs:

- Discord API docs
    - [List Scheduled Events for Guild](https://discord.com/developers/docs/resources/guild-scheduled-event#list-scheduled-events-for-guild)
    - [Reference docs for Scheduled Event objects](https://discord.com/developers/docs/resources/guild-scheduled-event#guild-scheduled-event-object)
    - If the URL isn't accessible by bot, there [may be a header that can be passed to enable it?](https://support.discord.com/hc/en-us/community/posts/4410436617879/comments/4410830664087)
- Tutorials
    - [Bad tutorial (no code logic, only setting bot up)](https://www.ionos.com/digitalguide/server/know-how/creating-discord-bot/)
