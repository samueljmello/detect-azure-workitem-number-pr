# Detect Azure Workitem Numbers In Pull Requests
A reusable workflow that will detect Azure workitem numbers in the title or body of a pull request.

## Usage
To use this shared workflow in your repository, simply [create a new workflow](https://docs.github.com/en/actions/quickstart) file with the following contents:

```yaml
name: Pull Request Audit
on:
  pull_request:
    types:
      - opened
      - reopened
      - synchronize
      - edited
jobs:
  scan:
    name: Use Shared Workflow
    uses: samueljmello/detect-azure-workitem-number-pr/.github/workflows/pull-request-audit-shared.yaml@main
```

This will enable the shared workflow for all default pull request (PR) events (`opened`, `reopened`, `synchronize`) as well as the `edit` event.

The script has a failure and success condition that will add comments appropriately, and add/remove labels depending on the outcome.

If the last comment on the PR is from this workflow, it will avoid making duplicates.

Additionally, the failure status reports `1` so that your workflow execution shows as `failed`. This will allow you to utilize the workflow with branch protection rules to block PR that do not have a workitem number in the title or body.