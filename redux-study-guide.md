# Redux

In class components, we have access to `componentDidMount()` and `componentWillUnmount()`

In components that are importing the store, you can use `store.subscribe` and `store.unsubscribe`

For example, inside the class component, after you've created your local state inside the constructor with `this.state`...

```js
  // when the component is put onto the DOM
  componentDidMount () {
    // when the redux store state changes
    this.unsubscribe = store.subscribe(() => {
      // also update the local react state
      //here, we are getting `counter` from the store and setting its value to our component's 'value' in its own `this.state`
      this.setState({
        value: store.getState().counter
      });
    });
  }
  componentWillUnmount () {
    // stop listenining
    this.unsubscribe();
  }

```

Create actions (in actions.js) that you can dispatch from your store inside your components (that are importing store)

```js
export const createAnAction = (num) => {
  return {
    type: 'INCREMENT',
    input: num
  }
};
```

The reducer is where you write your switch statements for each action type. Be sure to initialize state according to Tom's First Law.

```js
const initialState = {
  counter: 0
};

export default (state = initialState, action) => {
  // don't mutate original state!
  const newState = Object.assign({}, state)
  switch (action.type) {
    case 'INCREMENT':
       newState.counter += action.input
       return newState
    default:
      return state;
  }
}
```

How to dispatch from store -  Inside your class component, usually inside an event handler or in an anonymous function in a component's onClick, onSubmit (in a form), etc.

```js
  //don't forget to bind any event handlers in constructor (`this.changeHandler = this.changeHandler.bind(this)`)
  //here, we'd also have to imort { createAnAction } from actions.js

  changeHandler() {
    store.dispatch(createAnAction(2));
  }

```
