# nearvic-agent — Context

## What this crate is
The Rust binary running on the cloud VM (server side).
Captures the VM screen, encodes it, streams to the client.
Receives input events and injects them into the VM.

## Environment
- Runs on Linux (x86_64) on a GPU-enabled cloud VM
- Has access to GPU for hardware-accelerated video encoding
- OS: whatever the cloud provider runs (Ubuntu preferred)
- Must support Windows VM screen capture long-term (via API)

## What this binary does
1. Captures VM screen frames (at target FPS)
2. Encodes frames using GPU hardware encoder (H.264 / H.265)
3. Streams encoded video to connected client over QUIC
4. Receives input events from client → injects into VM OS
5. Captures and streams audio (bidirectional)
6. Handles USB passthrough (deferred to post-MVP)

## Performance rules
- Screen capture must be low-latency — avoid full copy pipelines
- Encoding MUST use GPU hardware encoder (NVENC, VAAPI, etc.) — not CPU
- Encoding pipeline must handle target FPS without dropping frames

## Gotchas
- Screen capture method differs between Linux and Windows — abstract it
- Input injection requires OS-level APIs (uinput on Linux, SendInput on Windows)
- Never hardcode GPU vendor — detect and use available hardware encoder