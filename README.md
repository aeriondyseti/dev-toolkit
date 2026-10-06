# dev-toolkit

Development toolkit for Claude Code: MCP servers (Serena, Context7, RepoMap) and git workflow skills.

## Install

```bash
/plugin marketplace add AerionDyseti/aeriondyseti-plugins
/plugin install dev-toolkit@aeriondyseti-plugins
```

## MCP Servers (auto-loaded)

| Server | Purpose |
|--------|---------|
| [Serena](https://github.com/oraios/serena) | LSP-backed semantic code navigation, symbol search, and symbolic editing |
| [Context7](https://github.com/upstash/context7) | Up-to-date library documentation lookup |
| [repomap-mcp](https://github.com/nicobailon/repomap-mcp) | Aider-style ranked codebase map via tree-sitter + PageRank |

## Skills

| Skill | Triggers On |
|-------|-------------|
| **Codebase Orientation** | Start of conversation, unfamiliar codebase, "how does X work" |
| **Git Conventions** | Commit message format, branch naming, release flow reference |
| **Creating Commits** | Staging files, writing conventional commit messages, pre-commit validation |
| **Branch Management** | Creating, switching, syncing, or cleaning up branches |
| **Pull Request Workflow** | Creating PRs, responding to feedback, merge strategies |

## Commands

| Command | Description |
|---------|-------------|
| `/dev:orient [file\|symbol]` | Generate a ranked codebase map, optionally focused on a file or symbol |
| `/dev:branch [type] [name]` | Quick-create a properly named feature or fix branch from dev |
| `/dev:commit [--all]` | Stage and commit changes with a conventional commit message |
| `/dev:sync` | Sync current branch with upstream (rebase on dev/main) |
| `/dev:pr [--draft] [--base]` | Create a PR with auto-generated description from commit history |
| `/dev:ship [--draft] [--base]` | Commit, push, and open a PR in one step |
| `/dev:clean [--gone]` | Clean up stale branches: gone remotes, merged branches, and worktrees |

## Prerequisites

- [uv](https://docs.astral.sh/uv/) (for Serena via `uvx`)
- [Node.js](https://nodejs.org/) (for Context7 and RepoMap via `npx`)

## License

MIT
