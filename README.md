# Reusable workflows for GitHub actions

https://docs.github.com/en/actions/using-workflows/reusing-workflows#calling-a-reusable-workflow

---

> **Warning**
> 
> ## This is a public repo!
>
> **Be extra careful with any commits that you make to this repo.**
>
> GitHub [does not support calling reusable workflows from private repos](https://docs.github.com/en/actions/using-workflows/reusing-workflows#limitations), so until / unless GitHub adds support for calling them from private repos, this repo needs to be public.
>
> Some steps you can take to make sure we keep this repo safe:
>
> - Pair with a CI/CD SME and/or someone from the S&C team
>   - This will help catch any issues early, before they've been pushed up to the repo
> - **On your local machine**, [squash the commits of a branch](https://stackoverflow.com/questions/6934752/combining-multiple-commits-before-pushing-in-git) before pushing the branch up for code review
>   - This will help avoid leaking secrets that might have been commited during local development, but are not readily apparent when looking at the "Files changed" tab in a PR

---

## Run jobs when PR is ready for review

```yaml
name: Call ready for review workflow

# In order to work with dependabot PRs, we need to use `pull_request_target`
# instead of `pull_request`.
#
# See:
# - https://github.com/dependabot/dependabot-core/issues/3253#issuecomment-795140576
# - https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#pull_request_target
on:
  pull_request_target:
    types: [opened, ready_for_review]

jobs:
  ready_for_review:
    uses: ForwardFinancing/github-workflows/.github/workflows/ready-for-review.yml@main
    secrets:
      SLACK_READY_FOR_REVIEW_WEBHOOK_URL: ${{ secrets.SLACK_READY_FOR_REVIEW_WEBHOOK_URL }}
```
