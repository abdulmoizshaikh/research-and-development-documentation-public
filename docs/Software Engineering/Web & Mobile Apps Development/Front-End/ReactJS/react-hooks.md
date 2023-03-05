# React Hooks

**Call child method from parent**
how to call child function from parent in react

### useImperativeHandle

(use to access child component function in parent component or you can say if we want to call function defined in child component from parent component then we use this useImperativeHandle )

**Modern React with Hooks (v16.8+)**

```jsx showLineNumbers
const { forwardRef, useRef, useImperativeHandle } = React;

// We need to wrap component in `forwardRef` in order to gain
// access to the ref object that is assigned using the `ref` prop.
// This ref is passed as the second parameter to the function component.
const Child = forwardRef((props, ref) => {
  // The component instance will be extended
  // with whatever you return from the callback passed
  // as the second argument
  useImperativeHandle(ref, () => ({
    getAlert() {
      alert("getAlert from Child");
    },
  }));

  return <h1>Hi</h1>;
});

const Parent = () => {
  // In order to gain access to the child component instance,
  // you need to assign it to a `ref`, so we call `useRef()` to get one
  const childRef = useRef();

  return (
    <div>
      <Child ref={childRef} />
      <button onClick={() => childRef.current.getAlert()}>Click</button>
    </div>
  );
};

ReactDOM.render(<Parent />, document.getElementById("root"));
```

https://reactjs.org/docs/hooks-reference.html#useimperativehandle
https://stackoverflow.com/questions/37949981/call-child-method-from-parent
https://stackoverflow.com/questions/60554808/react-useref-with-typescript-and-functional-component

### Hooks

Hooks are a new addition in React 16.8. They let you use state and other React features without writing a class.

🔌 Other Hooks

There are a few less commonly used built-in Hooks that you might find useful. For example, useContext lets you subscribe to React context without introducing nesting:

```jsx showLineNumbers
function Example() {
  const locale = useContext(LocaleContext);
  const theme = useContext(ThemeContext);
  // ...
}
```

And useReducer lets you manage local state of complex components with a reducer:

```jsx showLineNumbers
function Todos() {
const [todos, dispatch] = useReducer(todosReducer);
// ...
```

Tip: Optimizing Performance by Skipping Effects
Tip: Optimizing Performance by Skipping Effects
In some cases, cleaning up or applying the effect after every render might create a performance problem. In class components, we can solve this by writing an extra comparison with prevProps or prevState inside componentDidUpdate:

```js showLineNumbers
componentDidUpdate(prevProps, prevState) {
if (prevState.count !== this.state.count) {
document.title = `You clicked ${this.state.count} times`;
}
}
```

This requirement is common enough that it is built into the useEffect Hook API. You can tell React to skip applying an effect if certain values haven’t changed between re-renders. To do so, pass an array as an optional second argument to useEffect:

```jsx showLineNumbers
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if count changes
```

In the example above, we pass [count] as the second argument. What does this mean? If the count is 5, and then our component re-renders with count still equal to 5, React will compare [5] from the previous render and [5] from the next render. Because all items in the array are the same (5 === 5), React would skip the effect. That’s our optimization.

**Building Your Own Hooks**

Building your own Hooks lets you extract component logic into reusable functions.

When we were learning about using the Effect Hook, we saw this component from a chat application that displays a message indicating whether a friend is online or offline:

```jsx showLineNumbers
import React, { useState, useEffect } from "react";

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return "Loading...";
  }
  return isOnline ? "Online" : "Offline";
}
```

Now that we’ve extracted this logic to a useFriendStatus hook, we can just use it:

```jsx showLineNumbers
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);

  if (isOnline === null) {
    return "Loading...";
  }
  return isOnline ? "Online" : "Offline";
}

function FriendListItem(props) {
  const isOnline = useFriendStatus(props.friend.id);

  return (
    <li style={{ color: isOnline ? "green" : "black" }}>{props.friend.name}</li>
  );
}
```

**USEMEMO (cache)**

We can all agree, **useMemo can be useful to avoid unnecessary re-renders, by keeping the same object reference of a variable**. For the case of using useMemo to cache the actual calculation, where the main goal is not to avoid re-renders in subcomponents: useMemo should be **used when there is a high amount of processing**.23-Jan-2021

### MAIN CONCEPTS

**Props are Read-Only :**

Whether you declare a component as a function or a class, it must never modify its own props. Consider this sum function:

```jsx showLineNumbers
function sum(a, b) {
  return a + b;
}
```

Such functions are called “pure” because they do not attempt to change their inputs, and always return the same result for the same inputs.

In contrast, this function is impure because it changes its own input:

```jsx showLineNumbers
function withdraw(account, amount) {
  account.total -= amount;
}
```

Ref https://reactjs.org/docs/components-and-props.html

