## Agent Instructions

- Never execute `pnpm install`, `pnpm add`, `pnpm remove`, or any other command that installs/mutates dependencies. Edit `package.json` directly and tell the user to run the install themselves.
- Never execute `git commit` on your own without explicit instruction. After explicit instruction, execute without asking for additional confirmation.
- In this sandbox, `node_modules` was installed on Windows: `pnpm` is unavailable, `.bin` shims fail, and platform-specific binaries (e.g. Biome's Linux CLI) are missing. Never attempt `npx <tool>`, `pnpm exec <tool>`, `pnpm <script>`, or login-shell fallbacks. To verify changes, run `node node_modules/typescript/bin/tsc --noEmit` (ignore pre-existing errors in unrelated files) and skip lint/format checks — the user runs `pnpm check` on the host.
- When the entire user message is `coa`, treat it as the command `commit all`.

## Code Style
- General:
  - Insert an empty line before `return`, unless it is the first statement in its block.
  - Always brace a control-flow body and put its statement on its own line — never `if (x) return`.
  - Never add comments, except tool-control directive comments when explicitly instructed — e.g. suppression/ignore/pragma comments for linters, formatters, type-checkers, or static analyzers.
  - Preserve a file's existing line endings; write new files with CRLF.
- C#:
  - Tests:
    - Structure tests with the Arrange-Act-Assert pattern, marking each section with an `// Arrange`, `// Act` or `// Assert` comment.
- TypeScript:
  - Omit the braces and `return` when an arrow function body is a single expression, except in React components; keep them where the implicit return would change behaviour, such as a `useEffect` callback.
  - Add an explicit return type to every named function, except React components; inline callbacks may rely on inference. Omit it where the annotation would only restate an unspellable inferred type.
  - Use a `type` alias for React component props, never an `interface`.
  - Always use single quotes, matching the Biome config's `quoteStyle`.
  - Insert an empty line after a multi-line block statement (`if`, `for`, `while`, `do`/`while`, `switch`, `try`/`catch`), unless it is the last statement in its scope. Never insert one before a continuation keyword (`} else {`, `} catch {`, `} finally {`, `} while (…);`).
- Cypress:
  - Select elements only via `cy.get('[data-cy=...]')`; add a `data-cy` attribute to every element a test targets.
  - Keep `it()` titles to a few words naming the main thing, not action→result sentences.

## Workflows

### Creating/Modifying API endpoints

When adding or changing an API endpoint:

1. Add or update its request in the project's .http file, with a realistic sample body for POST, PUT and PATCH.
