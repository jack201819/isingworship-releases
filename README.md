# iSingWorship — Releases

Installers for the iSingWorship desktop app. This repository holds binaries
only; the source lives elsewhere and is private.

The app checks `releases/latest/download/update.json` for new versions and
verifies every download against the SHA-512 recorded there.

**Installers are unsigned**, so Windows SmartScreen will warn about an unknown
publisher on first install. Choose *More info* → *Run anyway*.

## Downloads

Grab the newest installer from the [Releases](../../releases/latest) page.

- `iSingWorship-Setup-<version>.exe` — the normal installer. Only this build
  can update itself.
- `update.json` — the update manifest the app reads. Not something to download
  by hand.
