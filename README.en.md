<div align="center">

<img src="https://raw.githubusercontent.com/mainuan/.github/main/profile/assets/mainuan-logo.svg" width="96" alt="Mainuan logo">

# Mainuan Icon Themes

Six colour variants of the Kora icon theme for **Mainuan Linux**, packaged as `mainuan-icon-themes`.

[![CI](https://github.com/mainuan/icons/actions/workflows/ci.yml/badge.svg)](https://github.com/mainuan/icons/actions/workflows/ci.yml)
[![Release](https://img.shields.io/github/v/release/mainuan/icons)](https://github.com/mainuan/icons/releases)

[Português](README.md)

</div>

---

## What it is

One Kora icon theme per Mainuan accent colour: `kora-brown`, `kora-cyan`,
`kora-grey`, `kora-lima`, `kora-magenta` and `kora-violet`. The
`mainuan-icon-themes` package installs them into `/usr/share/icons`, where
Plasma lists them under **System Settings > Colors & Themes > Icons**. Missing
icons are inherited from Breeze and hicolor. The package ships with the Mainuan
ISO; the default theme (`kora-cyan`) is set by
[`mainuan-desktop-defaults`](https://github.com/mainuan/dot-files).

The themes are stored as `kora-*.tar.gz` and unpacked at build time by
`debian/unpack-icon-themes`, which rejects members outside the theme folder,
drops the prebuilt cache, maintenance scripts and stray hidden files, and
rewrites absolute symlinks. The icon cache is generated on installation
(`dh_icons`). No file of another package is replaced.

## Installation

Download the `.deb` and `SHA256SUMS` from the
[latest release](https://github.com/mainuan/icons/releases/latest):

```bash
sha256sum --check --ignore-missing SHA256SUMS
sudo apt install ./mainuan-icon-themes_*_all.deb
```

## Build and tests

```bash
dpkg-buildpackage -us -uc -b
```

The [CI](.github/workflows/ci.yml) builds the package in Ubuntu 26.04, runs
`lintian`, installs it in a clean container, checks each theme's cache,
reference icons and `index.theme`, rejects broken or absolute symlinks, then
reinstalls, removes and purges it. A `v<version>` tag publishes the `.deb` and
`SHA256SUMS`.

## Credits and license

Kora icon theme by [bikass](https://github.com/bikass/kora); Mainuan colour
variants by Daigo ([daigoasuka](https://github.com/daigoasuka)); Debian
packaging and CI by Rafael Ruscher ([ruscher](https://github.com/ruscher)).

The Kora icon themes by [bikass](https://github.com/bikass/kora) and
Mainuan's colour variations are distributed under the **GNU GPL version 3**
(see [`LICENSE`](LICENSE)); being derived from GPL-3 work, they cannot be
relicensed. Mainuan's own work here (packaging in `debian/` and the
documentation) is distributed under the **GNU GPL version 2** (GPL-2.0), as
recorded in [`debian/copyright`](debian/copyright).
