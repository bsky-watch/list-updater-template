# List updater for Bluesky

This a template repository for setting up the list updater. Click "Use this template" button above to create your own copy.

This repository contains only a GitHub Workflow and an example configuration file. The actual code lives in https://github.com/bsky-watch/list-updater.

## Configuration

Copy `config.example.yaml` to `config.yaml` and customize as needed. List of all
available knobs is provided in a schema file in the https://github.com/bsky-watch/list-updater repo.

## Credentials

Credentials are provided using GitHub Secrets. Each account is stored in a separate secret, with the value of "`<login>:<app-password>`". Having a secret named `DEFAULT` is required - this account will be used for API queries.

## Bluesky's rate limits

One account is only allowed to create about 11000 records a day. (Each list entry counts as a separate record.) After that limit is reached, the account effectively becomes read-only for the rest of the day. 

List updater respects the rate limits and will not keep hammering Bluesky with pointless requests if it detects that it's being throttled, but it has no safeguards against exhausting the daily record creation quota. So if you anticipate adding a lot of list entries - be ready for that. 

You can create a separate account to host the list, to avoid making your main one read-only. If you do - be sure to clearly link it in the bio of your main account and the other way around, so that subscribers can verify that it indeed belongs to you.

## How/where does it run?

It is started automatically via GitHub Actions. You can view and adjust the
workflow in `.github/workflows/run.yaml` file. By default it will run every 3 hours. Note that GitHub Actions provide a [free quota](https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-actions/about-billing-for-github-actions#included-storage-and-minutes) of 2000 minutes per month. If, with your configuration file, a single run takes less than 8 minutes - it should fit nicely into that free quota. If it takes longer - you can reduce the frequency and/or set up a self-hosted runner.

## Accuracy

Where possible, it uses low-level `com.atproto.repo.listRecords` method to get
the list of entries. For things that require records from many different
accounts (e.g., a list of followers) it sends a query to AppView instead, and
AppView may take blocks into account and not return you a complete list.

You can minimize the possible impact of that by ensuring that your `DEFAULT` account is not discoverable:

1) create a new Bluesky account that has no public association to you or the lists you plan to add
2) do not use that account for anything else
3) from time to time check the log of a run in the Actions tab, to ensure that
  DID or handle of that account don't appear there.
