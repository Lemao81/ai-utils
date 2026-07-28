## Agent Instructions

- Never execute `pnpm install`, `pnpm add`, `pnpm remove`, or any other command that installs/mutates dependencies. Edit `package.json` directly and tell the user to run the install themselves.
- Never execute `git commit` on your own without explicit instruction. After explicit instruction, execute without asking for additional confirmation.
- In this sandbox, `node_modules` was installed on Windows: `pnpm` is unavailable, `.bin` shims fail, and platform-specific binaries (e.g. Biome's Linux CLI) are missing. Never attempt `npx <tool>`, `pnpm exec <tool>`, `pnpm <script>`, or login-shell fallbacks. To verify changes, run `node node_modules/typescript/bin/tsc --noEmit` (ignore pre-existing errors in unrelated files) and skip lint/format checks — the user runs `pnpm check` on the host.
- When the entire user message is `coa`, treat it as the command `commit all`.

## Code Style
- General:
  - Insert new line before return keyword if not first line of block.
  - Put single line statements in curly braces to separate line.
  - Never add comments, except tool-control directive comments when explicitly instructed — e.g. suppression/ignore/pragma comments for linters, formatters, type-checkers, or static analyzers.
  - Leave edited files with CRLF line ending.
- C#:
  - Tests:
    - Use Arrange, Act, Assert pattern (comment each section in method).
- TypeScript:
  - Remove braces around arrow function with single-statements.
  - Add the return type to all functions, except component functions.
  - For react components props declarations, use TypeScript type, not interface.
  - Always use single quotes, matching the Biome config's `quoteStyle`.
- Cypress:
  - Select elements only via `cy.get('[data-cy=...]')`; add a `data-cy` attribute to every element a test targets.
  - Keep `it()` titles to a few words naming the main thing, not action→result sentences.

## Workflows

### Creating/Modifying API endpoints

When creating or modifying API endpoints:

1. Add/update the endpoint in the .http file, use a sample payload for POST/PUT/PATCH methods.
