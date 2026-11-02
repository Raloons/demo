---
sidebar_position: 7
---

# Working with PAK stamps

Since v35, the game's main `res.pak` carries a *stamp*: a signature tying the archive to the exact game version that built it. Repack a PAK without the right stamp and the game skips it during loading — which looks exactly like your modifications "not working". This tutorial shows how to read a stamp, figure out which version it belongs to, and repack with it.

It assumes you've read [Unpacking and modifying game assets](/ModDocCE/tutorials/pak_tutorial/) and [the PAK format page](/ModDocCE/files/pak). If stamps are new to you, read [the stamps section](/ModDocCE/files/pak#stamps) first — the short version is: SHA-256 of a fixed salt plus the game's short git hash, stored as 64 ASCII hex characters.

## Prerequisites

- A computer (running Windows for this guide)

- An Internet connection

- [PAKTool Extended](https://github.com/N3rdL0rd/alivecells/releases/latest) (the official `PAKTool.exe` from the game's ModTools cannot handle v1 stamped PAKs)

- Your game's `res.pak` (usually `C:\Program Files (x86)\Steam\steamapps\common\Dead Cells\res.pak`)

## Reading a stamp

The easiest way is the [stamptool site](https://n3rdl0rd.github.io/alivecells/stamptool/): drag and drop your `res.pak`, click **Calculate**, and out comes the stamp. For reference, stamps look like this (example only — yours will differ per version):

```
00222281297b0973a12d345484b34c1debcd3a38734f1e0dd1f3b3f7acdd91c
```

:::note v0 PAKs have no stamp

Only v1 PAKs (game v35+) carry stamps. Official *mod* PAKs are v0 and stamp-free. If stamptool finds nothing, your PAK predates the scheme and you can repack without one.

:::

## Figuring out which version a stamp belongs to

Because the stamp is a deterministic hash of the short git commit, it runs *backwards* cheaply: brute-forcing short hashes until one reproduces the stamp tells you exactly which commit built the game. `alivecells` ships this as the `commitbrute` subcommand (see the [PAK format page](/ModDocCE/files/pak#stamps)). This is occasionally useful when a PAK's origin is unclear — match the stamp, and you've dated the file.

## Repacking with a stamp

Same repack flow as the [PAK tutorial](/ModDocCE/tutorials/pak_tutorial#repacking-with-a-stamp), restated here so the stamp step isn't skipped:

```
PAKTool.exe collapsev1 "<unpacked dir>" "<game dir>\res.pak" -s <YOUR STAMP HERE>
```

Replace `<YOUR STAMP HERE>` with the stamp you extracted above.

:::danger This overwrites your res.pak

Just like in the PAK tutorial: back the original up first, or be ready to verify the game's integrity from Steam to revert. A repack with the *wrong* stamp loads as if your changes don't exist — no error, just silence — so if a repacked PAK seems to do nothing, the stamp is the first thing to re-check.

:::

## That's all, folks!

Verify in-game that your changes load, and keep the stamp written down next to the game version it came from. Future you, mid-update, will be grateful.
