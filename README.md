# nu-lint releases

Prebuilt [nu-lint](https://codeberg.org/wvhulle/nu-lint) binaries for **macOS** (Apple Silicon and Intel) and **Windows** (x64).

Upstream publishes Linux binaries only. On macOS and Windows, `cargo install nu-lint` compiles most of Nushell itself and needs a full Rust toolchain. On Windows that means the Visual Studio Build Tools too. This repository builds once, so a machine only has to download one file.

## What is in a release

| File | Contents |
|---|---|
| `nu-lint-aarch64-apple-darwin.tar.gz` | macOS, Apple Silicon |
| `nu-lint-x86_64-apple-darwin.tar.gz` | macOS, Intel |
| `nu-lint-x86_64-pc-windows-msvc.tar.gz` | Windows x64 (`nu-lint.exe`) |
| `SHA256SUMS` | checksums of the three archives |
| `LICENSE` | upstream's MIT licence |

Each archive holds the binary at its root, the same layout as upstream's Linux releases.

## Where the binaries come from

**No code lives here.** [`.github/workflows/release.yml`](.github/workflows/release.yml) runs every Monday. If crates.io has a nu-lint version with no release here yet, it runs `cargo install nu-lint --version <v> --locked` for each target, on GitHub's own runners, smoke-tests the result with `--version`, and publishes it. The build log of every release is public, in the Actions tab.

To build a specific version by hand: *Actions → release → Run workflow*, and give the version.

## Install

```sh
v=1.5.0; t=aarch64-apple-darwin
curl -fsSLO "https://github.com/ChristianLemer/nu-lint-releases/releases/download/v$v/nu-lint-$t.tar.gz"
curl -fsSL  "https://github.com/ChristianLemer/nu-lint-releases/releases/download/v$v/SHA256SUMS" | grep "nu-lint-$t" | shasum -a 256 -c
tar -xzf "nu-lint-$t.tar.gz" -C ~/.local/bin
```

## Taking it over

Nothing here is specific to one person. To run your own copy, fork the repository and enable Actions on the fork. The first run builds the latest version. Point your installer at the fork's releases.

## Licence

nu-lint is © its authors, MIT-licensed. The licence is shipped in every release. This repository only adds the build workflow, under the same licence.
