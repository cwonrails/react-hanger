# react-hanger

> ⚠️ Warning: hooks are not part of a stable React release yet, so use this library only for experiments

## Install

```bash
yarn add react-hanger
```

## Usage

```jsx
import React, { Component } from "react";

import {
  useInput,
  useBoolean,
  useNumber,
  useArray,
  useOnMount,
  useOnUnmount
} from "react-hanger";

const App = () => {

  const newTodo = useInput("");
  const showCounter = useBoolean(true);
  const limitedNumber = useNumber(3, { lowerLimit: 0, upperLimit: 5 });
  const counter = useNumber(0);
  const todos = useArray(["hi there", "sup", "world"]);

  const rotatingNumber = useNumber(0, {
    lowerLimit: 0,
    upperLimit: 4,
    rotate: true
  });

  useOnMount(() => console.log("hello world"));
  useOnUnmount(() => console.log("goodbye world"));

  return (
    <div>
      <button onClick={showCounter.toggle}> toggle counter </button>
      <button onClick={counter.increase}> increase </button>
      {showCounter.value && <span> {counter.value} </span>}
      <button onClick={counter.decrease}> decrease </button>
      <button onClick={todos.clear}> clear todos </button>
      <input
        type="text"
        value={newTodo.value}
        onChange={newTodo.onChangeHandler}
      />
    </div>
  );
};
```

### Example

[Open in CodeSandbox](https://codesandbox.io/s/44m70xm70)

### useStateful

Just an alternative syntax to `useState`, because it doesn't need array destructuring.  
It returns an object with `value` and a `setValue` method.

```jsx
const username = useStateful("test");

username.setValue("tom");
console.log(username.value);
```

### useOnMount

```jsx
const App = () => {
  useOnMount(() => console.log("hello world"));
  return <div> hello world </div>;
};
```

### useOnUnmount

```jsx
const App = () => {
  useOnUnmount(() => console.log("goodbye world"));
  return <div> goodbye world </div>;
};
```

### useLifecycleHooks

```jsx
const App = () => {
  useLifecycleHooks({
    onMount: () => console.log("mounted!"),
    onUnmount: () => console.log("unmounted!")
  });

  return <div> hello world </div>;
};
```

### useBoolean

```jsx
const showCounter = useBoolean(true);
```

Methods:

- `toggle`
- `setTrue`
- `setFalse`

### useNumber

```jsx
const counter = useNumber(0);
const limitedNumber = useNumber(3, { upperLimit: 5, lowerLimit: 3 });
const rotatingNumber = useNumber(0, {
  upperLimit: 5,
  lowerLimit: 0,
  rotate: true
});
```

Methods:

- `increase`
- `decrease`

Options:

- `lowerLimit`
- `upperLimit`
- `rotate`

### useInput

```jsx
const newTodo = useInput("");
```

```jsx
<input value={newTodo.value} onChange={newTodo.onChangeHandler} />
```

```jsx
<input {...newTodo.bindToInput} />
```

Methods:

- `clear`
- `onChangeHandler`
- `bindToInput`

Properties:

- `hasValue`

### useArray

Methods:

- `add`
- `clear`
- `removeIndex`
- `removeById`
