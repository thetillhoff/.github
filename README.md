# Release Golang executable on tag

This workflow automatically builds your Golang executable cross-platform as soon as you push a git tag that fits the semantic versioning schema with `v` prefix (f.e. `v1.2.3`).

Some advanced features are included as well:
- Automatically retrieve the Go version from `go.mod`
- Check the `CHANGELOG.md` if the new version is listed there. If not, the pushed tag is automatically deleted and the build fails.
