# FS25 Mod Checker

Find out which Farming Simulator 25 mods are broken **before** you sit through a loading screen to find out the hard way.

It's one file you open in your web browser. It reads your mods on your own PC: nothing is installed, nothing is uploaded, and your mods are never changed.

**Download:** get `FS25-Mod-Checker-v1.0.0.zip` from the [latest release](https://github.com/kingjawz9/FS25-Mod-Checker/releases/latest).

## How to use it

Prefer watching? **[`Tutorial.mp4`](Tutorial.mp4)** in this folder is a 90-second walkthrough (no sound, captions on screen). It uses made-up demo mods.

1. Unzip this download anywhere (your Desktop is fine).
2. Double-click **`FS25-Mod-Checker.html`**. It opens in Chrome, Edge or Firefox.
3. Click **Choose folder** and pick your **FarmingSimulator2025** folder. It's usually here:

   `Documents\My Games\FarmingSimulator2025`

   (If your Documents folder syncs to OneDrive, it's under `OneDrive\Documents\My Games\FarmingSimulator2025`.)

4. If your browser asks whether the page may view the folder, say yes. It only reads.

A few hundred mods take about 10 to 30 seconds. You get a list of every mod with one of four labels:

| Label | What it means |
|---|---|
| **Won't load** | The game will skip this mod completely. |
| **Partly broken** | It loads, but part of it fails (a missing shop item, a script that won't run). |
| **Warning** | Probably fine, but worth a look (a missing picture, the same mod twice). |
| **OK** | Nothing wrong found. Go make hay. |

Click any mod to see what's wrong in plain English and how to fix it.

Picking the whole FarmingSimulator2025 folder (not just `mods`) lets the checker also read your saves and the game's `log.txt`. You can also pick just the `mods` folder, or drag zips onto the page.

## What it checks

- **The zip opens** and `modDesc.xml` is at the top of it, not tucked inside a folder.
- **It's an FS25 mod.** FS22 and older mods (descVersion below 90) are refused by the game.
- **The name is allowed.** FS refuses names with spaces or brackets, names that start with a number, and Windows' `Mod (1).zip` copies.
- **Every file the mod points to is in the zip**: icon, shop items, scripts, translations, 3D models, textures and sounds. It also checks **capital letters**: inside a zip, `Scripts` and `scripts` are different folders to the game.
- **Paths left over from the author's PC**, like `C:/Users/someone/Desktop/textures/...`.
- **Dependencies.** Mods that need another mod you don't have, or that's not turned on in your save.
- **The same mod installed twice.**
- **Features listed twice** in a vehicle type (the game's "Specialization already exists" error).
- **FS22 script code that FS25 removed** (`g_configurationManager` and friends).
- **Ground pile (heap) types.** Every map has a limit (63, 127 or 255). Too many mods adding pile materials, and some can't be tipped on the ground. The checker counts them for the map in your save and names the mods that add the most.
- **Your log.txt.** Every error and warning the game wrote is matched back to the mod that caused it.
- **Mods your save uses** that are no longer in your mods folder.

## One-click fixes

Some problems can be fixed automatically: a `modDesc.xml` buried in a folder, wrong capital letters in a path, shop items or scripts that point at missing files, features listed twice, and textures pointing at the author's PC when the zip has its own copy.

For those mods, click **Download fixed copy**. Your original is never touched. Then:

1. Move the old zip out of your `mods` folder and keep it somewhere as a backup.
2. Move the downloaded zip (same name) from your Downloads folder into `mods`.
3. Run the checker again.

Please keep in mind:

- A fixed mod is for your own PC. In multiplayer, everyone needs the exact same file.
- An update from the mod's author replaces your fixed copy, which is usually what you want.
- Please don't re-upload other people's mods, fixed or not. Tell the author instead; they'll appreciate it.

## Checking for updates

Click **Check for updates**. For mods that link a GitHub page, the checker asks GitHub for the latest release and tells you if yours is older. That's the only time anything goes online, and all it sends is the GitHub project names.

For ModHub mods, use **Update All** in the game's own ModHub screen. Each mod in the report also has a **Find on ModHub** link so you can compare versions yourself. (ModHub doesn't let other pages ask it for versions automatically.)

## Copy report

**Copy report as text** gives you a short summary of the problems to paste into a forum post or Discord when asking for help. Folder paths are shortened so your Windows user name isn't included.

## Things it can't see

The checker reads files, it doesn't run the game. A few problems only show up once the game runs a mod's scripts: a mod the game itself has blacklisted as outdated, script crashes, a model that's too big. Those still show up in the report if you include `log.txt`, because the game writes them there. Run the game once, quit, then check again.

## Questions

**Is it safe?** It's a single web page that you can read in Notepad. It has no install and no `.exe`, and it only reads the files you pick. Your browser keeps it from touching anything else.

**My browser says "upload files to this site?"** Some browsers word their folder prompt that way. The page is running from your own PC, so the files go nowhere. Chrome and Edge usually ask "Let site view files?" instead.

**A mod shows "can't be opened" but works in the game.** Close the game and run the checker again. The game can lock files while it's running.

**Does it work on Mac or Linux?** Yes, in any up-to-date Chrome, Edge or Firefox.

## For modders and tinkerers

- Everything is in `FS25-Mod-Checker.html`: plain JavaScript, no libraries. The browser's own zip decompression and XML parser do the heavy lifting.
- Run the built-in self-test by opening the file with `#selftest` at the end of the address. The tab title changes to `SELFTEST PASS` or `SELFTEST FAIL`.
- The newest descVersion the checker knows about is `KNOWN_MAX_DESC` near the top of the script. Raise it when a game patch does.
- The base-game vehicle and placeable type lists (`BASE_TYPES`) come from the game's own `sdk/xmlDoku` folder.

## License

MIT. Free to use, change and share. See [LICENSE](LICENSE).

Not made by or affiliated with GIANTS Software. Farming Simulator is a trademark of GIANTS Software GmbH.
