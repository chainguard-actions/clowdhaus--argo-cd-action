<!-- markdownlint-disable -->

# Hardening Report: clowdhaus--argo-cd-action/v4.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **clowdhaus--argo-cd-action/v4.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow uses actions pinned to mutable version tags instead of immutable 40-character commit SHAs. In integration.yml: `actions/checkout@v6` (lines ~29, ~68, ~90) and `actions/setup-node@v6` (line ~33). These tag-based refs can be silently moved to point to different (potentially malicious) commits without any change to the workflow file.

Locations:

- `.github/workflows/integration.yml:29`
- `.github/workflows/integration.yml:33`

### unpinned-uses (severity: high)

Workflow uses actions pinned to mutable version tags instead of immutable 40-character commit SHAs. In release.yml: `actions/checkout@v6` and `actions/setup-node@v6`. These tag-based refs can be silently moved to point to different (potentially malicious) commits without any change to the workflow file.

Locations:

- `.github/workflows/release.yml:22`
- `.github/workflows/release.yml:27`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all mutable tag-based action references to immutable commit SHAs:
- `actions/checkout@v6` → `actions/checkout@d23441a48e516b6c34aea4fa41551a30e30af803 # v6` (3 occurrences in integration.yml, 1 in release.yml)
- `actions/setup-node@v6` → `actions/setup-node@249970729cb0ef3589644e2896645e5dc5ba9c38 # v6` (1 occurrence in integration.yml, 1 in release.yml)
Original tag names preserved as inline comments for readability.

