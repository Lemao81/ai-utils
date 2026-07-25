## Agent Instructions

- Never execute `pnpm install`, `pnpm add`, `pnpm remove`, or any other command that installs/mutates dependencies. Edit `package.json` directly and tell the user to run the install themselves.
- Never execute `git commit` on your own without explicit instruction. After explicit instruction, execute without asking for additional confirmation.
- In this sandbox, `node_modules` was installed on Windows: `pnpm` is unavailable, `.bin` shims fail, and platform-specific binaries (e.g. Biome's Linux CLI) are missing. Never attempt `npx <tool>`, `pnpm exec <tool>`, `pnpm <script>`, or login-shell fallbacks. To verify changes, run `node node_modules/typescript/bin/tsc --noEmit` (ignore pre-existing errors in unrelated files) and skip lint/format checks — the user runs `pnpm check` on the host.
- When the entire user message is `coa`, treat it as the command `commit all`.

## Code Style
- General:
  - insert new line before return keyword if not first line of block
  - put single line statements in curly braces to separate line
  - never add comments
  - leave edited files with CRLF line ending
- C#:
  - Tests:
    - Arrange, Act, Assert pattern (comment each section in method)
- Typescript:
  - Remove braces around arrow function with single-statements
  - Add the return type to all functions, except component functions
  - for react components props declarations, use typescript type, not interface
  - when creating Cypress tests, use the data-cy attribute as targeted selector for elements used in the test

## Workflows

### Creating/Modifying API endpoints

When creating or modifying API endpoints:

1. Add/update the endpoint in the .http file, use a sample payload for POST/PUT/PATCH methods
