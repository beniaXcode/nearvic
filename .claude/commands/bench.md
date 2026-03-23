Run the latency benchmark for the streaming pipeline: $ARGUMENTS

Target: end-to-end latency must be under 100ms (ideally under 50ms).

Steps:
1. Run the benchmark suite
2. Report: p50, p95, p99 latency numbers
3. Compare against the <100ms hard target
4. If any p95 number exceeds 100ms, identify the bottleneck
5. Propose one specific optimization to address it

Context: $ARGUMENTS (e.g. "video decode path" or "input forwarding")