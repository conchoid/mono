# Dockerfile base image update reference

Repository: `mono`

## Standard pattern

- Copy the previous Debian variant into a new target directory if needed
- Change the base image from `debian:bookworm-slim` to `debian:trixie-slim`
- Preserve required `apt-get` packages
- Revalidate the Mono repository and GPG key setup

## Example from the original procedure

- Source Dockerfile: `6.12.0-bookworm/Dockerfile`
- Target Dockerfile: `6.12.0-trixie/Dockerfile`
- Example image tag: `conchoid/mono:6.12.0-trixie`

```bash
cd mono/6.12.0-bookworm
docker build -t conchoid/mono:6.12.0-trixie .
```

## Checklist

- Update the base image to the new Debian suite.
- Preserve required `apt-get` libraries unless incompatibility is confirmed.
- Verify Mono `6.12.0` or the intended Mono line still installs correctly.
- Verify the GPG keyring setup still works.
- Verify the configured Mono repository remains compatible with the new Debian suite.
- Verify locale-related behavior.
- Verify a real Mono project can build and run.

## Cautions

- Debian release changes can affect package names and versions.
- Older Mono repository mappings such as `stable-buster` may be brittle on newer Debian suites.
- GPG key acquisition and keyring conventions can change across Debian releases and should be revalidated explicitly.
