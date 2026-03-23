Enter plan mode for the following task: $ARGUMENTS

Before writing any code:
1. Read all relevant CLAUDE.md files in this workspace
2. Ask me clarifying questions using the AskUserQuestion tool — focus on:
   - Hardware/OS constraints I might not have considered
   - Latency or performance implications
   - How this interacts with nearvic-proto (shared types impact)
   - Edge cases in the streaming pipeline
3. Write a complete implementation plan to .claude/CURRENT_PLAN.md
4. Wait for my approval before writing a single line of code

Do not implement anything until I explicitly say "approved" or "go ahead".