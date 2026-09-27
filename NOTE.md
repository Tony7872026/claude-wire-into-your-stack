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

---

# Project Skills

Two project skills teach Claude about core conventions used in this repository.

## Skill 1: Test Structure Convention
**File:** `.claude/skills/test-structure.md`

**What it captures:** How tests are structured using Node's `test` module, `supertest` for HTTP requests, and `node:assert` for assertions. Includes patterns for setup with `test.beforeEach()`, making requests, checking `res.status` and `res.body`, and naming conventions.

**How it fires:** Triggered when writing or reviewing test cases, adding tests, debugging test failures, or explaining test patterns. Keywords: "write test", "test case", "test fails", "review test", "test structure", "add test".

**Example trigger:** User asks "I need to write a test that verifies the PUT endpoint returns 404 when the user doesn't exist. What should the test look like?" → skill automatically provides the `test()` pattern, `supertest` usage, and assertion examples.

---

## Skill 2: Error Response Format Convention
**File:** `.claude/skills/error-response-format.md`

**What it captures:** The standard error response format (`{ "error": "message" }`), HTTP status codes (400 for validation, 404 for not found, 201 for created), and the implementation pattern using early `return` statements. Teaches consistency in error handling across all routes.

**How it fires:** Triggered when handling errors, returning error responses, reviewing error handling code, working with error formats, or checking API error behavior. Keywords: "error response", "error handling", "return error", "404", "400", "error message", "error format".

**Example trigger:** User asks "I'm adding a delete endpoint. If the user doesn't exist, what should the error response look like?" → skill automatically provides the error JSON shape, 404 status code, and implementation pattern.
