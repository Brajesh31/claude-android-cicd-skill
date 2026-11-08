# claude-android-cicd-skill

A Claude Code skill for setting up and maintaining automated Android build and release pipelines.

## Overview

This skill helps configure repeatable Android CI/CD workflows for native Android, Flutter, React Native, and Trusted Web Activity projects. It focuses on automated builds, signing configuration, protected secrets, version management, and staged release promotion.

## Main Capabilities

- Identify the Android project type.
- Configure automated Gradle builds.
- Prepare Android signing for CI environments.
- Use protected CI secrets and environment variables.
- Automate version code updates where configured.
- Build release artifacts.
- Organize internal, alpha, beta, and production stages.
- Prepare Google Play publishing workflows.
- Validate workflow permissions and release conditions.

## Supported Project Types

- Native Android with Gradle.
- Flutter applications.
- React Native applications.
- Trusted Web Activity projects.

The exact workflow depends on the project's build system, signing setup, and publishing requirements.

## Installation

```bash
git clone https://github.com/Brajesh31/claude-android-cicd-skill.git ~/.claude/skills/android-cicd
```

Review the workflow and signing template before adding it to a production pipeline.

## Usage

Invoke the skill when creating or troubleshooting an Android release pipeline:

```text
/android-cicd
```

Provide the project type, Gradle and Android plugin versions, CI provider, release channel, and existing signing configuration.

## Signing Configuration

The repository includes a Gradle signing template:

```text
templates/gradle/signing.gradle
```

Use protected CI secrets or secure Gradle properties for signing credentials. Never commit keystores, passwords, or private signing material to the repository.

## Recommended Pipeline

1. Check out the source code.
2. Set up the required JDK, Android SDK, and build tools.
3. Restore dependencies.
4. Run lint and unit tests.
5. Build the required variant.
6. Sign the artifact using protected credentials.
7. Verify artifact metadata and versioning.
8. Publish to the selected testing track.
9. Promote through staged release channels after validation.

## Security Checklist

- Signing credentials are stored as protected secrets.
- Keystore files are not committed.
- CI permissions are limited to required operations.
- Release jobs run only under intended branch or tag conditions.
- Artifacts are retained and traceable.
- Version codes are unique and monotonic.
- Production publishing requires an explicit release condition.

## Repository Contents

- `SKILL.md`: Main Android CI/CD workflow.
- `templates/gradle/signing.gradle`: Signing configuration template.
- `README.md`: Pipeline overview, setup, and security checklist.

## Validation Checklist

- Build succeeds from a clean CI environment.
- Tests and lint checks run before publishing.
- Signing uses the correct protected credentials.
- Artifact package name and version are correct.
- Release channel is configured correctly.
- Failed builds cannot proceed to publishing.
- Rollback and release recovery are understood.

## Important Note

Google Play publishing and signing behavior depend on project configuration and account permissions. Test the pipeline with a non-production release before enabling automated production deployment.

## Release Engineering Resources

The following working documents complement the Gradle signing template already included in this repository.

| Resource | Purpose |
|---|---|
| [Release pipeline design template](resources/release-pipeline-design-template.md) | Map build, test, signing, verification, publishing, and monitoring stages. |
| [Signing and secret handling checklist](resources/signing-and-secret-handling-checklist.md) | Review keystore custody, CI secret exposure, access restrictions, and incident response. |
| [Release validation and rollback runbook](resources/release-validation-and-rollback-runbook.md) | Validate artifacts, promote releases in stages, define stop conditions, and coordinate recovery. |
| [Gradle signing template](templates/gradle/signing.gradle) | Starting point for wiring release signing through CI-provided credentials. |

## CI/CD Design Considerations

Keep build, test, signing, and publishing as clearly separated stages. Run lint and automated tests before exposing signing credentials. Restrict release secrets to trusted jobs on protected branches or approved tags. A pull request from an untrusted fork should never be able to read production signing material.

Treat the signed artifact as a release record. Preserve its checksum, source commit, build identifier, application ID, version name, version code, and signing certificate details. This makes it possible to identify exactly what was tested and published.

## Release Gating and Recovery

A successful build is not the same as a safe release. Verify the signed artifact, install it on representative devices, and exercise critical application journeys before publishing. Use staged tracks or controlled rollout where available. Define explicit stop conditions for crashes, ANRs, authentication failures, data loss, and other critical regressions.

Mobile releases cannot always be rolled back by simply reinstalling an earlier binary. Understand the distribution platform's supported recovery options, preserve the previous release details, and prepare a forward-fix process. Use server-side controls or feature flags only when they are designed and tested for that purpose.

## Release Handoff

Before promoting a release, the handoff should identify the commit, artifact, checksums, version details, test results, signing identity, release channel, approvals, known risks, and recovery owner. The process is incomplete until someone is accountable for monitoring the rollout after publication.
