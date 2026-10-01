# Forever WoW Beta Bluepost → Discord

A tiny GitHub Actions watcher for Blizzard's official Blue Tracker. It forwards only Blizzard posts whose topic belongs to **WoW: Forever Beta Discussion** (category `349`) to a Discord webhook.

## What it does

- polls every 5 minutes via GitHub Actions
- filters Blizzard tracker activity to the Forever Beta forum
- posts author, topic title, excerpt, timestamp, and direct link to Discord
- suppresses duplicates without a database
- bootstraps silently on the first run, so old blueposts are not dumped into the channel
- can also be run manually from **Actions → Forever WoW Beta Blueposts → Run workflow**

## Required repository secret

Create an Actions secret named:

`DISCORD_WEBHOOK_URL`

Its value is the Discord channel webhook URL. Do **not** commit the URL to the repository.

Path in GitHub:

**Settings → Secrets and variables → Actions → New repository secret**

## Duplicate suppression

The watcher stores the latest processed Blizzard post ID in the Discord webhook's own name:

`ForeverBlueposts:last=<postId>`

The individual Discord messages override their sender display name to `Forever Blueposts`, so this state marker is not shown as the message author.

## Notes

GitHub scheduled workflows can be delayed during periods of high Actions load. The five-minute cron is therefore a target polling cadence, not a real-time delivery guarantee.
