# Xbox One/Series X/Series S

Unfortunately, I'm unable to find a source that allows me to legally obtain the files for Dead Cells on Xbox. If anyone owns an Xbox with Dead Cells installed, please send me a DM on Discord `@n3rdl0rd` - let's figure this out!

Notably, the Xbox holds a lot of promise as an x64-based system that very very closely mimics Windows' systems, so if any console has a full bytecode image embedded on it, this would be the one.

## Why the Xbox is the interesting one

Every other non-PC port of Dead Cells we know about dodges the HashLink VM: mobile, Switch, and PS4 builds are all HL/C-transpiled native code (see [Mobile](/ModDocCE/category/mobile) and the console pages), precisely because the HL VM only runs on x86/x64. The Xbox One and Series consoles *are* x64 machines running an OS very close to Windows.

So, unlike every other console port, there is no technical reason the Xbox build *couldn't* ship the same full `hlboot.dat` bytecode image as the PC build — no transpiler needed, no debug info lost, no native-only binary to squint at. If that's how it shipped, then in principle everything that works on PC bytecode (disassembly, decompilation, patching, and maybe even framework-style mod loading) would transfer over almost directly.

:::warning Pure speculation

Nobody has confirmed any of this yet — no file listing, no executable, no save dump from an Xbox has been examined for this project. The reasoning above is "this *could* be true given the architecture", not "this *is* true". If you can check, please do — confirming or killing this hypothesis is the single most useful Xbox contribution possible.

:::

## What we'd need

By analogy with the [PS4](/ModDocCE/console/ps4) and [Switch](/ModDocCE/console/nx/) pages, the useful unknowns are, roughly in order:

1. **A file listing.** What does the installed game actually contain? Is there an `hlboot.dat`-shaped file, a `res.pak`, a native executable, or something else entirely?
2. **The executable format.** If it's a standard Windows-style binary running under the Xbox OS layer, existing PC tooling might just work on it.
3. **The save location.** Where saves live and whether they're encrypted/signed like the PS4's, or loose like the Switch's under CFW.

You don't need to answer all three — even one confirmed file listing would move this page from "hope" to "plan".

## How to help

If you own an Xbox with Dead Cells installed and can poke at its files (dev-mode consoles, legitimate backups, emulator save paths — whatever is legal in your situation), send a DM on Discord to `@n3rdl0rd` with whatever you've got. Partial information is welcome; "here's the folder layout but I can't read the files" is still progress.
