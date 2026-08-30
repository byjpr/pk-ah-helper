PK AH Helper
=====

![License](https://img.shields.io/badge/License-GPLv3-blue.svg)

Pokémon Fire Red and Leaf Green helper to distribute Aurora and Mystic Tickets and setting event flags, programmed in Python.

For each ticket it:
  * adds the key item to the Key Items pocket (quantity 1, correctly
    XOR-encrypted with the save's encryption key)
  * sets the "received via Mystery Gift" event flag
  * sets the ferry-destination flag so the Vermilion sailor lists the island
  * sets the world-map flag so the island shows on the Town Map

## Usage

> [!WARNING]
> **Back up your save first.** Even though `--in-place` writes a `.bak`
> automatically, keep your own copy of the original save somewhere else
> before running the tool on any file. Save corruption can't always be
> undone, and a backup sitting next to the file being modified is not a
> real backup.

```
Usage:
  python3 frlg_tickets.py SAVE.sav                 # both tickets -> SAVE.patched.sav
  python3 frlg_tickets.py SAVE.sav --aurora        # Aurora Ticket only
  python3 frlg_tickets.py SAVE.sav --mystic        # Mystic Ticket only
  python3 frlg_tickets.py SAVE.sav -o out.sav      # choose output path
  python3 frlg_tickets.py SAVE.sav --in-place      # overwrite (writes .bak first)
  python3 frlg_tickets.py SAVE.sav --info          # inspect, change nothing
```

## Using RetroArch `.srm` saves

RetroArch battery saves (`.srm`) for GBA cores are the same raw flash format
as `.sav`, so the tool works on them directly — the extension doesn't matter:

```
python3 frlg_tickets.py "Pokemon - Fire Red Version.srm"
```

The output will be named `Pokemon - Fire Red Version.patched.sav`. RetroArch
only loads a save whose name matches the ROM exactly, so rename it back
before launching the game:

```
mv "Pokemon - Fire Red Version.patched.sav" "Pokemon - Fire Red Version.srm"
```

Alternatively, patch with `--in-place` and no renaming is needed (a `.bak`
backup of the original is written first).

**Note:** make sure RetroArch is fully closed before patching, or the core
will overwrite your patched file with its in-memory copy. Savestates
(`.state` files) are not supported — save in-game at a Pokémon Center first.
