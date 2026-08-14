# P5 Search Jumper

A macOS app that lets you search your offline media archive and restore exactly
what you need.

P5 Search Jumper sits between two existing tools:

- **[Jumper](https://docs.getjumper.io/api-reference/introduction)** — a local
  media analysis app that builds a small, searchable index of the **visual
  content** and **spoken words** in your footage. It runs entirely on your Mac;
  nothing is uploaded.
- **[Archiware P5](https://blog.archiware.com/redoc/p5_rest_api/awp5api.html)** —
  the LTO tape archive system that stores your original source media and restores
  it by exact file handle.

## What it does

1. **Search.** Run a semantic visual search ("a boat on a lake") or a transcript
   search ("what she said about the budget") over a Jumper analysis cache.
2. **Find.** Results point to the exact source file and shot.
3. **Restore.** When that source file is offline (already archived to tape), P5
   Search Jumper resolves it to the exact archived handle and restores just that
   file from P5 to an isolated folder you choose — never overwriting the original
   path.

The point is efficiency: search a tiny online analysis index of thousands of hours
of footage, then pull back only the specific clip you need from the archive.

## How it works

The app talks to both products through their local REST APIs:

- **Jumper** — semantic visual and transcript search over the analysis cache
  (`/search/text`, `/search/transcript`), plus cache inventory and metadata
  inspection.
- **Archiware P5** — resolves a search result to its exact ArchiveEntry handle and
  restores it via `POST /rest/v1/restore/restoreselections`.

It also includes:

- **Menu bar search** — a quick-search popover you can use from anywhere.
- **Metadata filters** — narrow visual or transcript results by media kind,
  resolution, codec, camera, duration, and more.
- **Clip preview** — click a result (or press space) to play the source file
  from the exact matched frame; still images open in a viewer.
- **Result control** — choose how many top matches each file shows, and
  collapse duplicate/copy files to their best container.
- **Inventory** — check a folder against the Jumper cache and see which files are
  already analyzed or archived.
- **History** — an audit trail of every restore.
- **API log** — captures each request for troubleshooting, with credentials
  redacted.

Your Jumper license key and P5 credentials live in the macOS Keychain and are only
read when needed — never on launch, and never logged.

## Requirements

- macOS 13 or newer
- Jumper (running locally) with a Pro license
- Archiware P5 with the REST API available

## Releases

Ready-to-run builds are distributed as disk images (`.dmg`) on the
[Releases](https://github.com/macvfx/P5-Search-Jumper/releases) page.

## Disclaimer

P5 Search Jumper is an independent utility and is not affiliated with, endorsed
by, or sponsored by Jumper or Archiware. Jumper and Archiware P5 are trademarks of
their respective owners.