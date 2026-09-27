# MCP Server Configuration

## Which server did you connect?
**@anthropic-ai/mcp-server-filesystem** — Anthropic's built-in filesystem MCP server

## Why is it useful here?
The filesystem server provides structured access to the project's documentation and source files. For this Course API, it allows Claude to directly read:
- API reference documentation (`docs/api.md`)
- Source code structure (`routes/`, `db/store.js`, etc.)
- Test files and configuration

This enables Claude to answer questions about the API, understand endpoint signatures, and reference implementation details without manual context-passing.

## What did your permission rule allow?
The permission rule restricts the filesystem server to **read-only operations**:
- `read_file` — read file contents
- `list_directory` — list directory contents

This prevents any write, delete, or modification operations, keeping the server safe and scoped to information retrieval.

## Configuration Location
- Server definition: `.claude/.mcp.json`
- Permission rules: `.claude/settings.json`
- Root path: project root (`.`) — exposes all project files
