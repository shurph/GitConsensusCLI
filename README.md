# GitConsensus

This simple project allows github projects to be automated. It uses "reaction" as a voting mechanism to automatically
merge (or close) pull requests.

## Consensus Rules

The file `.gitconsensus.yaml` needs to be placed in the repository to be managed. Any rule set to `false` or ommitted
will be skipped.

```yaml
# minimum number of votes
quorum: 5

# Required percentage of "yes" votes
threshold: 0.65

# Only process votes by contributors
contributors_only: false

# Only process votes by collaborators
collaborators_only: false

# When defined only process votes from these github users
whitelist:
  - alice
  - bob
  - carol

# Number of days after last commit before issue can be merged
mergedelay: 3

# Number of days after last commit before issue is autoclosed
timeout: 30
```

## Authentication

```shell
gitconsensus auth
```

You will be asked for your username, password, and 2fa token (if configured). This will be used to get an authentication
token from Github that will be used in place of your username and password (which are never saved).

## Merge

Merge all pull requests that meet consensus rules.

```shell
gitconsensus merge USERNAME REPOSITORY
```

## Close

Close all pull requests that have passed the "timeout" date (if it is set).

```shell
gitconsensus close USERNAME REPOSITORY
```

## Label Overrides

Any Pull Request with the `WIP` or `DONTMERGE` label (case insensitive) will be skipped over.
