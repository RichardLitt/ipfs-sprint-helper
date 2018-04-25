# sprint-bot

## Purpose

- Creates meeting pads (using Cryptpad) with template filled out
- Creates issue linking to the pads on a regular interval (via cron syntax)
- Assigns moderator + notetaker based on previous facilitors

Future tasks:

- Announce before meetings start on IRC
- Setup live-streaming via Youtube automatically (Youtube + Zoom integration)

## Running

- `yarn` to install dependencies (or `npm install` if you like to wait)
- Export all neccessary environment variables from below
- `yarn start` to create one test issue
- `NODE_ENV=production yarn start` to start "cron-mode", it'll only create the issue
  when the cron syntax is triggering it to

## Cron schedule and dates

The cron schedule decides when sprint-helper should create the issue. Since the
date of the meeting is considered 6 days after this date, you should schedule
sprint-helper to run the day after a meeting is supposed to be had.

Notice: The value of "6 days" is currently hardcoded since we only have weekly
meetings. This would have to be adjusted or made into a variable if we have non-weekly
meetings

## Templates

The following templates should exists for sprint-helper to be able to create issues + cryptpad
for you:

- Cryptpad Template. Creates a cryptpad based on this template.
  - Has variables `$MODERATOR`, `$NOTETAKER` and `$DATE`
- Issue Template. Creates the issue based on this template
  - Has variables `$MODERATOR`, `$NOTETAKER` and `$CRYPTPAD`
- Facilitators file. A JSON file with a array of strings, each string is a Github profile
  that can be moderator or notetaker. Should contain people who are at every meeting.

## Configuration (environment variables)

Each deployed instance of sprint-bot should have a few different values, as we
have multiple meetings that needs to be scheduled each week.

- `SPRINT_HELPER_REPOSITORY` decides which repository the issue should be created at
- `SPRINT_HELPER_CRON_SCHEDULE` decides how often the issue should be created
- `SPRINT_HELPER_CRYPTPAD_TEMPLATE` decides which template to use for the cryptpad
- `SPRINT_HELPER_FACILITATORS_FILE` decides which JSON file to grab facilitators from
- `SPRINT_HELPER_ISSUE_TITLE` decides the title of the issue
- `SPRINT_HELPER_ISSUE_TEMPLATE` decides which template to use for creating the issue
- `SPRINT_HELPER_GITHUB_AUTH_TOKEN` is the token for authorizing the issue-creation

Examples values:

- `SPRINT_HELPER_REPOSITORY` = `ipfs/pm`
- `SPRINT_HELPER_CRON_SCHEDULE` = `00 18 * * 1` (At 18:00 on Mondays, see https://crontab.guru)
- `SPRINT_HELPER_CRYPTPAD_TEMPLATE` = `ipfs/pm,templates/all-hands-pad-template.md`
- `SPRINT_HELPER_ISSUE_TITLE` = `All Hands` (The date of the meeting gets appended to the title)
- `SPRINT_HELPER_ISSUE_TEMPLATE` = `ipfs/pm,templates/all-hands-issue-template.md`
- `SPRINT_HELPER_GITHUB_AUTH_TOKEN` = Get it from https://github.com/settings/tokens/new

## Deploy

*TOWRITE*

Basically, setup a git remote pointing to dokku, set the config values from inside
the instance and then push it!

# License

MIT 2018 Protocol Labs
