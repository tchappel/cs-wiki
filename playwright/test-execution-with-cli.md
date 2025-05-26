# Test Execution with CLI

run all tests (headless by default)

```bash
npx playwright test
```

show test report

```bash
npx playwright show-report
```

run one test file

```bash
npx playwright test <test-file>
```

run one test name

```bash
npx playwright test -g "test name"
```

run one test file with a specific browser

see `playwright.config.ts` under `projects` for the list of browsers

```bash
npx playwright test <test-file> --project=chromium
```

run one test file in headed mode (visible browser)

```bash
npx playwright test <test-file> --headed
```

Enable tracing (trace viewer) for debugging

A trace viewer is a sequence of snapshots of the test execution plus logs.

```bash
npx playwright test --trace on
```

## Run tests in `UI Mode`

This is a new feature in Playwright 1.28.0 that allows you to run tests in a UI mode.
This is useful for debugging and visualizing the test execution.

```bash
npx playwright test --ui
```

## Run tests using playwright debugger

this will run the test showing

- browser
- playwright inspector

With the playwright inspector, you can run and see the test execution, even step by step, and debug.

```bash
npx playwright test --debug
```
