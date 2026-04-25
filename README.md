# fledge-plugin-doctor

Toolchain diagnostics for [fledge](https://github.com/CorvidLabs/fledge) — extends the lean v0.15+ `fledge doctor` with checks for installed language toolchains.

Pre-v0.15, `fledge doctor` baked checks for rustc/cargo/node/npm/pnpm/bun/python/swift/kotlin/etc. directly into core (~250 LOC of `if-elif` over ecosystems). v0.15 stripped all of that to keep core lean. This plugin restores the toolchain probes as an opt-in add-on.

## Install

```sh
fledge plugins install CorvidLabs/fledge-plugin-doctor
```

## Commands

### `fledge doctor-tools [--json]`

Probes installed toolchains and reports versions.

```
$ fledge doctor-tools

  rust
    ✅ rustc                1.84.0
    ✅ cargo                1.84.0
    ✅ cargo-clippy         1.84.0

  node
    ✅ node                 22.13.0
    ✅ npm                  10.9.2
    ❌ pnpm                 not found
    ✅ bun                  1.1.45
    ❌ yarn                 not found

  python
    ✅ python3              3.13.1
    ✅ uv                   0.5.16
    ❌ poetry               not found

  go
    ❌ go                   not found

  swift
    ✅ swift                6.0.3
  ...
```

`--json` emits an array of `{tool, group, status, version}` entries.

## Probed groups

`rust` (rustc, cargo, cargo-clippy), `node` (node, npm, pnpm, bun, yarn), `python` (python3, uv, poetry), `go`, `ruby`, `swift`, `java` (java, gradle, mvn).

## Why a plugin?

Probing every toolchain in the binary every fledge user installs is dead weight for almost everyone. A Rust-only shop carries the npm/pip/swift code for nothing. As a plugin, this is opt-in and trivially extendable — to add a new toolchain, add one entry to the `PROBES` array in `bin/fledge-doctor-tools`.

## License

MIT
