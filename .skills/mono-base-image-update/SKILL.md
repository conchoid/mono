---
name: mono-base-image-update
description: Updates Dockerfiles in the mono repository for a new Debian base image release by switching the debian:<suite>-slim base image, preserving required apt packages, revalidating the Mono repository and GPG keyring setup, and verifying Mono runtime compatibility. Use when asked to move mono images from bookworm to trixie or another Debian suite.
---

# mono-base-image-update

Use this skill when updating `mono` Dockerfiles to a new Debian release.

## Workflow

1. Identify the source Dockerfile and target directory.
   Example: `6.12.0-bookworm/Dockerfile` -> `6.12.0-trixie/Dockerfile`.
2. If the target directory does not exist, create it and copy the previous Dockerfile into it.
3. Update the base image from `debian:<old-suite>-slim` to `debian:<new-suite>-slim`.
4. Keep the installed `apt-get` packages unless a compatibility issue is confirmed. Do not silently remove required libraries.
5. Re-check the external Mono package repository configuration.
   - verify the configured repository path is still valid
   - verify the configured distribution mapping still works on the new Debian suite
   - verify the GPG key retrieval and keyring setup still work
6. Build the image locally.
   ```bash
   cd <target-dir>
   docker build -t conchoid/mono:<target-tag> .
   ```
7. Validate compatibility:
   - confirm all `apt-get` packages still resolve
   - confirm Mono installs correctly
   - confirm the GPG keyring setup succeeds
   - confirm the configured Mono repository remains usable
   - confirm locale settings still work
8. If the repository has project-level or sample builds, run them with the new image and verify build success, runtime behavior, and dependency resolution.

## Notes

- External repository configuration is the fragile part of this update. Re-check it every time you change the Debian suite.
- If the existing Mono repository still points to an older Debian distribution such as `stable-buster`, do not assume it remains compatible with the new suite; verify it explicitly.
- Read [references/debian-release-update.md](references/debian-release-update.md) for the repo-specific checklist and original example.
