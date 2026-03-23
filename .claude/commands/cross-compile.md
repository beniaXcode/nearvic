Verify nearvic-client compiles cleanly for the ARM64 target.

Steps:
1. Run: cross build -p nearvic-client --target aarch64-unknown-linux-gnu --release
2. If it fails, show the full error and propose a fix
3. If it succeeds, run: cargo clippy -p nearvic-client --target aarch64-unknown-linux-gnu -- -D warnings
4. Report: binary size, any clippy warnings, compile time

Goal: zero warnings, clean binary for ARM64.