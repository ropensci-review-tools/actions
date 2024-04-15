# Actions

GitHub actions for ropensci-review-tools workflows.

## ping-dev-team

Workflow to ping the rOpenSci Dev Team on any workflow failures. Team members
are taken from https://github.com/orgs/ropensci/teams/dev-guide, but those
members are unable to read using default workflow tokens, so hard-coded here.
This action is currently triggered on workflow failures in:

- [ropensci-org/badges](https://github.com/ropensci-org/badges)
- [ropensci-review-tools/dashboard](https://github.com/ropensci-review-tools/dashboard) (in [the `publish` workflow](https://github.com/ropensci-review-tools/dashboard/blob/main/.github/workflows/publish.yaml))
