# oram — roadmap

## current: MVP (python)

prove oram as an instrument. terminal looper with speech commands, constrained
DSP, one generated texture layer, session archiving, and listening reports.

### phases

- [x] phase 0: repo foundation
- [x] phase 1: basic terminal looper, no AI
- [x] phase 2: TUI and unicode performance interface
- [x] phase 3: keyboard transport and push-to-talk
- [x] phase 4: command grammar and agent controller
- [x] phase 5: DSP transformations
- [x] phase 6: generative bed
- [x] phase 7: session archive and listening report
- [ ] phase 8: hardening and performance pass

### remaining MVP hardening

- test real microphone recording on multiple devices
- run a long playback soak test
- improve thread synchronization around realtime buffer swaps
- decide whether the browser dashboard remains part of the official surface
- add true time-stretch/pitch-shift if quality becomes important

## future: robust version

```
rust audio engine
+ terminal UI (ratatui)
+ python/node/rust agent layer
+ local API / websocket bridge
+ adapters for STT, SFX, TTS, AKOUO
+ MIDI / OSC / GPIO / raspberry pi controls
```

### potential rust stack

- `cpal` for audio IO
- `ratatui` for terminal UI
- `rubato` for resampling
- custom DSP crates
- websocket/local API bridge to agent layer

### hardware extension targets

- MIDI controller
- foot pedal
- OSC
- raspberry pi
- fates OLED interface
- GPIO buttons
- small hardware looper box

## non-goals (permanent)

- DAW features (multitrack timeline, plugin hosting, arrangement)
- chatbot behavior
- generic text-to-music generation
- always-on surveillance listening
- large-model dependency for basic operations
