# 7ኪሎ — OTA host

Public host for the **7ኪሎ** Android app's over-the-air updates. It holds:

- **`manifest.json`** — the version pointer the live app polls on every launch.
- **Releases** — the compiled web-bundle `.zip`s the app downloads and swaps in.

This is the **compiled web build only** (the same bundle that ships inside every APK and is already
extractable from it) — **not** the source code, which stays private in `TikusApp/7kilo` (the game) and
`TikusApp/7kiloAndroid` (the Android shell).

Published automatically by **`7kiloAndroid/ota-release.mjs`**. Don't edit by hand. See the
[7kiloAndroid README](https://github.com/TikusApp/7kiloAndroid) for the full OTA architecture.
