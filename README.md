# Reusable workflows for GitHub actions

https://docs.github.com/en/actions/using-workflows/reusing-workflows#calling-a-reusable-workflow

## Notify Slack when PR is ready for review

```yaml
name: Notify Slack if Ready for Review

on:
  pull_request_target:
    types: [opened, ready_for_review]

jobs:
  ready-for-review:
    uses: ForwardFinancing/github-workflows/.github/workflows/ready-for-review.yml@main
    secrets:
      SLACK_READY_FOR_REVIEW_WEBHOOK_URL: ${{ secrets.SLACK_READY_FOR_REVIEW_WEBHOOK_URL }}
```