**Converting a Function to a Class**

You can convert a function component like Clock to a class in five steps:

1. Create an ES6 class, with the same name, that extends React.Component.
2. Add a single empty method to it called render().
3. Move the body of the function into the render() method.
4. Replace props with this.props in the render() body.
5. Delete the remaining empty function declaration.

```jsx showLineNumbers
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

https://reactjs.org/docs/state-and-lifecycle.html

**Add a class constructor that assigns the initial this.state:**

```jsx showLineNumbers
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

The componentDidMount() method runs after the component output has been rendered to the DOM. This is a good place to set up a timer:

```jsx showLineNumbers

componentDidMount() {
this.timerID = setInterval(
() => this.tick(),
1000
);
}

tick() {
this.setState({
date: new Date()
});
}
```

Note how we save the timer ID right on this (this.timerID).

While this.props is set up by React itself and this.state has a special meaning, you are free to add additional fields to the class manually if you need to store something that doesn’t participate in the data flow (like a timer ID).

We will tear down the timer in the componentWillUnmount() lifecycle method:

```jsx showLineNumbers

componentWillUnmount() {
clearInterval(this.timerID);
}
```

**Do Not Modify State Directly**
For example, this will not re-render a component:

```jsx showLineNumbers
// Wrong
this.state.comment = "Hello";
```

Instead, use setState():

```jsx showLineNumbers
// Correct
this.setState({ comment: "Hello" });
```

The only place where you can assign this.state is the constructor.

**State Updates May Be Asynchronous**

React may batch multiple setState() calls into a single update for performance.

Because this.props and this.state may be updated asynchronously, you should not rely on their values for calculating the next state.

For example, this code may fail to update the counter:

```jsx showLineNumbers
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

To fix it, use a second form of setState() that accepts a function rather than an object. That function will receive the previous state as the first argument, and the props at the time the update is applied as the second argument:

```jsx showLineNumbers
// Correct
this.setState((state, props) => ({
  counter: state.counter + props.increment,
}));
```

We used an arrow function above, but it also works with regular functions:

```jsx showLineNumbers
// Correct
this.setState(function (state, props) {
  return {
    counter: state.counter + props.increment,
  };
});
```

**State Updates are Merged**

When you call setState(), React merges the object you provide into the current state.

For example, your state may contain several independent variables:

```jsx showLineNumbers

constructor(props) {
super(props);
this.state = {
posts: [],
comments: []
};
}

```

Then you can update them independently with separate setState() calls:

```jsx showLineNumbers
componentDidMount() {
fetchPosts().then(response => {
this.setState({
posts: response.posts
});
});

    fetchComments().then(response => {
      this.setState({
        comments: response.comments
      });
    });

}
```

The merging is shallow, so this.setState({comments}) leaves this.state.posts intact, but completely replaces this.state.comments.

https://reactjs.org/docs/state-and-lifecycle.html

**Handling Events**

Handling events with React elements is very similar to handling events on DOM elements. There are some syntax differences:

React events are named using camelCase, rather than lowercase.
With JSX you pass a function as the event handler, rather than a string.
For example, the HTML:

```jsx showLineNumbers
<button onclick="activateLasers()">Activate Lasers</button>
```

is slightly different in React:

```jsx showLineNumbers
<button onClick={activateLasers}>Activate Lasers</button>
```

Another difference is that you cannot return false to prevent default behavior in React. You must call preventDefault explicitly. For example, with plain HTML, to prevent the default form behavior of submitting, you can write:

```jsx showLineNumbers
<form onsubmit="console.log('You clicked submit.'); return false">
  <button type="submit">Submit</button>
