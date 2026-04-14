# ez-cdc CLI — release artifacts

Public binaries for the **`ez-cdc`** command-line tool — the operator and
verification CLI for the [dbmazz](https://github.com/ez-cdc/dbmazz)
PostgreSQL Change Data Capture daemon.

This repository contains only release artifacts (binaries + checksums).
For dbmazz documentation, source code, and issues, see
[ez-cdc/dbmazz](https://github.com/ez-cdc/dbmazz).

---

## Install

The recommended way is the one-liner installer hosted in the dbmazz repo:

```bash
curl -sSL https://raw.githubusercontent.com/ez-cdc/dbmazz/main/install.sh | sh
```

The installer auto-detects your OS and architecture, downloads the matching
binary from the latest release in this repository, verifies the SHA256
checksum against `SHA256SUMS`, and installs it to `$HOME/.local/bin/ez-cdc`
(falls back to `/usr/local/bin` with `sudo` if needed).

You can pin a specific version with the `EZ_CDC_VERSION` environment
variable, or change the install directory with `EZ_CDC_INSTALL_DIR`:

```bash
EZ_CDC_VERSION=v0.1.0 \
EZ_CDC_INSTALL_DIR=/opt/bin \
  curl -sSL https://raw.githubusercontent.com/ez-cdc/dbmazz/main/install.sh | sh
```

### Manual install

If you prefer to download the binary yourself, grab it from the
[latest release](https://github.com/ez-cdc/ez-cdc-cli-releases/releases/latest)
or use the direct URL pattern:

```bash
VERSION=v0.1.0
OS=linux       # or darwin
ARCH=amd64     # or arm64

curl -fsSL -o ez-cdc \
  "https://github.com/ez-cdc/ez-cdc-cli-releases/releases/download/${VERSION}/ez-cdc-${OS}-${ARCH}"
chmod +x ez-cdc
sudo mv ez-cdc /usr/local/bin/
```

### Verify the checksum

```bash
curl -fsSL -O \
  "https://github.com/ez-cdc/ez-cdc-cli-releases/releases/download/${VERSION}/SHA256SUMS"

# Linux
sha256sum --check --ignore-missing SHA256SUMS

# macOS
shasum -a 256 --check --ignore-missing SHA256SUMS
```

---

## Supported platforms

| OS | amd64 (x86_64) | arm64 (aarch64) |
|---|:---:|:---:|
| **Linux** | ✅ | ✅ |
| **macOS** (10.12+) | ✅ | ✅ |

Linux binaries are statically linked against musl libc, so they run on any
distribution (Debian, Ubuntu, Alpine, RHEL, Fedora, Arch, etc.) without
needing glibc compatibility.

---

## Quickstart

After installing, point the CLI at a PostgreSQL source and a sink:

```bash
ez-cdc datasource init                                    # write a starter config
ez-cdc datasource add                                     # interactive wizard for source + sink
ez-cdc quickstart --source my-pg --sink my-warehouse      # spin up dbmazz + live dashboard
```

Press `t` in the dashboard to generate live traffic, `q` to exit.

The CLI also ships with a 13-check end-to-end verification harness that
validates every supported sink (schema, snapshot integrity, CDC
operations, type fidelity, idempotency drift):

```bash
ez-cdc verify --source my-pg --sink my-warehouse           # full suite
ez-cdc verify --source my-pg --sink my-warehouse --quick   # skip slow checks
```

---

## Versioning

This repository follows [Semantic Versioning](https://semver.org/).
Release tags: `vMAJOR.MINOR.PATCH`. Each release publishes 4 binaries
(`ez-cdc-linux-amd64`, `ez-cdc-linux-arm64`, `ez-cdc-darwin-amd64`,
`ez-cdc-darwin-arm64`) plus a `SHA256SUMS` file.

Release notes are auto-generated from conventional commits (feat / fix /
refactor / perf / docs / chore / security) on every push that warrants a
version bump.

---

## Issues, questions, source code

This is a release-only repository. For everything else, go to
[ez-cdc/dbmazz](https://github.com/ez-cdc/dbmazz):

- 📚 Documentation
- 🐛 Bug reports and feature requests
- 💬 Discussions
- 🤝 Contributing

---

## About

`ez-cdc` and `dbmazz` are built and maintained by **[EZ-CDC](https://ez-cdc.com)**.

For managed BYOC deployment with auto-healing workers, centralized
monitoring, RBAC, audit logs, and a web portal — running dbmazz in your
own AWS or GCP account — see **[EZ-CDC Cloud](https://ez-cdc.com)**.

---

## License

The `ez-cdc` CLI is licensed under the
[Elastic License v2.0](https://www.elastic.co/licensing/elastic-license).
