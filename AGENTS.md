# Repository Guidelines

## Project Structure & Module Organization
Core library code lives in `src/`. Format-specific parsers are split by domain: `src/hwp5`, `src/hwpx`, `src/pdf`, `src/xlsx`, and `src/docx`. Shared entrypoints and utilities sit in files such as `src/index.ts`, `src/cli.ts`, `src/mcp.ts`, `src/types.ts`, and `src/utils.ts`. Higher-level features are grouped under `src/diff`, `src/form`, `src/table`, and `src/ocr`.

Tests live in `tests/` and mostly follow a feature-per-file layout such as `tests/detect.test.ts` or `tests/security.test.ts`. Keep reusable sample inputs in `tests/fixtures/`. The `demo/` directory contains the Remotion-based showcase app used to generate `demo.gif`.

## Build, Test, and Development Commands
- `npm ci`: install pinned dependencies for local work or CI.
- `npm test`: run the Node test suite via `node --import tsx --test tests/*.test.ts`.
- `npm run build`: bundle the library and CLI into `dist/` with `tsup`.
- `npm run dev`: rebuild on change while developing library code.
- `cd demo && npm install && npm run preview`: open the demo composition locally.
- `cd demo && npm run render`: regenerate `demo.gif` after demo changes.

CI runs `npm ci`, `npm test`, and `npm run build` on Node 18, 20, and 22. Keep changes compatible across that matrix.

## Coding Style & Naming Conventions
This is a strict TypeScript ESM project targeting Node 18+. Follow the existing style: use double quotes, omit semicolons, prefer named exports, and keep filenames lowercase with hyphens where needed (`cluster-detector.ts`, `text-diff.ts`). Use 2-space indentation and keep parser logic close to its format-specific module.

There is no dedicated lint script in the repo today, so consistency with nearby code is the standard. Preserve public API names in `src/index.ts` unless a breaking change is intentional.

## Testing Guidelines
Add or update `*.test.ts` files in `tests/` for every behavior change. Prefer targeted tests next to the affected feature area, and use `tests/fixtures/` for stable sample documents. Cover both success paths and failure/security cases when touching parsers, file detection, OCR, or archive handling.

## Commit & Pull Request Guidelines
Recent history uses Conventional Commit prefixes such as `feat:`, `fix:`, `docs:`, and `chore:`. Keep commit subjects short, imperative, and scoped to one logical change. For pull requests, include a concise description, note affected document formats, list test coverage, and attach sample output or screenshots when CLI output, parsing quality, or the `demo/` assets change.
