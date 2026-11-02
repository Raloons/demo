---
sidebar_position: 5
---

# Using DCCM

DCCM (Dead Cells Core Modding) is the way most people actually mod Dead Cells on PC: instead of unpacking and repacking the game's own files (see [Unpacking and modifying game assets](/ModDocCE/tutorials/pak_tutorial/)), you write a small mod and the framework loads it alongside the vanilla game. Mods install and uninstall cleanly, and the base game stays untouched.

See the official documentation [here](https://dead-cells-core-modding.github.io/docs/docs/) — what follows is the short version to get you oriented.

## Prerequisites

- A computer (running Windows for this guide)

- An Internet connection

- A Steam or GOG copy of Dead Cells (these tutorials reference game version **v35**)

- Some level of comfort with a terminal (eg. ability to run a command with arguments)

## Installing DCCM

The exact steps live in the [official documentation](https://dead-cells-core-modding.github.io/docs/docs/) and depend on your storefront:

- **Steam users** can install DCCM via the Workshop.
- **GOG users** install it manually.

:::note Version matching matters

DCCM releases support specific game versions. If the game updates under you, check the DCCM release notes for the pairing you need before assuming anything is broken.

:::

## Verifying the install

Once installed, don't launch the game from the Steam Play button — DCCM only loads under its modded launcher, `DeadCellsModding.exe`, sitting next to the vanilla game files. Launch that, and confirm:

1. The game reaches the title screen normally (framework alone, zero mods — this is your clean baseline).
2. A `coremod` folder exists in the game install, containing `mods` (where built mods go) and `logs` (where you'll look first whenever anything misbehaves).

If all three check out, the framework works on your machine and any future problem belongs to a specific mod, not your install.

## Back up your saves first

Do this before installing any mod, not after something breaks. Dead Cells saves live under your Steam userdata folder (`userdata/<your Steam ID3>/588650/remote/` when Cloud sync is on) — copy the whole Dead Cells save folder somewhere safe and verify the copy matches. Title-screen mods barely touch saves, but gameplay mods absolutely can, and swapping between modded and vanilla launches on the same run without a backup is how progress gets damaged.

## Where to go next

- The [official DCCM documentation](https://dead-cells-core-modding.github.io/docs/docs/) for framework API, tutorials, and the modding workflow.
- [DCCM-Modding-Handbook](https://github.com/Raloons/DCCM-Modding-Guides) ([live site](https://raloons.github.io/DCCM-Modding-Guides/)), a community-written handbook covering setup, custom equipment, effects, gameplay mods, biomes, and debugging — with complete worked examples.
