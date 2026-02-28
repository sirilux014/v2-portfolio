# Environment Variables on Windows CLI Tool Installations

**Date**: 2026-02-28
**Source**: rrr: v2-portfolio

## The Pattern
When downloading and executing new CLI tools (like `gh`, `bun`, or Git) via PowerShell during an active session, the `$env:Path` often remains stale downstream in the same command execution chain or immediately following script phases.

## The Friction
Attempting to run `bunx` right after installing `bun` failed with a "CommandNotFoundException", even when forcefully appending to `$env:Path` within the same execution line.

## Resolution
1. **Absolute Paths Guarantee Execution**: If a tool was just installed into a user directory (e.g., `C:\Users\admin00\.bun\bin\bunx.exe`), call the absolute binary path directly for immediate downstream operations instead of relying on `$env:Path`.
2. **Git Identity Initialization**: Fresh environments without global git config require explicit `--global user.name` and `user.email` definitions before the first commit. Do not assume `git init -> git commit` will succeed blindly on new VMs.
