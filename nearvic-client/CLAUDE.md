# nearvic-client — Context

## What this crate is
The Rust binary that runs on the ARM64 thin client device.
Boots fullscreen from BusyBox init. No user can ever see the OS beneath it.

## Hardware context
- Target: ARM64 (aarch64-unknown-linux-gnu)
- Boards: Khadas VIM4 (Amlogic A311D2) or RK3566-based
- Has: hardware VPU for video decode, HDMI out, evdev input, Wi-Fi, USB
- No GPU for compute — only VPU for decode

## What this binary does
1. Starts fullscreen (DRM/KMS or EGL, no compositor)
2. Connects to nearvic-agent over QUIC
3. Receives encoded video frames → hardware decode → render to display
4. Captures keyboard/mouse/gamepad via evdev → sends to agent
5. Plays audio (bidirectional)
6. Forwards USB devices to agent

## Rendering approach
Use DRM/KMS directly or EGL. Do NOT use:
- X11 or any Xorg dependency
- Wayland or any Wayland protocol
- Any desktop toolkit (GTK, Qt, etc.)

## Performance rules
- Video decode MUST use hardware VPU — never software decode in production
- Input latency must be minimal — no buffering input events
- Keep binary size small — this runs from a read-only minimal OS image

## Gotchas
- The evdev fd and DRM fd need careful event loop integration — do not block either
- Hardware decode APIs vary per SoC — abstract behind a trait
- No network calls except to nearvic-agent — this is a closed appliance