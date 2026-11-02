---
sidebar_position: 6
---

# Finding game code with crashlink

You know *what* the game does (it writes saves, it loads PAKs, it checks something) but not *where* in 60,000+ functions it does it. This tutorial walks the standard hunt: pick a string you know exists, find who references it, and decompile the suspects until one of them is your function.

It assumes you've read [Using crashlink to manipulate game code](/ModDocCE/tutorials/crashlink) and have crashlink installed.

## Prerequisites

- A computer

- An Internet connection (first run only, for reference)

- crashlink installed ([setup here](/ModDocCE/tutorials/crashlink#installing))

- Your game's bytecode: on Windows pass crashlink your `deadcells.exe`, everywhere else pass `hlboot.dat` (see [loading the game](/ModDocCE/tutorials/crashlink#loading-the-game))

## Step 1: pick a string that must exist

Every hunt starts with text the game cannot avoid containing. Good candidates are names from file formats documented on this very site: chunk flags like `S_User`, magic values, error messages, file extensions. Bad candidates are guesses about internal names — start from something you've *seen*, not something you hope exists.

As a running example we'll use `S_User`, the save chunk flag documented on the [Save Files](/ModDocCE/files/save) page. That page's format notes were obtained exactly this way — someone searched for save-related strings and followed the references.

## Step 2: search the string table

Load the game in crashlink (this takes a minute or so), then:

```
crashlink> ss S_User
```

`ss` searches the string constant pool for a substring. You'll get back one or more string indexes. Note them down — indexes, like everything else here, are specific to your exact game version.

:::warning Indexes are per-version

Function indexes (`f@…`), string indexes, type indexes — all of these shift between game versions. A write-up that says "the save function is f@34927" means "on the version I looked at". Never hardcode an index into a tool or a tutorial; always re-derive it with the steps on this page.

:::

## Step 3: find who references the string

For a promising string index:

```
crashlink> sref <idx>
```

(`sref`, alias `strref`.) This lists every function that references the string directly, or via a global initialized to it. Save-writing code, UI labels that display the string, and half a dozen unrelated coincidences may all show up — that's normal. You're panning, not sniping.

## Step 4: disassemble the suspects

```
crashlink> fn <findex>
```

Read the disassembly of each candidate. You're looking for context clues: calls to compression helpers near save strings, file-write natives near path strings, chunk-size arithmetic near format strings. Most candidates eliminate themselves in seconds — wrong neighborhood, wrong callees.

For the survivors, get pseudocode instead of raw ops:

```
crashlink> dec <findex>
```

If you installed crashlink with `[extras]`, the output is syntax-highlighted. One level up from raw disassembly is usually where a function finally becomes readable.

## Step 5: confirm with callers and debug info

Two independent checks, either of which can confirm or kill a suspect:

- **Callers:** `xref <findex>` lists every function that calls your suspect. A save-writing function should be called from save-flow code, not from the title screen.
- **Debug info:** `debugfiles` lists source files recorded in the bytecode; `infile <file.hx>` lists functions from one of them. If your suspect originates from a file whose name matches the feature (save logic living in a save-ish file), that's strong corroboration.

When disassembly, callers, and file origin all agree, you've found your function. Write down *how* you found it (string → reference → confirmation), not just its index — the next game update will renumber everything and only the method transfers.

## Where to go next

- [Decompile the whole class](/ModDocCE/tutorials/crashlink#decompilation-and-control-flow) (`class`) once you've found one of its methods.
- [Patch and save](/ModDocCE/tutorials/crashlink#modifying-bytecode) if your goal is modifying behavior rather than just reading it.
- Generate [API docs](/ModDocCE/tutorials/crashlink#utility-commands) (`apidocs`, `mkdocs`) when you've mapped enough of an area to want it written down.
