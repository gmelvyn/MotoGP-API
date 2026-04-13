# Repository Guidelines

## Project Structure & Module Organization
`src/` contains the published library surface. Use `src/client/MotoGPClient.ts` for HTTP client logic, `src/types/` for shared API response types, `src/utils/helpers.ts` for reusable helpers, and `src/index.ts` for package exports. Tests live in `test/`, currently centered in `test/client.test.ts`. Build output is generated into `dist/` and should not be edited by hand.

## Build, Test, and Development Commands
This project is built with Bun.

- `bun run build`: bundles `src/index.ts` into `dist/` and generates declaration files with `tsc`.
- `bun test`: runs the Bun test suite in `test/`.
- `bun run lint`: runs ESLint across `.ts` files.
- `bun run types`: emits `.d.ts` files only, useful when checking public typings.

Run commands from the repository root, for example: `bun test`.

## Coding Style & Naming Conventions
Write TypeScript as ES modules and keep `.js` extensions in internal imports, matching the current source. Follow the existing style: 2-space indentation, semicolons, single quotes, trailing commas only where already used, and `PascalCase` for classes/types (`MotoGPClient`, `BroadcastEvent`). Use `camelCase` for functions and methods (`getBroadcastEvents`, `parseTimeToMs`) and `UPPER_SNAKE_CASE` for exported constants such as `CATEGORY_IDS`.

Keep public methods documented with concise JSDoc when behavior or parameters are not obvious.

## Testing Guidelines
Tests use `bun:test` with `describe`, `test`, and `expect`. Name test files `*.test.ts` and colocate broad integration coverage in `test/`. Prefer deterministic unit tests for helpers, and wrap network-dependent API checks defensively, as current tests do, because the MotoGP endpoints may be unavailable. There is no explicit coverage gate in the repo; add tests for every public method or helper you change.

## Commit & Pull Request Guidelines
Recent history favors short Conventional Commit prefixes, mainly `feat:` and `fix:`. Keep commit subjects imperative and specific, for example `feat: add rider statistics endpoint`. For pull requests, include a clear summary, note any API contract changes, list the commands you ran (`bun test`, `bun run build`), and attach example payloads or screenshots only when documentation output changes.

## Security & Configuration Tips
Do not hardcode secrets; the client currently uses public MotoGP endpoints and accepts configuration through `ClientOptions`. When changing request behavior, preserve sane defaults for `baseURL`, timeout, and `User-Agent`.
