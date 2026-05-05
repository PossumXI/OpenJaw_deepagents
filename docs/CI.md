# CI Operator Notes

This repository keeps its GitHub Actions workflows at the repository root under
`.github/workflows`.

The workflow registration guard for this repo is:

- all workflow YAML must pass `actionlint`;
- reusable workflows must stay in `.github/workflows`;
- release-package integration tests must be gated by actual package capability,
  not by a constant-disabled workflow condition.
- PR labeler contributor membership checks must degrade when
  `ORG_MEMBERSHIP_APP_ID` and `ORG_MEMBERSHIP_APP_PRIVATE_KEY` are absent.
  Size, file, and title labels still run with `GITHUB_TOKEN`; internal,
  external, and trusted-contributor labels require the membership app.

`release.yml` checks whether the selected package Makefile exposes an
`integration_test` target before running integration tests. That preserves
package-specific behavior without hiding a real integration test failure behind
`make integration_test || echo ...`.
