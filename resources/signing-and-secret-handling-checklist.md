# Android Signing and Secret Handling Checklist

## Keystore custody

- [ ] Release keystore is stored outside the source repository.
- [ ] A protected secret store or CI secret mechanism holds required credentials.
- [ ] Access is limited to maintainers and release jobs that need it.
- [ ] A secure backup and recovery owner are defined.
- [ ] Keystore file integrity and expected signing certificate are verified.
- [ ] Rotation or key-upgrade requirements are understood before a change.

## CI configuration

- [ ] Credentials are exposed only to the signing job.
- [ ] Pull requests from untrusted forks cannot access release secrets.
- [ ] Secrets are not printed in logs, build scans, or failure messages.
- [ ] Avoid passing passwords through visible command-line arguments.
- [ ] Temporary keystore files are stored in restricted runner paths.
- [ ] Temporary secret files are removed after the job.
- [ ] Release jobs use least-privilege permissions.
- [ ] Secret availability is tested without revealing secret values.

## Gradle setup

- [ ] Signing configuration is applied only to intended release variants.
- [ ] Debug builds do not accidentally use production signing credentials.
- [ ] Missing credentials fail safely rather than creating an unsigned or incorrectly signed release.
- [ ] Environment variable names and Gradle property names are documented.
- [ ] No local developer password is hard-coded in a build file.

## Release verification

- [ ] Package/application ID is correct.
- [ ] The artifact is signed with the expected certificate.
- [ ] Version name and version code match the release plan.
- [ ] The artifact is retained with commit and build metadata.
- [ ] The release owner confirms the signing identity before publishing.

## Incident response

If signing material is exposed, stop releases, restrict access, identify affected artifacts and logs, notify the release owner, and follow the relevant app-signing and key-management recovery process. Do not assume deleting a secret from the latest commit removes it from history or previous build logs.
