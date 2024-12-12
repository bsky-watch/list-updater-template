# List updater for Bluesky

This a template repository for setting up the list updater. Click "Use this template" button above to create your own copy.

This repository contains only a GitHub Workflow and an example configuration file. The actual code lives in https://github.com/bsky-watch/list-updater.

## Configuration

Copy `config.example.yaml` to `config.yaml` and customize as needed. List of all
available knobs is provided in a schema file in the https://github.com/bsky-watch/list-updater repo.

## Credentials

Credentials are provided using GitHub Secrets. Each account is stored in a separate secret, with the value of "`<login>:<app-password>`". Having a secret named `DEFAULT` is required - this account will be used for API queries.

## How/where does it run?

It is started automatically via GitHub Actions. You can view and adjust the
workflow in `.github/workflows/run.yaml` file. By default it will run every 3 hours. Note that GitHub Actions provide a [free quota](https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-actions/about-billing-for-github-actions#included-storage-and-minutes) of 2000 minutes per month. If, with your configuration file, a single run takes less than 8 minutes - it should fit nicely into that free quota. If it takes longer - you can reduce the frequency and/or set up a self-hosted runner.
