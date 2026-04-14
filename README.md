# ez-cdc CLI — public release artifacts

This repository hosts public release artifacts (binaries + checksums) for
the `ez-cdc` CLI, the companion tool for the
[dbmazz](https://github.com/ez-cdc/dbmazz) PostgreSQL CDC daemon.

## Install

```bash
curl -sSL https://raw.githubusercontent.com/ez-cdc/dbmazz/main/install.sh | sh
```

The installer downloads the right binary for your OS and architecture
from the latest release in this repository, verifies the SHA256 checksum,
and installs it to `$HOME/.local/bin/ez-cdc`.

Supported platforms: `linux/amd64`, `linux/arm64`, `darwin/amd64`, `darwin/arm64`.

## Releases

See the [Releases](https://github.com/ez-cdc/ez-cdc-cli-releases/releases)
tab for all published versions and changelogs.

## License

The `ez-cdc` CLI is released under the Elastic License v2.0.
