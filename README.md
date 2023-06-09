Following are few examples of methods supported by [React Testing Library(RTL)](https://testing-library.com/docs/react-testing-library/intro/) for easy access.

## Table of Contents

- [Fetch elements by](#fetch-elements-by)
   - [aria-label](#aria-label)
   - [input placeholder](#input-placeholder)
   - [role](#role)
   - [test id](#test-id)
   - [id](#id)
   - [class name](#class-name)
   - [text](#text)
- [Fire click event on an element](#fire-click-event-on-an-element)
- [Fire change event on an input field](#fire-change-event-on-an-input-field)
- [Fire key press event](#fire-key-press-event)
- [Wait for expectation to pass](#wait-for-expectation-to-pass)
- [Using debug method](#using-debug-method)
- [Debug Print Limit](#debug-print-limit)

## Fetch elements by

### aria-label

Source code

```html
<input aria-label="givenName">
```

Test code

```html
const wrapper = render(
    <DOMElement
    data={{id: "123"}}
    />);

const givenName = wrapper.getByLabelText("givenName");
```

### input placeholder

Source code

```html
<input placeholder="Enter user name">
```

Test code

```html
const wrapper = render(
    <DOMElement
    data={{id: "123"}}
    />);

const givenName = wrapper.getByPlaceholderText("Enter user name");
```

### role

Source code

```html
<Spinner role="status" />
```

Test code

```html
const wrapper = render(
    <DOMElement
    data={{id: "123"}}
    />);

const spinnerDisplay = wrapper.getByRole("status");
```
NOTE: It is recommended to use valid roles with non-abstract ARIA role.

### test id

Source code

```html
<button data-testId="buttonTest">Click Me!</button>
```

Test code

```html
const wrapper = render(
    <DOMElement
    data={{id: "123"}}
    />);

const buttonElement = wrapper.getByTestId("buttonTest");
```
NOTE: It is recommended to avoid relying too heavily on implementation details like specific `data-testid` attributes. Instead, it's best to utilize available attributes and search methods that reflect how users interact with the application.

### id

Source code

```html
<button id="clickButton">Click</button>
```

Test code

```html
const wrapper = render(
    <DOMElement
    data={{id: "123"}}
    />);

const buttonElement = wrapper.container.querySelector("#clickButton");
```

### class name

Source code

```html
<a class="text-info">Home</a>
<a class="text-info">About</a>
<a class="text-info">Contact</a>
```

Test code

```html
const { container } = render(
    <DOMElement
    data={{id: "123"}}
    />);

expect(container.getElementsByClassName("text-info").length).toBe(3);
```

### text

Source code

```html
<button>Connect with us</button>
```

Test code

```html
const wrapper = render(
    <DOMElement
    data={{id: "123"}}
    />);

const elementFull = wrapper.getByText("Connect with us");
const elementIgnoreCase = wrapper.getByText("connect with us", {exact: false});
const elementSubstring = wrapper.getByText("with us", {exact: false});
```

Assertion

```html
expect(wrapper.container.textContent).toMatch("Hello World");
```


## Fire click event on an element

```html
render(<DOMElement data={{id: "123"}}/>);

<!-- Fire click event on an element containing a rendered text "Submit" -->
fireEvent.click(screen.getByText("Submit"));
```

OR

```html
const wrapper = render(
    <DOMElement
    data={{id: "123"}}
    />);

<!-- Fetch DOM element -->
const buttonElement = wrapper.getByText("Submit");
<!-- Fire click event on the element -->
fireEvent.click(buttonElement);

```

## Fire change event on an input field

```html
const wrapper = render(
    <DOMElement
    data={{id: "123"}}
    />);

<!-- Fetch the input field by label text -->
const givenName = wrapper.getByLabelText("givenName");
<!-- Fire change event on the above field -->
fireEvent.change(givenName, { target: { value: "testValue" } });
<!-- Assert the value entered in DOM -->
expect(givenName.value).toBe("testValue");
```

## Fire key press event

```html
const wrapper = render(
    <DOMElement
    data={{id: "123"}}
    />);

<!-- Fetch the input field by placeholder text -->
const passwordField = wrapper.getByPlaceholderText("Enter password");
<!-- Fire change event on the above field -->
fireEvent.change(passwordField, { target: { value: "Test@123" } });
<!-- Fire key press event of "Enter" key -->
fireEvent.keyPress(passwordField, { key: "Enter", code: 13, charCode: 13 });
<!-- Similar with keyUp, keyDown -->
```

## Wait for expectation to pass

```html
await waitFor(() => expect(wrapper.container.textContent).toMatch("Click Me"));
```
The default timeout is 1000ms.

The examples provided offer a glimpse into a few methods. For a deeper dive into the library, please explore the following official link, which provides additional details: [react-testing-library/cheatsheet](https://testing-library.com/docs/react-testing-library/cheatsheet/)

## Using debug method

```html
import { render, screen } from "@testing-library/react";

const wrapper = render(<DOMElement
    data={{id: "123"}}
    />);
screen.debug();
```
### Debug Print Limit
Debug statements have a print limit of 7000 by default, you will see `...` in the console, when the DOM content is stripped off. To print more content when the DOM size is really large:

In MAC/Linux:
```html
DEBUG_PRINT_LIMIT=10000 npm test
```

In Windows:

Install cross-env 
```html
npm install --save-dev cross-env
```

Update the script for test to append 
```html
"scripts": {
  "test": "cross-env DEBUG_PRINT_LIMIT=10000 react-scripts test"
}
```
