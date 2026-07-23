# Actions

GitHub actions for ropensci-review-tools workflows.

## ping-dev-team

Workflow to ping the rOpenSci Dev Team on any workflow failures. Team members
are taken from https://github.com/orgs/ropensci/teams/dev-guide, but those
members are unable to read using default workflow tokens, so hard-coded here.
This action is currently triggered on workflow failures in:

- [ropensci-org/badges](https://github.com/ropensci-org/badges)
- [ropensci-review-tools/dashboard](https://github.com/ropensci-review-tools/dashboard) (in [the `publish` workflow](https://github.com/ropensci-review-tools/dashboard/blob/main/.github/workflows/publish.yaml))

## push-to-elsewhere

Composite action to mirror a branch (with tags) to non-GitHub remotes.
Mirrors are passed by the caller, so none are hard-coded here:

```yaml
name: push-to-elsewhere

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

concurrency:
  group: push-to-elsewhere
  cancel-in-progress: false

jobs:
  mirror:
    runs-on: ubuntu-latest
    steps:
      - uses: ropensci-review-tools/actions/push-to-elsewhere@main
        with:
          mirrors: |
            codeberg=https://${{ secrets.UNAME }}:${{ secrets.CODEBERG }}@codeberg.org/ropensci-review-tools/srr.git
            codefloe=https://${{ secrets.UNAME }}:${{ secrets.CODEFLOE }}@codefloe.com/ropensci-review-tools/srr.git
```

On pull requests the step completes as a no-op so a required check reads
green rather than skipped; mirroring only happens on pushes to `main`
(override with the `branch` input).
