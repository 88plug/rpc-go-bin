# rpc-go-bin

AUR package for [Intel's `rpc-go`](https://github.com/device-management-toolkit/rpc-go) — the Device Management Toolkit CLI for Intel AMT / vPro activation, configuration, and queries via `/dev/mei0` or network.

[![AUR](https://img.shields.io/aur/version/rpc-go-bin?label=AUR&style=flat-square)](https://aur.archlinux.org/packages/rpc-go-bin)
[![CI](https://img.shields.io/github/actions/workflow/status/88plug/rpc-go-bin/auto-update.yml?label=auto-update&style=flat-square)](https://github.com/88plug/rpc-go-bin/actions)
[![License](https://img.shields.io/badge/license-Apache--2.0-blue?style=flat-square)](https://github.com/device-management-toolkit/rpc-go/blob/main/LICENSE)

## Install

```bash
yay -S rpc-go-bin
```

Installs `/usr/bin/rpc`.

## What it does

`rpc` is Intel's reference CLI for managing Intel AMT / vPro firmware locally via `/dev/mei0` or remotely over the network. Used for:

- Activating AMT (`rpc activate -local -ccm`) — see [amt-activate-linux](https://github.com/88plug/amt-activate-linux) for the full guide
- Querying state (`rpc amtinfo`)
- Configuration (TLS, WiFi, 802.1x, CIRA)
- Deactivation (`rpc deactivate -local`)

This package ships the **pre-built x86_64 Linux binary** from Intel's official GitHub releases. The binary is statically linked Go — no system dependencies.

## Why a separate package?

`openwsman` / `wsmancli` are the traditional AUR options for AMT WS-Man — both are **broken** on current Arch (Ruby rdoc `ArgumentError` during build). `rpc-go-bin` is the working modern replacement and is small enough (~10MB) to stand alone.

## Automation

`auto-update.yml` runs daily at 06:00 UTC. When upstream rpc-go publishes a new release, this repo:
1. Bumps `pkgver` and recomputes `sha256sums_x86_64`
2. Commits to `main`
3. Pushes the new PKGBUILD to AUR

No manual tagging required. Upstream `vX.Y.Z` → AUR `X.Y.Z-1` within 24h.

## Manual update

```bash
git clone https://github.com/88plug/rpc-go-bin
cd rpc-go-bin
makepkg -si
```

## Source vs binary

This is a `-bin` package (pre-built binary). For source builds, you'd need the Go toolchain — there is no `rpc-go` source package on AUR currently. File an issue if you want one.

## Related

- [amt-activate-linux](https://github.com/88plug/amt-activate-linux) — Linux-only AMT activation guide + `intel-amt-activate` wrapper script
- [intel-amt-linux](https://github.com/88plug/intel-amt-linux) — Linux GUI + CLI to manage AMT after activation
- [device-management-toolkit/rpc-go](https://github.com/device-management-toolkit/rpc-go) — upstream
