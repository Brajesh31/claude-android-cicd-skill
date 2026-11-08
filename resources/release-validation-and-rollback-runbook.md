# Android Release Validation and Rollback Runbook

## Before build

- [ ] Confirm the release branch or tag.
- [ ] Confirm the version name and unique version code.
- [ ] Confirm environment, API endpoints, feature flags, and application ID.
- [ ] Review dependency and build-tool changes.
- [ ] Confirm release notes and known issues.
- [ ] Confirm required approvals.

## Build and artifact checks

- [ ] Build from a clean CI environment.
- [ ] Run required unit tests, lint, and integration tests.
- [ ] Verify package name, version, minimum SDK, and target SDK.
- [ ] Verify artifact signature and signing certificate.
- [ ] Install the artifact on representative test devices or emulators.
- [ ] Smoke-test startup, authentication, navigation, and critical flows.
- [ ] Save artifact checksum and associated commit/build identifiers.

## Staged publishing

1. Publish to an internal testing channel.
2. Verify installation and core journeys with a controlled tester group.
3. Review crashes, startup failures, ANRs, and critical backend errors.
4. Promote to the next testing or rollout stage only when release criteria pass.
5. Increase rollout exposure in planned steps.
6. Record approval, time, artifact version, and observed health at each stage.

## Rollout stop conditions

Stop promotion and investigate when any of the following occurs:

- A critical user journey fails.
- Crash or ANR rates materially exceed the agreed baseline.
- Authentication, payments, or data integrity is affected.
- A release introduces a severe privacy or security issue.
- The artifact or version metadata does not match the approved release.

## Recovery procedure

- Pause or halt the staged rollout using the distribution platform's supported controls.
- Identify the affected version and rollout percentage.
- Preserve logs, crash reports, artifact identifiers, and the triggering commit.
- Decide whether a server-side mitigation, feature-flag disablement, or new app release is required.
- Prepare and test the corrective build.
- Re-run the complete validation sequence.
- Communicate the impact, mitigation, and next update to stakeholders.

Mobile application rollbacks have platform and version constraints. A previously published binary may not be directly redeployable as a downgrade for every user. Validate the distribution platform's supported recovery path and prefer a corrected forward release where necessary.

## Post-release review

- [ ] Confirm rollout completed as planned.
- [ ] Review production health signals.
- [ ] Confirm support and incident channels have no unresolved release issue.
- [ ] Archive the artifact, checksums, logs, and approval record.
- [ ] Capture lessons and update the pipeline or checklist.
