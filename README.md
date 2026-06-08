# Plan with Corvi — Claude Code plugin

Connect your agent to [Corvi](https://corvi.sh)'s **code-grounded implementation plans**. Corvi drafts, reviews, and synthesizes a plan against your actual repo (multi-model) in the macOS app; this plugin lets Claude Code (or any MCP agent) **read, dispatch, and verify** those plans — Corvi is the planning backend, your agent does the work.

Read-only: plans are authored in the Corvi app. (Agent-triggered plan generation is planned for a later release.)

## Prerequisites

- **[Corvi.app](https://corvi.sh)** installed (the plugin runs the `corvi` CLI bundled inside it — default `/Applications/Corvi.app/Contents/Resources/corvi`).
- At least one plan saved in your Corvi library.

## Install

```
/plugin marketplace add corvi-sh/claude-plugin
/plugin install corvi@corvi
```

If Corvi.app isn't in `/Applications`, set the plugin's **`corvi_binary`** config to the path of `Corvi.app/Contents/Resources/corvi`.

## What you get

A `corvi` MCP server (stdio) exposing your plan library:

| Tool | Does |
|---|---|
| `list_plans` | All plans: id, title, type, workspace, created, todo count |
| `search_plans` | Plans matching a query (title/prompt/body) |
| `get_plan` | A plan's Markdown + structured fields |
| `get_plan_todos` | The actionable checklist (files + acceptance per todo) |
| `plan_dispatch` | Pending todos as ordered, file-disjoint parallel-safe waves |
| `plan_verify` | Structurally check a `git diff --name-only` against the plan |

Plus a **`plan-with-corvi` skill** (drives the read → dispatch → implement → verify loop) and a **`/corvi [query]`** command to start from a plan.

## How it works

The plugin registers `corvi mcp-serve` (the read-only MCP server shipped in the Corvi CLI) — the same server the app's in-app "Connect" button installs, packaged for one-command distribution. It reads the app's local plan store; nothing leaves your machine.
