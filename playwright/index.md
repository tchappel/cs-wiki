# Playwright

## Skip test

```typescript
test.skip("test name", async ({ page }) => {
  // test code
});
```

## Run only one test

```typescript
test.only("test name", async ({ page }) => {
  // test code
});
```

- [test execution with CLI]("./text-execution-with-cli.md")
- [test execution with UI]("./text-execution-with-ui.md")
- [fixtures]("./fixtures.md")
- [Hooks and Flow Control]("./hooks-and-flow-control.md")
- [UI Components]("./ui-components.md")

## Locator

[Locator](https://playwright.dev/docs/api/class-locator) finds all elements on the page that matched a selector (Playwright's custom selector engine).

A locator can be created with the [page.locator()](https://playwright.dev/docs/api/class-page#page-locator) method.

```typescript
import { test } from "@playwright/test";

test("test name", async ({ page }) => {
  // by tag
  page.locator("tagName");

  // by id
  page.locator("#some-id");

  // by class
  page.locator(".some-class");

  // by attribute
  page.locator("[attribute='value']");

  // by class value in full (same as attribute)
  page.locator("[class='value1 value2']");

  // by partial text match
  page.locator(":text('substring')");

  // by exact text match
  page.locator(":text-is('exact string')");

  // combined
  page.locator("tagName#some-id.some-class[attribute='value']");

  // by XPath
  page.locator("//tagName[@attribute='value']");

  // get first element that matches the selector
  page.locator("tagName").first();

  // perform action on the element (element must be unique)
  await page.locator("tagName").first().click();

  // locating child elements (there are multiple ways to do this)
  // separate selector string by space
  await page.locator("tagName childTagName").first().click();
  // chain locators
  await page.locator("tagName").first().locator("childTagName").click();
  await page.locator("tagName").first().locator("childTagName").nth(1).click();
  await page.locator("tagName").first().locator("childTagName").last().click();
  await page
    .locator("tagName")
    .first()
    .locator("childTagName")
    .filter({ hasText: "text" })
    .click();
});

// convert selector of multiple elements to array
const elements = await page.locator("tagName").all();
```

## Playwright Native Locators

### User-Facing Locators

Mimic the way users find elements on the page. These are considered best practices for selecting elements.

- [page.getByRole](https://playwright.dev/docs/api/class-page#page-get-by-role),
- [page.getByLabel](https://playwright.dev/docs/api/class-page#page-get-by-label),
- [page.getByPlaceholder](https://playwright.dev/docs/api/class-page#page-get-by-placeholder),
- [page.getByText](https://playwright.dev/docs/api/class-page#page-get-by-text),
- [page.getByTitle](https://playwright.dev/docs/api/class-page#page-get-by-title),

### Non User-Facing Locators

- [page.getByTestId](https://playwright.dev/docs/api/class-page#page-get-by-test-id),
  uses `data-testid` attribute (can be configured to be different)

It is also good strategy to combine page.locator with user-facing locators for more complex situations.

## Assertions

```typescript
import { test, expect } from "@playwright/test";

test("test name", async ({ page }) => {
  // General Assertions
  const value = 5;
  expect(value).toBe(5);

  // Locator Assertions
  const locator = page.locator("tagName");
  await expect(locator).toHaveText("text");

  // Soft Assertions
  // It will just log the error and continue with the test
  const softValue = 5;
  expect.soft(softValue).toBe(5);
});
```

## Auto-Waiting

Some locator methods in playwright have built-in auto-waiting capabilities.

[Auto-Waiting](https://playwright.dev/docs/actionability)

If you are working with methods that do not have auto-waiting capabilities, you can use the following methods to wait for the element to be ready before proceeding with your test.

- [locator.waitFor](https://playwright.dev/docs/api/class-locator#locator-wait-for)
- page.waitForSelector(selector, options)
- page.waitForResponse

default waiting time can be configured.

Assertions have a different waiting time (default 5 seconds).

### Timeouts

1. **Global Timeout**
   - Time limit of the whole test run (ALL tests).
   - Unset by default.
2. **Test Timeout**
   - Time limit for single test.
   - default: 30 seconds
3. **Action Timeout**
   - Time limit for single action (e.g. click, fill, etc.).
   - default: no timeout (wait forever until test timeout is reached)
4. **Navigation Timeout**
   - Time limit for navigation actions (e.g. page.goto, page.waitForNavigation, etc.).
   - default: no timeout (wait forever until test timeout is reached)
5. **Assertion Timeout**
   - Time limit for expect locator assertions (e.g. expect(locator).toHaveText("text")).
   - default: 5 seconds

### Configuring Timeouts

- `playwright.config.ts`
  - `timeout`: config test timeout
  - `globalTimeout`: config global timeout
  - `use`
    - `actionTimeout`: config action timeout
    - `navigationTimeout`: config navigation timeout
  - `expect`
    - `timeout`: config locator assertion timeout
- override global config for specific instances
  - test.slow()
  - test.setTimeout(1000)
  - locator.click({ timeout: 1000 })
  - set testInfo object in beforeEach hook

## Page Object Model

Design patter used in test automation.

Core concept: every page of the application is represented by a class with methods for interacting with that page.

It’s still a good idea to give some components their own classes — like the nav menu, header, and footer.

Principles to follow:

- DRY: Don't Repeat Yourself
- KISS : Keep It Simple, Stupid (prioritize readability and maintainability)
- Descriptive naming
- Avoid "tiny" methods (e.g. "clickSubmitButton")

put these classes in a separate folder (e.g. `page-objects`)

Playwright suggests to separate locators from methods (don't put locators in the methods), and store them as class properties (fields).

## Best Practices

[Best Practices](https://playwright.dev/docs/best-practices)
