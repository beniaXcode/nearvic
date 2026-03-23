Prepare and make a safe commit for the current changes.

Steps:
1. Run cargo fmt --check — fix any formatting issues first
2. Run cargo clippy --workspace -- -D warnings — fix all warnings
3. Run cargo test --workspace — all tests must pass
4. Run cross build -p nearvic-client --target aarch64-unknown-linux-gnu — must compile
5. Show me git diff --stat for final review
6. Write a commit message that explains WHY this change was made (not just what)
7. Wait for my approval before running git commit

Do not commit if any of steps 1-4 fail.
