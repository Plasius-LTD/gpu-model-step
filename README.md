# @plasius/gpu-model-step

STEP analytic geometry import/export and controlled tessellation contracts.

This repository is the dedicated package boundary defined by ADR 0094.

## Bootstrap status

This initial repository contains the approved schema baseline, legal and governance files, and a package smoke-test surface. Functional model conversion work is tracked in the repository's [TASK] issues and must flow through the canonical GPU model boundary.

## Rollout

- Feature flag: gpu.model.conversion.enabled
- Capability: none for this package-only layer
- Rollback: disable the feature flag and keep the published package version pinned to the last validated release

## Development

Requires Node.js 24 and npm.

```bash
npm ci
npm run typecheck
npm test
npm run lint
npm run build
npm pack --dry-run
```

## License

Apache-2.0. See LICENSE, SECURITY.md, and the files under legal/.

<!-- BEGIN PLASIUS RELEASE INTEGRITY -->
## Release integrity

CI keeps the administrative contributor registry outside Git and npm package
artifacts using exact, case-normalised path checks. CI runs on explicit
GitHub-hosted runners. Publication uses the GitHub-hosted `production` job with
Node 24 and a pinned npm 11.6.2 client. It is token-free and proceeds only while
the prepared SHA is the exact `main` head after successful push-triggered CI.
The completed `0.1.0` bootstrap path has been removed; subsequent releases must
use npm trusted publishing.
<!-- END PLASIUS RELEASE INTEGRITY -->

## Automatic npm releases

Run `.github/workflows/cd.yml` on `main` with `phase=prepare` and the intended
version bump. The schema-template pipeline prepares release metadata through a
pull request, waits for CI on that exact main commit, then publishes the sealed
package through npm trusted publishing in the `production` environment.
Normal privacy, audit, tests, coverage and artifact checks run automatically.
No separate release-owner or dependency-coordination admission is required.

`npm run privacy:check` checks repository path metadata. `npm run test:privacy`
tests the policy and release contract. `npm run pack:check` checks the package
against the reviewed inventory in `scripts/package-artifacts.json`; update that
inventory deliberately when public package files change. Add real notes under
`Unreleased`; only the release pipeline promotes them to a versioned section.
