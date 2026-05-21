# ORAM macOS App Plan

ORAM remains a local-first instrument: recorder, looper, summoner, listener,
archive. The macOS app is a native control shell around the existing Python
engine, not a replacement for it.

## Current Surfaces

- CLI: `oram` and `oram run` start the terminal instrument with keyboard,
  push-to-talk, realtime or mock audio, command parsing, routing, generation,
  listening, and archive export.
- Dashboard: `oram dashboard` starts a localhost FastAPI dashboard for manual
  testing. It binds to `127.0.0.1` by default and requires
  `ORAM_DASHBOARD_TOKEN` before LAN exposure.
- Engine: `oram.app` wires `OramSession`, `LayerManager`, audio engine,
  `AgentController`, `ActionRouter`, provider gateways, and the engine registry.
- Session archive: `oram.archive.session` writes `mix.wav`, stems,
  `session.json`, `commands.log`, `listening_report.md`, and `waveform.txt`.
- Providers: mock generation is the safe default. ElevenLabs and other engines
  are registered only when credentials are configured.

## Target Architecture

```text
SwiftUI ORAM.app
  -> launches or discovers local ORAM daemon
  -> sends authenticated localhost HTTP commands
  -> daemon routes commands through existing parser/action system
  -> Python ORAM engine owns audio state
  -> credentials are read from macOS Keychain through CredentialStore
  -> generated sounds are written to ORAM Library
```

## Repository Boundary

```text
src/oram/             existing Python engine and CLI behavior
src/oram_daemon/      local helper daemon and HTTP control API
src/oram_security/    credential store, redaction, privacy utilities
src/oram_library/     generated sound library and SQLite index
apps/macos/           native SwiftUI app shell
docs/security/        key handling, threat model, privacy guarantees
docs/app/             app architecture and release notes
```

## App Sections

1. Welcome and onboarding
2. Provider setup
3. Engine status
4. Recorder and looper
5. Prompt-to-sound generation
6. Listening and analysis
7. Local library
8. Settings
9. Security and privacy

## Extracted Service Modules

- `oram_daemon`: owns process metadata, random port selection, daemon API,
  local auth, and daemon lifecycle.
- `oram_security`: owns credential lookup, Keychain storage, `.env` developer
  fallback, memory store for tests, and redaction.
- `oram_library`: owns `~/Music/ORAM Library`, generated sound metadata,
  SQLite indexing, tags, favorites, reveal/export helpers.

## Non-goals For The First Shell

- No Momoto account.
- No remote ORAM server.
- No telemetry by default.
- No API key visible in app state, daemon state, archive files, crash output, or
  logs.
- No replacement of the existing terminal app.

## Licensing

The Python package is MIT licensed in `pyproject.toml`. The macOS app shell and
new helper modules stay MIT unless a future bundled dependency requires a
separate license boundary in release packaging.
