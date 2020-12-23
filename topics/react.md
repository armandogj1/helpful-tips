# React 101

### Passing Props

- When rendering a component all values passed to it will be accessible on the props object as properties
- Props should never be mutated, see them as read only values

```javascript
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

```javascript
// Class Component
  class App extends React.Component {
    //.....
    <p> {this.props.hello} </p>
  }

// Functional Component
  const App = (props) => {
    //.....
    <p> {props.hello} </p>
  }
```

- Props can also be destructured, allowing us to use facts without having to type props

```javascript
const Fact = (props) => {
  //..
  <h1>{props.fact.animal}</h1>

const Fact = ({fact, handleFavoriteClick}) => {
  //..
  <h1>{fact.animal}</h1>
```
