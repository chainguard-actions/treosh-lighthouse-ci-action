<!-- markdownlint-disable -->

# Hardening Report: treosh--lighthouse-ci-action/12.6.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **treosh--lighthouse-ci-action/12.6.2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable version tags (@v6) instead of immutable 40-character commit SHA digests. This exposes the workflow to supply-chain attacks where a tag could be silently moved to point to malicious code. Affected references: `actions/checkout@v6` and `actions/setup-node@v6`.

Locations:

- `.github/workflows/main.yml:6`
- `.github/workflows/main.yml:7`
- `.github/workflows/LHCI-assert-on-budget.yml:8`
- `.github/workflows/LHCI-assert-on-lighthouserc.yml:8`
- `.github/workflows/LHCI-static-dist-dir.yml:8`
- `.github/workflows/LHCI-upload-to-private-server.yml:9`
- `.github/workflows/LHCI-urls-interpolation.yml:8`

### missing-permissions (severity: medium)

None of the workflow files define a top-level `permissions:` block, and no job within any workflow defines its own `permissions:` block. Without explicit permissions, workflows run with the default (potentially broad) GITHUB_TOKEN permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/main.yml:1`
- `.github/workflows/LHCI-assert-on-budget.yml:1`
- `.github/workflows/LHCI-assert-on-lighthouserc.yml:2`
- `.github/workflows/LHCI-static-dist-dir.yml:1`
- `.github/workflows/LHCI-upload-to-private-server.yml:2`
- `.github/workflows/LHCI-urls-interpolation.yml:2`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 6 workflow files: (1) Pinned actions/checkout@v6 to full SHA d23441a48e516b6c34aea4fa41551a30e30af803 and actions/setup-node@v6 to 249970729cb0ef3589644e2896645e5dc5ba9c38 with # v6 comments for readability. (2) Added top-level `permissions: {}` block to all 6 workflow files to enforce least-privilege GITHUB_TOKEN permissions.

