Review all changes in the current git branch compared to main.

Focus on:
1. Memory safety — any unsafe blocks, raw pointers, potential leaks
2. Latency regressions — anything that could add latency to the streaming pipeline
3. Protocol compatibility — any changes to nearvic-proto types that break compatibility
4. ARM64 compatibility — anything that won't compile or run on aarch64-unknown-linux-gnu
5. Missing error handling — unwrap(), expect(), panic!() in production paths
6. Security — unencrypted data paths, missing auth checks

Be direct. List real issues only. Skip style and naming comments.
Format: one issue per line, with the file:line reference.