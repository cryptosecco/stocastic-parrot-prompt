# Turn off auto-compaction in Claude Code

- URL: https://stocasticparrot.ai/en/tutorials/turn-off-auto-compaction/
- Updated: 2026-11-03
- Tested with: Claude Code 2.1.311 (2026-10-27)

```text
Check with claude --version that Claude Code is on 2.1.311 or later; if it’s older, stop and tell me. Then, in ~/.claude/settings.json, set "autoCompactEnabled": false and "idleCompaction": false. If the file doesn’t exist, create it. Don’t touch the other keys. Before saving, show me the file as it is now and as it will be, and wait for my yes.
```
