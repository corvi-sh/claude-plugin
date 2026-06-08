---
description: List or search your Corvi plans and start work from one (read its todos, dispatch waves).
argument-hint: "[search query]"
---

You have access to the `corvi` MCP server (Corvi's plan library).

- If `$ARGUMENTS` is non-empty, call `search_plans` with it.
- Otherwise call `list_plans`.

Show the matches compactly (title · type · workspace · todo count · id). Then ask the user which plan to work on (or proceed if there's an obvious single match). Once chosen:

1. `get_plan_todos { id }` to load the work items, and `get_plan { id }` if you need the full approach.
2. `plan_dispatch { id }` to get parallel-safe waves.
3. Implement wave by wave (see the `plan-with-corvi` skill), then `plan_verify { id, paths }` with `git diff --name-only` output.

Plans are authored in the Corvi app — this is read-only.
