---
title: React 101
nav_exclude: true
---

# React 101

### Passing Props

- When rendering a component all values passed to it will be accessible on the props object as properties
- Props should never be mutated, see them as read only values

```jsx
// App.jsx
<FactsList facts={this.state.facts} />

// FactsList.jsx
const FactsList = (props) => {
  return (
    {
      props.facts.map( //....
    }
);
```

- Class and functional components get props but are accessed slightly differently

```jsx
// Class Component
class App extends React.Component {
  //.....
  render() {
    return (
      // We need to use the keyword 'this'
      <p> {this.props.hello} </p>
    );
  }
}

// Functional Component
const App = (props) => {
  //.....
  return (
    // Being a functional component props is an argument passed to it
    <p> {props.hello} </p>
  );
};
```

- Props can also be destructured, allowing us to use facts without having to type props

```jsx
const Fact = (props) => (
  //..
  return (
    // Chaining can get long if props contains lots of nested objects
    <h1>{props.fact.animal}</h1>
  )
);

const Fact = ({ fact, handleFavoriteClick }) => (
  //..
  return (
    // Fact itself could also be destructured
    <h1>{fact.animal}</h1>
  )
);
```

### Rendering Children

- In the return statement we can include JSX tags and other Components, which will be rendered when FactsList is rendered itself.

```jsx
const FactsList = ({ facts, handleClick }) => {
  return (
    <div>
      {/** All siblings need to be wrapped into a single element */}
      <h1>These are FactsLists Children</h1>
      <Fact
        key={facts[0].id} // React wants unique keys for siblings
        fact={facts[0]} // We pass fact located at index 0
        handleFavoriteClick={handleClick} // click handler is shared by all children
      />
      <Fact
        key={facts[1].id}
        fact={facts[1]}
        handleFavoriteClick={handleClick}
      />
      <Fact
        key={facts[2].id}
        fact={facts[2]}
        handleFavoriteClick={handleClick}
      />
    </div>
  );
};
```

- Children can be rendered dynamically
  Doing the former can be repetitive if there are many facts. The number of facts may not always be the three using the map array method can ensure that a component will be generated for each value in the facts array.

```jsx
const FactsList = ({ facts, handleClick }) => {
  return (
    <div>
      {
        // include javascript code inside curly braces
        facts.map((
          curFact,
          idx // the map returns an array of components
        ) => (
          <Fact
            key={idx} // React wants unique keys for siblings, the current index works most cases
            fact={curFact} // We pass the current fact as a prop
            handleFavoriteClick={handleClick} // click handler is shared by all children
          />
        ))
      }
    </div>
  );
};
```
