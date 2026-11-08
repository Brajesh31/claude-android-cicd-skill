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
