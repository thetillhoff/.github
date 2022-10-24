# Release-on-tag actions

These workflows are made to be triggered each time a semantic version tag is pushed.

They'll then verify you didn't forget to add the version in the changelog and either build and push automatically builds your Golang executable cross-platform as soon as you push a git tag that fits the semantic versioning schema with `v` prefix (f.e. `v1.2.3`).

## Example usage

```yaml
name: Release Golang executable on tag

on:
  push:
    tags:
    - "v[0-9]+.[0-9]+.[0-9]+"

jobs:
  prerequisites:
    uses: thetillhoff/.github/.github/workflows/release-on-tag-prerequisites.yaml@main
  release-on-tag:
    uses: thetillhoff/.github/.github/workflows/release-on-tag-golang-executable.yaml@main
    #uses: thetillhoff/.github/.github/workflows/release-on-tag-docker-build.yaml@main
```

## Action `changelog-prerequisite`
This workflow checks if the `./CHANGELOG.md` contains an entry for the specified tag.

If it doesn't exist, the pushed tag is automatically deleted and the build fails.

## Action `tagged-docker-build-and-push`
This workflow builds a docker image according to `./Dockerfile`, tags it with the pushed tag (and `latest`) and pushes the image to `ghcr.io`.

## Action `tagged-golang-build`
This workflow automatically builds your Golang executable cross-platform as soon as you push a git tag that fits the semantic versioning schema with `v` prefix (f.e. `v1.2.3`).

Some advanced features are included as well:
- Cross-platform builds out of the box; Linux, Mac and Windows executables included in every release
- Automatically retrieves the Go version from `./go.mod`