</form>
```

In React, this could instead be:

```jsx showLineNumbers
function Form() {
  function handleSubmit(e) {
    e.preventDefault();
    console.log("You clicked submit.");
  }

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">Submit</button>
    </form>
  );
}
```

Here, e is a synthetic event. React defines these synthetic events according to the W3C spec, so you don’t need to worry about cross-browser compatibility. React events do not work exactly the same as native events. See the SyntheticEvent reference guide to learn more.

When using React, you generally don’t need to call addEventListener to add listeners to a DOM element after it is created. Instead, just provide a listener when the element is initially rendered.

https://reactjs.org/docs/handling-events.html

**Conditional-rendering :**

You can use Ternary operator e.g condition? true :false

**Preventing Component from Rendering**

In rare cases you might want a component to hide itself even though it was rendered by another component. To do this return null instead of its render output.

In the example below, the `<WarningBanner />` is rendered depending on the value of the prop called warn. If the value of the prop is false, then the component does not render:

```jsx showLineNumbers
function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }

  return <div className="warning">Warning!</div>;
}
```

https://reactjs.org/docs/conditional-rendering.html

**8. Lists and Keys**

The best way to pick a key is to use a string that uniquely identifies a list item among its siblings. Most often you would use IDs from your data as keys:

```jsx showLineNumbers
const todoItems = todos.map((todo) => <li key={todo.id}>{todo.text}</li>);
```

When you don’t have stable IDs for rendered items, you may use the item index as a key as a last resort:

Keys Must Only Be Unique Among Siblings

**Extracting Components with Keys**

Keys only make sense in the context of the surrounding array.

For example, if you extract a ListItem component, you should keep the key on the `<ListItem />` elements in the array rather than on the `<li>` element in the ListItem itself.

Example: Incorrect Key Usage

```jsx showLineNumbers
function ListItem(props) {
  const value = props.value;
  return (
    // Wrong! There is no need to specify the key here:

    <li key={value.toString()}>{value}</li>
  );
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) => (
    // Wrong! The key should have been specified here:
    <ListItem value={number} />
  ));
  return <ul>{listItems}</ul>;
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById("root")
);
```

Example: Correct Key Usage

```jsx showLineNumbers
function ListItem(props) {
  // Correct! There is no need to specify the key here:
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) => (
    // Correct! Key should be specified inside the array.
    <ListItem key={number.toString()} value={number} />
  ));
  return <ul>{listItems}</ul>;
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById("root")
);
```

https://reactjs.org/docs/lists-and-keys.html

**Controlled Components**

In HTML, form elements such as`<input>`, `<textarea>`, and `<select>` typically maintain their own state and update it based on user input. In React, mutable state is typically kept in the state property of components, and only updated with setState().

We can combine the two by making the React state be the “single source of truth”. Then the React component that renders a form also controls what happens in that form on subsequent user input. `An input form element whose value is controlled by React in this way is called a “controlled component”`.

For example, if we want to make the previous example log the name when it is submitted, we can write the form as a controlled component:

```jsx showLineNumbers
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = { value: "" };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({ value: event.target.value });
  }

  handleSubmit(event) {
    alert("A name was submitted: " + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input
            type="text"
            value={this.state.value}
            onChange={this.handleChange}
          />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

176
This relates to stateful DOM components (form elements) and the React docs explain the difference:

- A [Controlled Component](https://facebook.github.io/react/docs/forms.html#controlled-components) is one that takes its current value through props and notifies changes through callbacks like onChange. A parent component "controls" it by handling the callback and managing its own state and passing the new values as props to the controlled component. You could also call this a "dumb component".
- A [Uncontrolled Component](https://facebook.github.io/react/docs/uncontrolled-components.html) is one that stores its own state internally, and you query the DOM using a ref to find its current value when you need it. This is a bit more like traditional HTML.
  Most native React form components support both controlled and uncontrolled usage:

```jsx showLineNumbers
// Controlled: <input type="text" value={value} onChange={handleChange} /> // Uncontrolled: <input type="text" defaultValue="foo" ref={inputRef} /> // Use `inputRef.current.value` to read the current value of <input>
```

In most (or all) cases you should use controlled components.

https://stackoverflow.com/questions/42522515/what-are-react-controlled-components-and-uncontrolled-components

```jsx showLineNumbers
<textarea value={this.state.value} onChange={this.handleChange} />
```

The select Tag
In HTML,`<select>` creates a drop-down list. For example, this HTML creates a drop-down list of flavors:

```jsx showLineNumbers
<select>
  <option value="grapefruit">Grapefruit</option>
  <option value="lime">Lime</option>
  <option selected value="coconut">
    Coconut
  </option>
  <option value="mango">Mango</option>
</select>
```

**Handling Multiple Inputs**

```jsx showLineNumbers
handleInputChange(event) {
const target = event.target;
const value = target.type === 'checkbox' ? target.checked : target.value;
const name = target.name;

    this.setState({
      [name]: value
    });

}
```

**Fully-Fledged Solutions**

If you’re looking for a complete solution including validation, keeping track of the visited fields, and handling form submission, `Formik` is one of the popular choices. However, it is built on the same principles of controlled components and managing state — so don’t neglect to learn them.

**Formik:** Build forms in React, without the tears

https://formik.org/

https://reactjs.org/docs/forms.html

**Lifting State Up**

As we know that props are read only but we can change the value of prop in child function by passing callback function in child and child will call this fun to change the state of parent function that's how parent and child sync together (like we achieved 2 way data flow this way)

https://reactjs.org/docs/lifting-state-up.html

**Composition vs Inheritance**

React has a powerful composition model, and we recommend using composition instead of inheritance to reuse code between components.

**What is composition in react?**

In React, composition is a natural pattern of the component model. `It's how we build components from other components`, of varying complexity and specialization through props. Depending on how generalized these components are, they can be used in building many other components.

https://reactjs.org/docs/composition-vs-inheritance.html
