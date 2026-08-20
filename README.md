# pipeshift-test-lab

A deliberate test fixture for [PipeShift](https://pipeshiftai.com). Everything
here exists to be migrated, scanned, broken and verified by automated tests.

**Nothing in this repository is real.** There is no deployment target, no cloud
account and no secret. Jobs that look like they deploy are wired to fail
immediately if they are ever executed — that is intentional, and it is the
second line of defence behind PipeShift's own job classifier.

## What is here, and what it is for

### Source pipelines — migration (MIGRATE-001)

| Path | Platform | Expected |
|---|---|---|
| `Jenkinsfile` | Jenkins | detected, migrated |
| `.gitlab-ci.yml` | GitLab CI | detected, migrated |
| `.circleci/config.yml` | CircleCI | detected, migrated |
| `azure-pipelines.yml` | Azure DevOps | detected, migrated |
| `services/api/Jenkinsfile` | Jenkins | detected — monorepo naming |

### Decoys — must NOT be migrated

| Path | Why |
|---|---|
| `examples/Jenkinsfile` | example directory — low confidence, reported not migrated |
| `vendor/legacy/Jenkinsfile` | vendored — never a user's own source |
| `docs/Jenkinsfile.md` | documentation about a pipeline, not a pipeline |

### Existing workflows — collision and verification

| Path | Purpose |
|---|---|
| `.github/workflows/existing-ci.yml` | migration must NOT overwrite it |
| `.github/workflows/verify-safe-pass.yml` | verification: passes first time |
| `.github/workflows/verify-safe-fail.yml` | verification: fails on purpose, then is fixable |
| `.github/workflows/verify-unsafe-deploy.yml` | classifier must refuse every job |
| `.github/workflows/verify-never-starts.yml` | no push trigger — "could not verify", not failure |

## Keeping `main` green

The deliberately failing workflow ignores `main`, so a red badge here means
something unexpected broke rather than something working as designed.
