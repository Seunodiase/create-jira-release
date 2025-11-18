# create-jira-release (GitHub Action)

Creates a new Jira release for a specific Jira project and assigns all relevant* Jira issue numbers to it.  
\* All Jira issue numbers (e.g. TEST-123) in commit messages since last Git tag.

## Prerequisites

In order to be able to use this GitHub Action, a custom Jira automation rule needs to be created first. Please refer to the screenshot below for the most important settings.

![Setup Jira automation rule](./setup-jira-automation-rule.png)

## Usage

See [action.yml](action.yml)

```yaml
steps:
- uses: actions/checkout@v4

- uses: GeoWerkstatt/create-jira-release@v1
  with:
    jira-project-key: 'TEST'
    jira-automation-webhook: ${{ secrets.JIRA_AUTOMATION_WEBHOOK }}
    build-version: v${{ env.VERSION }}
```

## Options

| key                       | description                           | required |
| ------------------------- | ------------------------------------- | -------- |
| `jira-project-key`        | Jira project identifier (e.g. _TEST_) | true     |
| `jira-automation-webhook` | Jira automation webhook url           | true     |
| `build-version`           | Version identifier                    | true     |

## Secrets

| key                               | description                                                                                                         | required |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------- | -------- |
| `secrets.JIRA_AUTOMATION_WEBHOOK` | Can be obtained or regenerated in the _Incoming webhook_ automation step of the corresponding Jira automation rule. | true     |

## Workflow Integration

This action can be integrated into your GitHub workflows. An example workflow that creates a Jira release when a pull request from `dev` to `main` is opened or updated is available at [`.github/workflows/create-jira-release-on-pr.yml`](.github/workflows/create-jira-release-on-pr.yml).

The example workflow:
- Triggers on pull requests from `dev` to `main` branch
- Automatically increments the minor version number
- Creates a Jira release with all issues found in commits since the last tag

## License

The scripts and documentation in this project are released under the [MIT License](LICENSE)
