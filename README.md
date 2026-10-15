# setup-miso

A GitHub Action that installs [miso](https://github.com/haskell-miso/cli) (the
command line tool for [miso](https://haskell-miso.org) apps: MicroHs,
MicroCabal, and miso) from a release, and builds and tests the project of
`miso.yml`.

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      - uses: haskell-miso/setup-miso@v1
        with:
          test: miso run tests     # a shell command, after miso build
```

| input | default | |
|---|---|---|
| `version` | `latest` | the release to install, such as `v0.1.0` |
| `working-directory` | `.` | the directory of `miso.yml` |
| `build` | `true` | run `miso build` (`false`: only install miso) |
| `lint` | `false` | run `miso lint` before the build |
| `test` | | a shell command run after the build |
| `emscripten` | `auto` | set up emscripten: `auto` (when `miso.yml` has a `browser` or `browser_js` target), `none`, or a version |
| `cache` | `true` | cache the installed packages and browser runtimes (keyed on `miso.yml` and `miso.lock`), and emscripten (in `.emsdk-cache` in the workspace, keyed on its version) |

It puts `miso` on the `PATH` for the later steps, and sets `MISO_HOME`; its
outputs are `version` and `miso-home`.  It runs on Linux and macOS (on
Windows, run `install.sh` in an MSYS2 shell).

