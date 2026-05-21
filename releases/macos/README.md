# ORAM macOS DMG

This folder is the repository-visible macOS app build.

- `ORAM.dmg`: unsigned development DMG.
- `checksums.txt`: SHA-256 checksum for the DMG in this folder.

Because this DMG is unsigned and not notarized, macOS Gatekeeper may require
right-click > Open the first time it is launched. Public distribution should use
Developer ID signing and Apple notarization.

This development DMG includes the ORAM Python source and a bundled `uv` launcher.
On first run, `uv` creates the local daemon environment under
`~/Library/Application Support/ORAM`. A future signed release should preflight or
vendor runtime dependencies for fully offline first launch.
