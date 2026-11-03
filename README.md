# WezTerm Windows IME nightly

This fork publishes unofficial, unsigned Windows x64 builds of
[WezTerm](https://github.com/wezterm/wezterm) with a pinned Windows IME caret patch.
Download the complete portable ZIP or installer from the
[IME nightly release](https://github.com/CoderTCY/wezterm/releases/tag/ime-nightly).
The GUI requires the bundled `OpenConsole.exe`, `conpty.dll`, graphics libraries,
and other runtime files; do not copy only `wezterm-gui.exe`.

## Branch layout

- [`automation`](https://github.com/CoderTCY/wezterm/tree/automation) is this fork's
  **default branch**. It contains only this README and the fork-only workflow,
  with independent history and no inherited upstream workflows or source tree.
  GitHub schedules workflows from the default branch.
- [`main`](https://github.com/CoderTCY/wezterm/tree/main) tracks
  [`wezterm/wezterm:main`](https://github.com/wezterm/wezterm/tree/main) without
  fork-specific commits. Clone or check out `main` for the source tree.
- [`patches/windows-ime-caret`](https://github.com/CoderTCY/wezterm/tree/patches/windows-ime-caret)
  preserves the standalone patch pinned by `PATCH_COMMIT` in the workflow.
- [`fix/8229-windows-ime-caret`](https://github.com/CoderTCY/wezterm/tree/fix/8229-windows-ime-caret)
  preserves the original development history.

Sync upstream changes into **`main` only**, for example:

```sh
gh repo sync CoderTCY/wezterm --branch main
```

Do not sync upstream into `automation`, change the default branch to `main`, or
put fork-only build configuration on `main`. The build does not depend on the
fork's `main` being up to date: it resolves upstream directly.

## Build and publication

The [workflow](.github/workflows/wezterm-ime-nightly.yml) checks upstream `main`
daily at 03:17 UTC. Workflow changes pushed to `automation` also trigger it.
The source-selection job only runs for this repository's default branch;
manual dispatch must select `automation` and always rebuilds.
Scheduled and push runs skip source/workflow combinations already published.

Each build resolves an immutable upstream commit, checks out that revision from
`wezterm/wezterm`, and applies the pinned patch only in the runner. It runs the
Windows IME regression tests, uses upstream packaging, verifies the portable
runtime, and smoke-runs the packaged binaries before publishing the installer
and portable ZIP. Patch conflicts or failed checks stop publication.

The rolling release includes SHA-256 checksums and `build-info.txt` identifying
the upstream, patch, build tree, workflow revision, and Actions run. The release
tag points to the patch commit; it does not point to this automation branch.

To build manually:

```sh
gh workflow run wezterm-ime-nightly.yml --repo CoderTCY/wezterm --ref automation
```

## Updating the patch

Prepare a new standalone patch commit based on upstream and preserve it on
`patches/windows-ime-caret`. Update `PATCH_COMMIT` in the workflow on `automation`
to the full commit SHA. Pushing that workflow change starts a build; the source
branches are never rewritten by the workflow.

## Upstream

User documentation and installation guidance: <https://wezterm.org/>.
Report upstream issues to [WezTerm](https://github.com/wezterm/wezterm/issues);
these patched, unsigned packages are maintained by this fork, not upstream.
