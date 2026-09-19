# pcs-advanced-updates

Update manifest for **Paramount Console Suite Advanced** (`PmCA`,
`com.paramount.consolesuiteadvanced`).

This repo exists to serve exactly one file:

    https://raw.githubusercontent.com/soundslikehoot/pcs-advanced-updates/main/updates.json

The plug-in GETs it on editor open (at most once per 24 h, background thread, silent on
failure) and may draw a corner banner. It never downloads or installs anything.

## Why this is separate from `pcs-updates`

`updates.json` has a fixed two-channel shape (`beta` / `release`) describing ONE product.
Advanced ships on its own version line and its own schedule, so sharing the file would
make Simple's channels and Advanced's collide. The two products also use different update
cache filenames (`update-cache.json` vs `update-cache-advanced.json`) so they can never
read each other's cached manifest out of the shared product folder.

## Publishing

The manifest is RSA-signed with the same key as the licence files. Chain every new
manifest from whatever is LIVE rather than authoring from scratch — `--in` refuses input
that does not verify against the baked-in public key, and chaining carries untouched
channels forward so publishing a beta cannot blank the release channel.

See `Tools/RELEASING.md` in the plug-in repo for the full ritual.
