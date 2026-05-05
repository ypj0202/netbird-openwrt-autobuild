# netbird-openwrt-autobuild

Automated build of [NetBird](https://netbird.io) for OpenWrt **25.12 and later**.

Based on [tbc0309/openwrt-netbird](https://github.com/tbc0309/openwrt-netbird).

## Overview

This repository uses GitHub Actions to automatically track new NetBird releases and build `.apk` packages using the official OpenWrt SDK. Built packages are published as GitHub Releases.

NetBird is an open-source VPN management platform built on top of WireGuard®, making it easy to create secure private networks for your organization or home — with zero configuration effort and no need to open ports or manage complex firewall rules.

## Supported Architectures

| Architecture | Target |
|---|---|
| `mipsel_24kc` | ramips/mt7621 |

## Requirements

- OpenWrt 25.12 or later
- `kmod-wireguard` kernel module

## Installation

Download the latest `.apk` package for your architecture from the [Releases](../../releases/latest) page and install it on your device:

```sh
opkg install netbird_*.apk
```

Or install directly from the release URL:

```sh
opkg install https://github.com/ypj0202/netbird-openwrt-autobuild/releases/latest/download/netbird_<version>_<arch>.apk
```

## Usage

Enable and start the NetBird service:

```sh
/etc/init.d/netbird enable
/etc/init.d/netbird start
```

Connect to a NetBird management server (use the default hosted server or your own self-hosted instance):

```sh
netbird up --management-url https://api.netbird.io
```

Check connection status:

```sh
netbird status
```

## How It Works

- A weekly scheduled workflow (every Sunday at midnight UTC) checks for new NetBird releases on [netbirdio/netbird](https://github.com/netbirdio/netbird).
- If a new release is found, the `Makefile` is updated with the new version and source hash and committed automatically.
- The build workflow then compiles the package using the OpenWrt 25.12 SDK and uploads the resulting `.apk` files as a GitHub Release tagged with the NetBird version.
- The workflow can also be triggered manually via **workflow_dispatch**.

## Configuration

The NetBird service is managed by procd and stores its state at:

| Path | Purpose |
|---|---|
| `/etc/netbird/config.json` | NetBird configuration (preserved on upgrade) |
| `/root/.config/netbird` | Runtime state directory |
| `/var/lib/netbird/state.json` | DNS state file |

## Credits

- Original OpenWrt package: [tbc0309/openwrt-netbird](https://github.com/tbc0309/openwrt-netbird)
- NetBird: [netbirdio/netbird](https://github.com/netbirdio/netbird)
- Go toolchain for OpenWrt: [sbwml/packages_lang_golang](https://github.com/sbwml/packages_lang_golang)

## License

The NetBird package is licensed under the [BSD-3-Clause License](https://github.com/netbirdio/netbird/blob/main/LICENSE).
