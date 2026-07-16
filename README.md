# 7ኪሎ — OTA & streamed-asset host

Public host for the **7ኪሎ** Android app. Public because the app fetches from it over plain HTTP with no auth
(raw.githubusercontent + release-asset CDN both send permissive CORS, and GitHub serving is unmetered — kind
to low-data users). It holds:

- **`manifest.json`** — the version pointer the live app polls on every launch (see schema below).
- **`ota-vNN` releases** — the compiled web-bundle `.zip`s the app downloads and swaps in (OTA updates).
- **`music-v1` release** — the streamed radio tracks (`r01.mp3`…). To keep the app install small, only a few
  songs ship inside the APK; the rest download once on-device from here (see `7kilo/src/engine/remoteassets.ts`).

This is **compiled/output artifacts only** (the same web bundle already extractable from any APK) — **not**
source, which stays private in `TikusApp/7kilo` (game) and `TikusApp/7kiloAndroid` (Android shell).

### manifest.json schema
```jsonc
{
  "build": 21,                 // integer; the app applies an update only when build > its own baked OTA_BUILD
  "version": "1.12.2",         // human-readable
  "url": "https://github.com/TikusApp/7kilo-ota/releases/download/ota-v21/7kilo-bundle-21.zip",
  "mandatory": false,          // true = must apply before play (enforced at the boot gate)
  "checksum": "…",             // sha256 of the zip (@capgo verifies)
  "notes": "…"                 // shown in the in-app "update ready" toast
}
```

**Published automatically by `7kiloAndroid/ota-release.mjs` — don't edit by hand.** The `music-v1` release is
published once via `gh release create` (the game repo's `tools/music-split.mjs` prepares the slugged tracks).
See the [7kiloAndroid README](https://github.com/TikusApp/7kiloAndroid) for the full OTA architecture.
