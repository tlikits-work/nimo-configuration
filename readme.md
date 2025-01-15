# Nimo Configuration

## Introduction

This repository provides the ability to synchronize configurations across different environments.

## How it works

The configuration files will be stored in the `/config` directory under the specific storage where they are actually kept. For example, `/config/dynamodb` for those stored in DynamoDB.

To update the configuration in each environment, start by making a pull request to update the branch for the lower environment first, then proceed to make a pull request for the upper environment.

Once the pull request is accepted and merged, GitHub will automatically trigger an action that will check the configuration files that were changed. It will then update the configuration in the target storage.

## Branches and Environments

- Development - `development`
- UAT - `uat`
- Production - `main`

## Structure

```
/config # Level-0
  /dynamodb # Level-1: Defines the type of storage
    /nimo # Level-2: Defines the storage name (in this case, table name)
      /modules # Level-3+: Any directory - for grouping the configurations
        purpose-home-loan.json
        purpose-vehicle-loan.json
        ...
      assessmentpipeline.json # Level-3: Or can be a configuration file
    /...
      ...

[diff.txt]
```

## Process to Update Configuration in Dev Branch

1. Create a branch to update the configuration. The branch should be related to JIRA, to allow tracking the change with the requirement.
2. Update the configuration file in the branch.
3. Open a PR to the `development` environment branch.
4. Merge the change and let the action run.
5. Test the configuration against the environment.
6. Update your JIRA.

## Process to Update Configuration in Upper Environment Branch

1. Open a PR from the one-level lower environment branch based on the upper environment branch.
2. Merge the change and let the action run.
3. Test the configuration against the environment.

## Process to Provide a Hotfix on a Specific Environment

1. Create a branch to update the configuration based on a specific environment branch. The branch should be related to JIRA, to allow reference to the issue it needs to fix.
2. Update the configuration file in the branch.
3. Open a Pull Request to the specific environment branch.
4. Merge the change and let the action run.
5. Test the configuration against the environment.
6. Update your JIRA.
