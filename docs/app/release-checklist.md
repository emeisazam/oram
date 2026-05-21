# ORAM macOS Release Checklist

- Run `uv run pytest`.
- Run `swift build` in `apps/macos`.
- Build `ORAM.app` with `apps/macos/script/build_and_run.sh --no-open`.
- Build unsigned DMG with `apps/macos/script/package_unsigned.sh`.
- Confirm `releases/macos/ORAM.dmg` and `releases/macos/checksums.txt` were refreshed.
- Confirm `.env` and local secrets are absent from artifacts.
- Confirm `oram --mock-audio` still works.
- Confirm `oram daemon --mock-audio` starts and `/health` returns `ok`.
- Confirm app runs with mock backend before any API key is configured.
- Confirm ElevenLabs and Stability AI key setup stores keys in Keychain.
- Confirm generated WAV files appear in `~/Music/ORAM Library/Sounds`.
- Update release notes from `docs/app/release-notes-template.md`.
- Sign and notarize public builds.
