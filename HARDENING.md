<!-- markdownlint-disable -->

# Hardening Report: clowdhaus--argo-cd-action/v3.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **clowdhaus--argo-cd-action/v3.2.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference GitHub Actions using mutable version tags (@v6) instead of pinned 40-character commit SHA digests. This exposes the workflow to supply-chain attacks if the tag is moved to a malicious commit. Affected references: `actions/checkout@v6` (3 occurrences in integration.yml, 1 in release.yml) and `actions/setup-node@v6` (1 occurrence in release.yml). Each should be replaced with a full SHA pin, e.g. `actions/checkout@<40-char-sha> # v6`.

Locations:

- `.github/workflows/integration.yml:30`
- `.github/workflows/integration.yml:50`
- `.github/workflows/integration.yml:68`
- `.github/workflows/release.yml:14`
- `.github/workflows/release.yml:19`

### missing-permissions (severity: medium)

Neither `integration.yml` nor `release.yml` declares a top-level `permissions:` block, and no individual job within either file declares its own `permissions:` block. Without explicit permissions, workflows run with the default repository token permissions, which may be broader than necessary (e.g. write access to contents, pull-requests, etc.). A minimal `permissions:` block should be added at the top level or per-job.

Locations:

- `.github/workflows/integration.yml:1`
- `.github/workflows/release.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files: (1) Pinned all action references to full 40-character commit SHAs — actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 (4 occurrences) and actions/setup-node@v6 → @249970729cb0ef3589644e2896645e5dc5ba9c38 (1 occurrence), with the original tag preserved as a comment. (2) Added `permissions: {}` at the top level of both integration.yml and release.yml to deny all default permissions. For release.yml, the release job is granted `contents: write` at the job level since semantic-release needs to create tags and GitHub releases.

