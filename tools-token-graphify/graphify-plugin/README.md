# graphify — Claude Code plugin

Packages the [graphify](../graphify) knowledge-graph tool as an installable Claude Code plugin.

Turn any folder of code, docs, papers, images, or videos into a navigable knowledge graph with
community detection, an honest `EXTRACTED / INFERRED / AMBIGUOUS` audit trail, and three outputs:
interactive HTML, GraphRAG-ready JSON, and a plain-language `GRAPH_REPORT.md`.

## What's inside

| Component | Path | Purpose |
|-----------|------|---------|
| Skill | `skills/graphify/SKILL.md` | The full `/graphify` pipeline + query logic (auto-loaded by Claude). |
| Command | `commands/graphify.md` | Slash command `/graphify` that hands off to the skill. |
| Hook | `hooks/hooks.json` | On `Stop`, runs `graphify update .` (AST-only, no API cost) when a `graphify-out/` graph exists, keeping it current. |

## Prerequisite

The plugin drives the `graphify` Python CLI. Install it once:

```bash
uv tool install graphifyy     # recommended (puts `graphify` on PATH)
# or: pipx install graphifyy
```

## Install the plugin

From the repository root (`tools-token-graphify/`, which holds `.claude-plugin/marketplace.json`):

```bash
claude plugin marketplace add .
claude plugin install graphify@graphify-marketplace
```

Then restart Claude Code. Verify with `/plugin` (should list **graphify**) and `/help` (should show `/graphify`).

## Usage

```
/graphify                                   # full pipeline on current directory
/graphify <path>                            # full pipeline on a specific path
/graphify https://github.com/owner/repo     # clone a repo, then build its graph
/graphify <path> --update                   # incremental re-extract of changed files
/graphify query "how does auth reach the DB?"
/graphify path "AuthModule" "Database"      # shortest path between two concepts
/graphify explain "SwinTransformer"
/graphify --help                            # print the full usage block
```

Outputs land in `graphify-out/` (graph.json, graph.html, GRAPH_REPORT.md, Obsidian vault).
