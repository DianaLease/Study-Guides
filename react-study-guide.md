# React

## Props

In dumb components, they are passed in from another components where rendered `<DumbComp handleChange={this.handleChange} />`. The dumb component would be defined with props as parameter `function DumbComp(props {})`

In class components, they are passed in from another components where rendered (same as dumb) `<ClassComp handleChange={this.handleChange} />`. However, you access them inside the class component through `this.props`. In this example, the class component would have access to `this.props.handleChange`.

## Creating state

Inside constructor function, after invoking `super()`, assign local state by doing `this.state = {stateKey: initialStateValue};`

Mutate local state by using setState, for example:
`this.setState({stateKey: differentValue})`, usually done in an eventHandler or other component method

## JSX

All JSX in an return statement, must be wrapped in a single element (such as a `<div>`)

For example...

```js
// do this

return(
  <div>
    <div>
      <p>paragraph</p>
    </div>
    <div>
      <p>paragraph</p>
    </div>
  </div>
)

// NOT this

return(
  <div>
    <p>paragraph</p>
  </div>
  <div>
    <p>paragraph</p>
  </div>
)
```

Use conditional rendering if you only want to render something when that data exists or meets a certain condition that the specs specify. Use the `&&` operator. If the condition to the left of the `&&` is not met, the JSX to the right will not render.

For example...

```js

function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}
```

When iterating over items to render, use the `map` array method.
When mapping over items, make sure to give that element a unique key (such as `{item.id}`).

## Forms

How to get a value from a field (i.e. input, textarea, select): `event.target.value` for a single field. If in a form using `onSubmit` with multiple fields, the target would be the form itself, so chain `event.target.fieldName`

In in the example below, `handleSubmit` would be defined as a method on the component and bound in the constructor.

```js
<form onSubmit={this.handleSubmit}>
  <input name="title">
  </input>
  <input name="content">
  </input>
</form>

//access by doing...
event.target.title.value
event.target.content.value
```

You can use `event.target.value` to capture the value of an event (ex. input, textarea, select), and use it in an event handler to mutate state via `setState`.

```js
// in the component where defining component's method
 previewPet(event) {
    this.setState({
      petToPreview: this.props.pets.find((pet) => pet.name === event.target.value
      )
    })
  }

// in the render()
<select onChange={this.previewPet}>
  {this.state.pets.map((pet) => {
    return (
      <option key={pet.name} value={pet.name}>{pet.name}</option>
    )
  })}
</select>
```


