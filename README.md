# Android Cicd

## Overview

This repository provides a Claude skill for android cicd. It organizes practical guidance into a repeatable workflow for implementing and maintaining the related process.

## What It Covers

- Core concepts and terminology.
- Recommended workflows and implementation considerations.
- Practical guidance for planning, execution, and validation.
- Original supporting files included with the skill.

## Repository Structure

```text
SKILL.md
```

## Prerequisites

- A Claude-compatible environment with skill support.
- Relevant project source code and configuration.
- Required development tools and platform access for the tasks being performed.

## Getting Started

1. Read `SKILL.md` and review the workflow.
2. Install the skill in your Claude environment's supported skills directory.
3. Provide the relevant project context, constraints, and desired outcome.
4. Apply the instructions to the task.
5. Test the resulting changes in a suitable development environment before release.

## Best Practices

Keep secrets out of source control, use least-privilege access, and validate changes through automated checks. Confirm platform-specific behavior against current official documentation.

## License

MIT. See [LICENSE](LICENSE).

## Supporting template

Added `templates/gradle/signing.gradle` as a secure signing configuration reference. It uses CI environment variables or Gradle properties and intentionally does not include keystore files or hard-coded credentials. Enable release signing only after configuring protected CI secrets.
