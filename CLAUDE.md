# Nearvic — Root Context

## What this project is
Cloud-powered remote desktop platform. Low-power ARM client device streams
a full desktop from a GPU-backed cloud VM. Client OS is a minimal Buildroot
Linux that boots directly into a single Rust app. No desktop environment.

## Workspace structure
- nearvic-client/  → Rust app running on ARM thin client (video decode, input, display)
- nearvic-agent/   → Rust app running on cloud VM (screen capture, encode, stream)
- nearvic-proto/   → Shared protocol types used by both crates

## Core language
Rust everywhere. C only via FFI for hardware drivers if absolutely necessary.
Web dashboard: TypeScript + Next.js (separate, not in this repo).

## Build commands
cargo build --workspace
cargo test --workspace
cargo clippy --workspace -- -D warnings
cargo fmt --check

## Cross-compile for ARM64 (client only)
cross build -p nearvic-client --target aarch64-unknown-linux-gnu --release

## Key constraints — never violate these
- Client must compile and run on aarch64-unknown-linux-gnu
- No std desktop environment on client (no X11, no Wayland, no compositor)
- All network communication must be encrypted
- No proprietary protocols (no PCoIP, no RDP)
- Latency target: <100ms end-to-end, ideally <50ms
- Boot time target: <2 seconds on client device

## Key decisions already made — do not revisit
- OS: Buildroot-based minimal Linux (Redox rejected — no GPU/Wi-Fi/USB drivers)
- Transport: QUIC-based (low latency, built-in TLS, multiplexing)
- Primary codec direction: H.264 / H.265 hardware decode on client
- Rendering: DRM/KMS or EGL directly (no compositor overhead)
- Input: evdev kernel subsystem

## Open questions (still deciding — propose options, don't assume)
- Final codec: H.264 vs H.265 vs AV1
- QUIC only vs WebRTC fallback
- USB passthrough depth

## Git rules
- Always create a new branch before starting any feature or fix
- Never commit directly to main
- Every commit message must explain WHY, not just what changed
- Run `cargo clippy` and `cargo fmt` before every commit

## Gotchas (things Claude has gotten wrong before — avoid these)
- Do not suggest adding a window manager or compositor to the client OS
- Do not assume std library features unavailable in no_std contexts
- Do not use tokio::main on the client if it conflicts with DRM event loop
- The client and agent are separate binaries — do not merge them
- nearvic-proto must stay dependency-free of hardware crates