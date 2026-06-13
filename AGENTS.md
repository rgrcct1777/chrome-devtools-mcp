This repository contains an MCP server and CLI for Chrome DevTools.

# Instructions

- Use only scripts from `package.json` to run commands.
- Use `npm run build` to run tsc and test build.
- Use `npm run test` to build and run tests, run all tests to verify correctness.
- Use `npm run test path-to-test.ts` to build and run a single test file, for example, `npm run test tests/McpContext.test.ts`.
- Use `npm run format` to fix formatting and get linting errors.

## Rules for TypeScript

- Do not use `any` type.
- Do not use `as` keyword for type casting.
- Do not use `!` operator for type assertion.
- Do not use `// @ts-ignore` comments.
- Do not use `// @ts-nocheck` comments.
- Do not use `// @ts-expect-error` comments.
- Prefer `for..of` instead of `forEach`.

## Cursor Cloud specific instructions

- The build/prepare scripts run `.ts` files directly (`node scripts/post-build.ts`, `node scripts/prepare.ts`), which require Node's TS type-stripping (Node >= 22.18 or >= 24; see `.nvmrc` which pins v24). The Cloud VM's default non-login `node` is v22.14 and fails these with `ERR_UNKNOWN_FILE_EXTENSION`. Run `npm`/build/test commands from a login shell (`bash -l`), which resolves the nvm-managed Node v22.22.2, or prepend it: `export PATH="$HOME/.nvm/versions/node/v22.22.2/bin:$PATH"`. `nvm use 22` alone may not win over the system `node` on `PATH`.
- `google-chrome-stable` is installed, so live browser automation and the CLI work headlessly. Quick end-to-end check via the built CLI: `node build/src/bin/chrome-devtools.js new_page "https://example.com"` then `... take_screenshot --filePath out.png` (use `... stop` to shut down the background daemon).
