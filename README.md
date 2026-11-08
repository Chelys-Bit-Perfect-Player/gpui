# GPUI for Chelys

A fork of [Zed](https://github.com/zed-industries/zed) for [Chelys](https://github.com/Chelys-Bit-Perfect-Player)'s
desktop app, which is built on GPUI. The `chelys` branch is Zed at
[`b5cd310b`](https://github.com/zed-industries/zed/commit/b5cd310b3b54dfc659fcc06453e6358843dfe216) plus the changes below;
nothing else differs from Zed.

- **Idle windows let their spare Metal drawables go (macOS 14 and later).** GPUI already pauses a window's
  `CAMetalDisplayLink` when nothing is drawn, but its `CAMetalLayer` keeps up to four drawables (14.4 MB each at
  1180×780 @2x). After 10 s paused, the layer's drawable size is set to 1×1, which makes it drop its pool; the
  drawable on screen stays. The size comes back before the next frame, and a resize in between wins. In
  `footprint`, an idle window went from 76 to 60–64 MB, and one paused after continuous rendering from 97 to
  54 MB. Rendering is unchanged. Files: `crates/gpui_apple/src/display_link.rs`,
  `crates/gpui_macos/src/display_link.rs`, `crates/gpui_macos/src/window.rs`.

Use it like Zed's GPUI, from this repository at a commit on `chelys`:

```toml
gpui = { git = "https://github.com/Chelys-Bit-Perfect-Player/gpui", rev = "<commit>" }
```

The changed crates stay under Zed's licence (Apache-2.0, `LICENSE-APACHE`).

---

# Zed

[![Zed](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/zed-industries/zed/main/assets/badge/v0.json)](https://zed.dev)
[![CI](https://github.com/zed-industries/zed/actions/workflows/run_tests.yml/badge.svg)](https://github.com/zed-industries/zed/actions/workflows/run_tests.yml)

Welcome to Zed, a high-performance, multiplayer code editor from the creators of [Atom](https://github.com/atom/atom) and [Tree-sitter](https://github.com/tree-sitter/tree-sitter).

---

### Installation

On macOS, Linux, and Windows you can [download Zed directly](https://zed.dev/download) or install Zed via your local package manager ([macOS](https://zed.dev/docs/installation#macos)/[Linux](https://zed.dev/docs/linux#installing-via-a-package-manager)/[Windows](https://zed.dev/docs/windows#package-managers)).

Other platforms are not yet available:

- Web ([tracking discussion](https://github.com/zed-industries/zed/discussions/26195))

### Developing Zed

- [Building Zed for macOS](./docs/src/development/macos.md)
- [Building Zed for Linux](./docs/src/development/linux.md)
- [Building Zed for Windows](./docs/src/development/windows.md)

### Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for ways you can contribute to Zed.

Also... we're hiring! Check out our [jobs](https://zed.dev/jobs) page for open roles.

### Licensing

Zed source code is licensed primarily under GPL-3.0-or-later, with Apache-2.0 components where marked.

License information for third party dependencies must be correctly provided for CI to pass.

We use [`cargo-about`](https://github.com/EmbarkStudios/cargo-about) to automatically comply with open source licenses. If CI is failing, check the following:

- Is it showing a `no license specified` error for a crate you've created? If so, add `publish = false` under `[package]` in your crate's Cargo.toml.
- Is the error `failed to satisfy license requirements` for a dependency? If so, first determine what license the project has and whether this system is sufficient to comply with this license's requirements. If you're unsure, ask a lawyer. Once you've verified that this system is acceptable add the license's SPDX identifier to the `accepted` array in `script/licenses/zed-licenses.toml`.
- Is `cargo-about` unable to find the license for a dependency? If so, add a clarification field at the end of `script/licenses/zed-licenses.toml`, as specified in the [cargo-about book](https://embarkstudios.github.io/cargo-about/cli/generate/config.html#crate-configuration).

## Sponsorship

Zed is developed by **Zed Industries, Inc.**, a for-profit company.

If you’d like to financially support the project, you can do so via GitHub Sponsors.
Sponsorships go directly to Zed Industries and are used as general company revenue.
There are no perks or entitlements associated with sponsorship.
