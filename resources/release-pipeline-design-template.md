# Android Release Pipeline Design Template

## Project context

- Application:
- Project type: Native Android / Flutter / React Native / Trusted Web Activity
- Repository:
- Default branch:
- Build system and version:
- Android Gradle Plugin version:
- JDK version:
- CI provider:
- Package/application ID:
- Release owner:

## Pipeline objective

- Required build variants:
- Target release channels:
- Supported Android SDK range:
- Required test suites:
- Artifact formats:
- Publishing destination:
- Approval requirements:

## Pipeline stages

| Stage | Required actions | Gate to continue | Output |
|---|---|---|---|
| Checkout | Resolve commit and source ref | Expected branch/tag | Source revision |
| Environment | Set up JDK, SDK, build tools | Toolchain check passes | Build environment |
| Dependencies | Resolve and cache dependencies | Dependency resolution succeeds | Dependency state |
| Quality | Run lint, unit tests, static checks | Required checks pass | Test reports |
| Build | Build selected variants | Build completes | APK/AAB |
| Sign | Sign using protected credentials | Signature verifies | Signed artifact |
| Verify | Inspect package ID, version, signing identity | Metadata matches release plan | Validated artifact |
| Publish | Upload to chosen testing or production channel | Approval and release conditions pass | Published release |
| Monitor | Review crash, startup, and rollout signals | Health criteria remain acceptable | Rollout decision |

## Release configuration

- Version name:
- Version code:
- Build variant:
- Distribution track:
- Artifact retention period:
- Signing identity:
- Required reviewers:
- Release notes location:

## Failure handling

For each stage, define whether failure blocks all later stages, what logs and artifacts are retained, who receives the alert, and how the pipeline can be safely rerun without publishing duplicate or unintended releases.

## Acceptance criteria

- [ ] Build is reproducible from a clean CI runner.
- [ ] Required tests and static checks pass.
- [ ] Version code is unique.
- [ ] Signing credentials are not stored in source control.
- [ ] Signed artifact metadata is verified.
- [ ] Publishing is gated by branch/tag and approval rules.
- [ ] The published artifact can be traced to a commit.
- [ ] Rollback or staged rollout halt procedure is documented.
