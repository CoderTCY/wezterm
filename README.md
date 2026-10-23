# Wez's Terminal

<img height="128" alt="WezTerm Icon" src="https://raw.githubusercontent.com/wezterm/wezterm/main/assets/icon/wezterm-icon.svg" align="left"> *A GPU-accelerated cross-platform terminal emulator and multiplexer written by <a href="https://github.com/wez">@wez</a> and implemented in <a href="https://www.rust-lang.org/">Rust</a>*

User facing docs and guide at: https://wezterm.org/

![Screenshot](docs/screenshots/two.png)

*Screenshot of wezterm on macOS, running vim*

## Installation

https://wezterm.org/installation

### Patched Windows IME nightly (this fork)

Unofficial, unsigned Windows x64 packages are available from the
[IME nightly release](https://github.com/CoderTCY/wezterm/releases/tag/ime-nightly).
Use the complete portable ZIP or installer; the GUI also needs its bundled
`OpenConsole.exe`, `conpty.dll`, graphics libraries and other runtime files.

The [fork-only workflow](.github/workflows/wezterm-ime-nightly.yml) checks
upstream `main` daily at 03:17 UTC and skips already published source/workflow
combinations. Manual dispatch always rebuilds. It applies the pinned IME patch
only in the runner, runs the Windows IME regression tests, uses upstream
packaging, checks the portable runtime, then publishes packages with SHA-256
checksums and `build-info.txt` identifying upstream, patch and workflow revisions.
Patch conflicts or failed checks stop publication.

The original development history is preserved on `fix/8229-windows-ime-caret`;
`patches/windows-ime-caret` holds the standalone, single-commit patch.
To update the patch, prepare a new standalone commit based on upstream and
update `PATCH_COMMIT` in the workflow. Keep `main` at upstream plus one
fork-automation commit; upstream workflow files are not modified.

## Getting help

This is a spare time project, so please bear with me.  There are a couple of channels for support:

* You can use the [GitHub issue tracker](https://github.com/wezterm/wezterm/issues) to see if someone else has a similar issue, or to file a new one.
* Start or join a thread in our [GitHub Discussions](https://github.com/wezterm/wezterm/discussions); if you have general
  questions or want to chat with other wezterm users, you're welcome here!
* There is a [Matrix room via Element.io](https://matrix.to/#/#wezterm:matrix.org)
  for (potentially!) real time discussions.

The GitHub Discussions and Element/Gitter rooms are better suited for questions
than bug reports, but don't be afraid to use whichever you are most comfortable
using and we'll work it out.

## Supporting the Project

If you use and like WezTerm, please consider sponsoring it: your support helps
to cover the fees required to maintain the project and to validate the time
spent working on it!

[Read more about sponsoring](https://wezterm.org/sponsor.html).

* [![Sponsor WezTerm](https://img.shields.io/github/sponsors/wez?label=Sponsor%20WezTerm&logo=github&style=for-the-badge)](https://github.com/sponsors/wez)
* [Patreon](https://patreon.com/WezFurlong)
* [Ko-Fi](https://ko-fi.com/wezfurlong)
* [Liberapay](https://liberapay.com/wez)
