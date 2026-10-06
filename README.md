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

## Releasing

Always release with [plugin-kit](https://github.com/aeriondyseti/plugin-kit)'s `release` command. It bumps the version, tags the release, and pins this plugin's entry in the [aeriondyseti-plugins](https://github.com/aeriondyseti/aeriondyseti-plugins) marketplace to that exact tag and commit in one step, so the published plugin never drifts from this repo. Don't bump versions, create tags, or edit the marketplace entry by hand.

1. Add your changes under `## [Unreleased]` in `CHANGELOG.md` and commit them. `release` refuses to run with an empty `[Unreleased]` section or a dirty tree.
2. Optionally run `npx @aeriondyseti/plugin-kit doctor` to catch anything that would break the plugin once installed.
3. From this repo, with the marketplace repo cloned alongside it (adjust the path if yours lives elsewhere), preview and then release:

   ```bash
   npx @aeriondyseti/plugin-kit release patch --plugin . --marketplace ../aeriondyseti-plugins/.claude-plugin/marketplace.json --dry-run
   npx @aeriondyseti/plugin-kit release patch --plugin . --marketplace ../aeriondyseti-plugins/.claude-plugin/marketplace.json
   ```

   Use `patch`, `minor`, `major`, or an explicit `x.y.z`. This bumps `.claude-plugin/plugin.json`, moves `[Unreleased]` under the new version in `CHANGELOG.md`, commits `Release x.y.z`, tags `vx.y.z`, and updates `ref`, `sha`, and `version` in the marketplace entry. It never pushes.
4. Push this repo first: `git push origin main --follow-tags`.
5. Then commit and push the marketplace change. Pushing it first would pin a commit GitHub doesn't have yet, and installs would fail.

## License

MIT
