# UI Components

1. leverage the Codegen tool to generate the code you.
2. Use AI and documentation.
3. DRY

## Input Field

## interactions with input fields

- locator.fill()
- locator.pressSequentially()
- locator.clear()

### assertions on input fields

```javascript
// generic assertions
const inputValue = await locator.inputValue();
expect(inputValue).toBe("expected value");

// locator assertions
assert(locator).toHaveValue(...)
```

## Radio Buttons and Checkboxes

Note: sometimes the native radio button is hidden and replaced with a custom component. in this case, you might need to force the click on the native radio button (personal note... check what the codegen suggests you).

### interactions with radio buttons and checkboxes

- locator.check({force: true})
- locator.uncheck({force: true})

### assertions on radio buttons

```javascript
// generic assertions
const isChecked = await locator.isChecked();
expect(isChecked).toBe(true);

// locator assertions
assert(locator).toBeChecked(true);
```
