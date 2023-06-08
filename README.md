# React Testing Library Cheatsheet

Following are few examples of methods supported by [React Testing Library(RTL)](https://testing-library.com/docs/react-testing-library/intro/) for easy access.

## Table of Contents

- [Fetch elements by](#fetch-elements-by)
   - [aria-label](#aria-label)
   - [input placeholder](#input-placeholder)
   - [role](#role)
   - [id](#id)
   - [class name](#class-name)
- [Fire click event on an element](#fire-click-event-on-an-element)
- [Fire change event on an input field](#fire-change-event-on-an-input-field)
- [Fire key press event](#fire-key-press-event)

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

const buttonElement = header.container.querySelector("#clickButton");
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
```

The examples provided offer a glimpse into a few methods. For a more comprehensive understanding of the library, please explore the following official link, which provides additional details: [react-testing-library/cheatsheet](https://testing-library.com/docs/react-testing-library/cheatsheet/)
