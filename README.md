# iSingWorship — Releases

Installers for the iSingWorship desktop app. This repository holds binaries
only; the source lives elsewhere and is private.

**Already running iSingWorship? You do not need this page.** The app checks for
updates itself, shows you what changed, and installs when you say so. That path
downloads over its own connection, so none of the warnings below appear.

## Downloading by hand

Grab the newest installer from the [Releases](../../releases/latest) page:
`iSingWorship-Setup-<version>.exe`.

(`update.json` is the manifest the app reads. There is no reason to download it
by hand.)

### You will see two warnings. Both are expected.

The app is **not code-signed**, so Windows and your browser have no publisher
identity to recognise. Neither warning means anything was detected in the file —
they mean "we do not know who made this".

**1. In the browser, while downloading**

> *iSingWorship-Setup-….exe isn't commonly downloaded. Make sure you trust
> iSingWorship-Setup-….exe before you open it.*

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

Every release records the SHA-512 of its installer in `update.json`. The app
checks this automatically and refuses to install a file that does not match. To
check by hand, in PowerShell:

```powershell
# The hash of the file you downloaded
$h = Get-FileHash -Algorithm SHA512 "iSingWorship-Setup-2026.1.1.exe"
[Convert]::ToBase64String(($h.Hash -split '(..)' -ne '' | ForEach-Object { [Convert]::ToByte($_, 16) }))

# The hash the release claims
(Invoke-RestMethod "https://github.com/jack201819/isingworship-releases/releases/latest/download/update.json").releases[0].sha512
```

The two should be identical. If they are not, do not run the file.

## Which build can update itself

Only the **Setup** installer. The portable build cannot overwrite itself while
running, so it reports that it cannot update rather than pretending to — a
portable copy has to be replaced by hand.
