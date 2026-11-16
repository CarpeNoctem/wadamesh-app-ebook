# Ebook for Wadamesh

An .epub and .txt reader app (Lua) for [Wadamesh](https://github.com/ALLFATHER-BV/wadamesh) OS,
aimed mainly at the LilyGo T-Deck Pro and T-Deck Max, and working on the other
boards that run Lua apps with the extended SDK (`requires: sdk_ext`).

- Reads an .epub or a plain .txt file (UTF-8 or Latin-1; hard-wrapped lines are
  joined into paragraphs) a page at a time, with a chapter list, three text sizes, and your
  place remembered for the last ten books.
- Touch taps and swipes, trackball or D-pad, keyboard, and jog wheel / encoder.
- Pictures: with firmware that has `wada.ui.image`, a book's pictures can show on
  their own page or on a tap (Menu > Images). Without it the app shows an
  `<image: description>` line.

## Install

1. Copy `ebook.lua` and `ebook.json` to `/apps/` on the device (or
   `/meshcomod/apps/` on the SD card). Files from `deploy/apps/ebook/<version>/`
   are the released versions.
2. Prepare a book (below) and copy it to `/apps/ebook.d/` (internal flash) or
   `/meshcomod/apps/ebook.d/` (SD card).
3. Open **Ebook** from the apps list.

## Preparing books

The Lua SDK has no inflate, so the `.epub` must be stored uncompressed, and
`wada.fs` file names are at most 32 characters of `A-Z a-z 0-9 . _ -`.
`scripts/ebook-prep.py` repacks any `.epub` that way (the result is still a valid
`.epub`) and shortens its name:

    scripts/ebook-prep.py book.epub [more.epub ...] [-o OUTDIR] [--no-images]

## Testing

The app runs unmodified in the Wadamesh Lua harness:
`scripts/lua-harness/run.sh deploy/apps/ebook/2.0/ebook.lua` in the
[wadamesh](https://github.com/ALLFATHER-BV/wadamesh) repository.

## Layout

    ebook.lua, ebook.json          current version, ready to copy to a device
    deploy/apps/ebook/<version>/   each released version
    scripts/ebook-prep.py          repack an .epub for the app

## Status

Version 2.0 (current) adds: pictures shown on tap by default, a long title no longer
overlapping the author in the menu, `.txt` files, a first-run README that names the
books folder, and no separate "View image" menu row (tap the picture line, or press `i`).
Version 1.0 is kept under `deploy/apps/ebook/1.0/`.

Books stay in the app's own folder (`ebook.d`): the Lua SDK can list the SD card
(`wada.sd`) but only lets an app read files inside its own folder.

## License

**GPL-3.0-or-later**, the same as Wadamesh: see [LICENSE](LICENSE). Source files
carry an `SPDX-License-Identifier: GPL-3.0-or-later` header.
