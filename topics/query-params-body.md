---
title: Query, Params and Body
parent: topics
# nav_exclude: true
---

# Query, Params and Body

## Accessing data in the controllers

### Query Strings

URL containing query strings like http://localhost:8000/products?count=10&page=1

- All the '=' separated strings following the question mark
- Will be found in the query object present in the request

```javascript
  // In the controller
  console.log(req.query);

  // logs
  {
    count: '10',
    page: '1'
  }
```

### URL Params

Routes containing URL parameters like http://localhost:8000/products/1

- The last part of path is dynamic, different depending on the product requested
- To make our route handle all possible values for it we can capture it using a parameter
- The incoming value will be paired with the parameter name in our route handler

```javascript
app.get('/prducts/:id/', (req, res) => {
  console.log(req.params); // logs {id: 1}

  const id = req.params.id;
});
```

### Body

Request sending data as an object can be accessed in the body

- Unlike params and query, for the body property to exist in the request will require the use of a middleware like `body-parser`
- Using the middleware before the routes will include the incoming data as values in the body object.

```javascript
// client request
axios.post('/products/review', {
  id: 1,
  title: 'Great Shoes',
  text: 'So comfy I wear them in bed',
});

// server app
app.use(bodyParser.json());

app.post('/products/review', (req, res) => {
  const { id, title, text } = req.body; // destructuring the values

  console.log(text); // logs: So comfy I wear them in bed
});
```
