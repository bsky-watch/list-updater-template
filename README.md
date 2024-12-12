# List updater for Bluesky

This a template repository for setting up the list updater. Click "Use this template" button above to create your own copy.

## Configuration

Copy `config.example.yaml` to `config.yaml` and customize as needed. List of all
available knobs is provided in a schema file in the github.com/bsky-watch/list-labeler repo.

## Credentials

Credentials are provided using GitHub Secrets. Each account is stored in a separate secret, with the value of "`<login>:<app-password>`". Having a secret named `DEFAULT` is required - this account will be used for API queries.


