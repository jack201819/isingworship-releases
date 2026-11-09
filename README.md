# Lamplight — Releases

Installers for the Lamplight desktop app for Windows. This repository holds
binaries only; the source lives elsewhere and is private.

**Already running Lamplight? You do not need this page.** The app checks for
updates itself, shows you what changed, and installs when you say so. That path
downloads over its own connection, so none of the warnings below appear.

## Downloading by hand

Grab the newest installer from the [Releases](../../releases/latest) page:
`Lamplight-Setup-<version>.exe`.

(`update-windows.json` is the manifest the app reads to update itself. There is
no reason to download it by hand.)

### You will see two warnings. Both are expected.

The app is **not code-signed**, so Windows and your browser have no publisher
identity to recognise. Neither warning means anything was detected in the file —
they mean "we do not know who made this".

**1. In the browser, while downloading**

> *Lamplight-Setup-….exe isn't commonly downloaded. Make sure you
> trust Lamplight-Setup-….exe before you open it.*

Every release is a brand-new file that almost nobody has downloaded yet, so it
has no reputation. Click the **chevron (⌄) next to Delete**, then **Keep** —
browsers deliberately put "Keep" behind that dropdown so it cannot be clicked
by accident. In Chrome, use **See more → Keep anyway**.

**2. When you run the installer**

> *Windows protected your PC — Windows Defender SmartScreen prevented an
> unrecognised app from starting.*

Click **More info**, then **Run anyway**.

Neither warning goes away over time. Reputation is tracked per file, so each new
release starts from nothing again. Only a code-signing certificate removes them.

## Verifying a download yourself

Every release records the SHA-512 of its installer in `update-windows.json`. The
app checks this automatically and refuses to install a file that does not match.
To check by hand, in PowerShell:

```powershell
# The hash of the file you downloaded
$h = Get-FileHash -Algorithm SHA512 "Lamplight-Setup-2026.9.0.exe"
[Convert]::ToBase64String(($h.Hash -split '(..)' -ne '' | ForEach-Object { [Convert]::ToByte($_, 16) }))

# The hash the release claims
(Invoke-RestMethod "https://github.com/jack201819/isingworship-releases/releases/latest/download/update-windows.json").releases[0].sha512
```

The two should be identical. If they are not, do not run the file.

<!-- Maintained in the source repository at docs/releases-repo/README.md. Edits made here are overwritten on the next release. -->
