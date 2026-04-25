# fledge-plugin-doctor — DEPRECATED

> **This plugin has been re-absorbed into core `fledge doctor`.** The toolchain probes now live in core as an informational `Toolchains` section. The repo is archived.

## What changed

In fledge **v0.15.2+**, `fledge doctor` ships the toolchain probes (rustc/cargo/node/npm/pnpm/bun/yarn/python3/uv/poetry/go/ruby/swift/java/gradle/mvn) as a fourth section called `Toolchains`. The section is **informational** — missing tools render dimmed (`· tool (not installed)`) and don't pollute the pass/fail totals (a Python project shouldn't fail because Swift is absent).

```
$ fledge doctor

  fledge
    ✅ fledge config 0.15.2 — loaded

  Git
    ✅ git 2.50.1
    ...

  AI
    ...

  Toolchains
    ✅ rustc 1.93.0
    ✅ cargo 1.93.0
    ✅ node 25.5.0
    · pnpm (not installed)
    ✅ bun 1.3.12
    ...
```

If you previously installed this plugin via `fledge plugins install --defaults`, you can remove it:

```sh
fledge plugins remove fledge-plugin-doctor
```

## Why archive?

This plugin was 110 lines of shell parallel to core `fledge doctor`. It registered as the sibling command `doctor-tools` with a description claiming to "extend `fledge doctor`" — but it didn't extend anything; it was a separate command. Re-absorbing back into core gives you one diagnostic surface with one section per concern.

See [`CorvidLabs/fledge`](https://github.com/CorvidLabs/fledge) — `fledge doctor --help`.

## License

MIT
