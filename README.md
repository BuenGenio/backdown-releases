# BackDown releases

Download builds of **BackDown**, backup that thinks: find out what's on your drives, what's duplicated, and which drives are safe to wipe, with a SHA-256 hash behind every claim.

**Website: [backdown.io](https://backdown.io)**

This repository holds release files only. BackDown's source code is private while the product is in early development.

## Command-line preview

Download the archive for your platform from the [latest release](https://github.com/BuenGenio/backdown-releases/releases), unpack it and run `backdown --help`.

| Platform | Archive |
|---|---|
| Linux x86-64 (static) | `backdown-<version>-linux-x86_64.tar.gz` |
| Linux ARM64 (static) | `backdown-<version>-linux-arm64.tar.gz` |
| macOS, Apple silicon and Intel | `backdown-<version>-macos-universal.tar.gz` |
| Windows x86-64 | `backdown-<version>-windows-x86_64.zip` |

Check a download against the release's `SHA256SUMS.txt`:

```sh
sha256sum -c SHA256SUMS.txt --ignore-missing        # Linux
shasum -a 256 -c SHA256SUMS.txt --ignore-missing    # macOS
```

## Quick start

```sh
backdown index /media/old-drive /media/archive   # record every file (read-only)
backdown check /media/old-drive                  # is it safe to wipe? exit 0 = yes, 2 = copy first
backdown check /media/old-drive --list           # every file that exists nowhere else
backdown dupes --min-size 10M                    # duplicated content, biggest savings first
```

BackDown only reads your drives. The one file it writes is its index database (`backdown.db` in the current folder, or `--db FILE`).

## Preview notes

- Builds aren't signed yet. On macOS, run `xattr -d com.apple.quarantine backdown` once after unpacking (or allow it under System Settings › Privacy & Security). On Windows, SmartScreen may ask you to confirm ("More info" › "Run anyway").
- Hardlinks are recognised on Linux and macOS; on Windows every path counts as its own file for now.
- Preview builds are provided as-is, without warranty, for evaluation. Check the results before you wipe anything.

Found a problem? Leave your email at [backdown.io](https://backdown.io) or open an issue here.
