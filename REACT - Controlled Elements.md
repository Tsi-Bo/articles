# REACT CONTROLLED ELEMENTS, BASICALLY

Learning React isn't an easy and straightforward process. During my journey of self-learning web development I compiled notes from personal research, online courses, and tutorials, as well as engaged in discussions with industry experts. I distilled down this knowledge into manageable chunks of information.

In this article we uncover and explain the secret technique of **controlled elements**.

## THE SECRET TECHNIQUE

When we use React, or more specifically JSX, things can get blurry between who “controls” the DOM. Is it React ? Is it the browser ? And this (_generally_) we don’t want ! All component control must (_generally_) be placed in the hands of the lord of UI rendering : React. This is a fundamental notion to understand while learning React.

“Controlled components" or "controlled elements" refer to form elements whose value is controlled by React state. This means that the value of the form element (like an input field or a textarea) is stored in the component's state, and any changes to the value are handled by updating the state.

## IT'S LIKE A CAR, KIND OF...

I understand that the concept can be hard to grasp at first. It took some time before I understood what happened and why it was so important. So let’s use a simple analogy.

Imagine you have a small remote-controlled car. The car represents the form input element, and the remote control represents React state and event handlers.

**In an uncontrolled component:**

- You give the car a push and let it move freely without any control. The car's movement isn't managed or controlled by anything external.
- Similarly, in an uncontrolled component, the input value isn't managed by React state. It can change freely without any synchronization with the component's state.

**In a controlled component:**

- You hold the remote control and use it to steer the car. Every movement of the car is controlled by you through the remote control.
- Likewise, in a controlled component, the input value is controlled by React state. Any change in the input value is controlled and synchronized with the component's state.

In the uncontrolled component, the input value behaves like a free-moving car, changing without any external control. In contrast, the controlled component resembles a remote-controlled car, where every movement is controlled and synchronized with the remote (React state).

## HOW DOES IT WORK, BASICALY?

The technique of controlled components involves setting the value of the form element explicitly through props, and then providing an `onChange` event handler to update the state whenever the value of the form element changes.

```jsx
import React, { useState } from "react";

function MyForm() {
  const [inputValue, setInputValue] = useState("");

  const handleChange = (event) => {
    setInputValue(event.target.value);
  };

  return (
    <div>
      <label>
        Name:
        <input
          type="text"
          value={inputValue} // This value is controlled by React state
          onChange={handleChange} // We update state on change here
        />
      </label>
      <p>You typed: {inputValue}</p>
    </div>
  );
}

export default MyForm;
```

**Let's dive into this example:**

- We have an input field whose value is controlled by the `inputValue` state variable.
- The `value` attribute of the input element is set to `{inputValue}`, so it always reflects the current state.
- The `onChange` event handler, `handleChange`, updates the `inputValue` state whenever the input field changes.
- As a result, the input field's value is controlled by React. Any changes to the input field will trigger a state update, and the component will re-render with the updated value.

If you want to take things further you can use [React dev tools here](https://react.dev/learn/react-developer-tools).

- Open your browsers dev tools >> React Components.
- Check the MyForm component and you should find the different state hooks attached to it. (This is, in part, why we call them hooks btw).
- As soon as you type in your input field, the state will automatically change. React will ‘react’ to the changes made in the input field.

## SO… WHY DO WE DO THIS?

Controlled components are useful for several reasons:

**One ring to rule them all**

With controlled components, the React state becomes the one and only source of truth for values in form elements. This means that the state holds the current value of the input, making it easier to change/synchronize with other parts of our applications.

Keep in mind this principle can, of course, be overruled if necessary.

**Predictable Behavior**

Since the value of the form element is controlled by React state, we have full control over its behavior (which makes debugging and testing more easy). This allows us to enforce validation rules, perform conditional rendering based on the input value, or implement JS logic quickly.

**Productivity**

Controlled components typically provide better developer productivity due to their centralized logic. This can outweigh any potential minor performance differences in many cases, as the benefits of maintainability and predictability are often more significant in the long term.

## BUT, THIBAULT, IS IT REALLY ALL THAT GREAT?

Well, not really. If React isn’t here to control the inputs, the browser will do its job.

First thing obvious which comes to mind is : a state re-rendering every time you type a character in an input field doesn’t seem like the most performance-friendly idea.

As [@ilyamkin](https://twitter.com/ilyamkin?lang=fr) pointed out in his quick [read here](https://hackernoon.com/you-might-not-need-controlled-components-fy1g360o) , you don’t need to use controlled inputs all the time. When using large forms, a certain delay can be experienced.

Still, I believe there are too many good reasons to use controlled components. My advice would be to use them, and when necessary (for performance or reliability issues for ex.) to rely on uncontrolled components. There can even be a mixture of both !

The important thing now is that we know what’s the difference between a controlled and uncontrolled component, why they exist and how to use them.
