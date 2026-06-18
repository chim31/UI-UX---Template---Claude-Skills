---
description: Build or query a graphify knowledge graph
argument-hint: "[path|url] | query \"<question>\" | add <url> | --help"
---

Invoke the `graphify` skill immediately.

Pass the full `/graphify` argument string through unchanged: `$ARGUMENTS`.
If no arguments were supplied, treat the target path as `.` (current directory).

Examples:
- `/graphify`
- `/graphify src --update`
- `/graphify https://github.com/owner/repo`
- `/graphify query "what connects auth to billing?"`
- `/graphify add https://example.com/paper.pdf`

Do not answer from raw files before handing off to the `graphify` skill.
