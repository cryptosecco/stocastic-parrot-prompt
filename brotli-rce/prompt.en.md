# Using AI agents? You’re at risk: the prompt that keeps you safe

- URL: https://stocasticparrot.ai/en/security/brotli-rce/
- Updated: 2026-11-01

```text
You are a technical assistant. Your task is to check this machine and secure it against CVE-2026-111497 (an out-of-bounds write in Google’s Brotli decoder, which is included in Node.js and Bun) and against the other 9 vulnerabilities in the Node.js security release of October 21, 2026.
Run the steps in order, record every output, and summarize the final state. Before each update, show the command and wait for my OK.

1. Full inventory
• Show: node -v, which -a node (on Windows: where node) and the version of every node found; bun -v and which -a bun; claude --version and claude doctor
• Look for other runtimes: Node/Bun installs managed by nvm, fnm, asdf, Volta, or similar
• Identify the AI tools and agents on this machine (Claude Code, Cursor, Codex, Aider, Open Interpreter, Continue, Hermes Agent, etc.) and check whether they use a bundled runtime: look for folders that contain their own node or bun
• Look for single-file executables (Node SEA, bun build --compile): they bundle the runtime and must be recompiled
• Check the Docker images: docker images | grep -E 'node|bun'
• On Linux, check the version of the system brotli package: on Debian and Ubuntu, Node uses it

2. Node.js update
• Bring the system Node and every managed install to the fixed versions: ≥ 22.23.4 on line 22, ≥ 24.22.1 on line 24, ≥ 26.12.1 on line 26
• Release lines 25, 23, 21, 20, and older don’t get the fix: propose a migration to a supported line
• Use the method that matches how each one was installed (nvm, Homebrew, NodeSource, winget, official installer)
• Restart any running Node processes

3. Bun and Claude Code update
• Update Bun to ≥ 1.4.4 (bun upgrade, or brew upgrade bun if it comes from Homebrew)
• Claude Code must be ≥ 2.1.308. Native install: claude update. npm: npm install -g @anthropic-ai/claude-code@latest. Homebrew: brew upgrade claude-code (or claude-code@latest). WinGet: winget upgrade Anthropic.ClaudeCode. apt, dnf, apk: update the claude-code package
• Update the other AI tools that bundle their own runtime, through their official channel

4. Docker and containerized environments
• Flag the images based on vulnerable versions
• Give the commands to update them: docker pull node:24 (or the tag in use), then docker build --pull and a new deploy. Restarting the old container is not enough

5. Packages and system
• Update the global package managers (npm, yarn, pnpm), if present
• Suggest updating the operating system (apt, brew, winget, Windows Update, macOS updates)
• Note: npm audit does not cover this bug, because it is in the runtime, not in the packages

6. Final check and recommendations
• Re-run the version checks on every runtime found
• Confirm that no vulnerable runtimes are still active
• List the manual actions that remain
• Suggest a minimum set of good practices: isolate agents when possible, don’t fetch untrusted content without checks, keep automatic updates on, don’t run PoCs found online

Do not run destructive operations: no uninstalls, no deletions. At the end, report a table (runtime, path, version before and after, status) and separate what you updated from what needs human action.
```
