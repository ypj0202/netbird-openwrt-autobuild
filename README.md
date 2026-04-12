# netbird-openwrt-autobuild

This repository contains an OpenWrt package definition and GitHub Actions workflow to automatically build NetBird packages for OpenWrt.

## Original source

- Upstream NetBird project: https://github.com/netbirdio/netbird
- NetBird official website: https://netbird.io

## What this repository does

- Tracks the latest NetBird release version
- Updates `netbird/Makefile` version and hash
- Builds OpenWrt package artifacts using the OpenWrt SDK
- Publishes built `.apk` artifacts via GitHub Actions releases
