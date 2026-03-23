Save the current session state to .claude/PROGRESS.md

Include:
1. What we were working on
2. What was completed this session (list changed files)
3. Current state of the codebase (does it compile? do tests pass?)
4. What was left unfinished
5. The exact next action to take in the next session
6. Any decisions made this session that should be added to a CLAUDE.md file

Then run: git diff --stat to show what changed.
This file will be read at the start of the next session to resume context.