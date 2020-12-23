# Server concepts

## High Level

### What is the server's purpose?

It is important to think about what the server's expect function is from a broad view. Let's ignore the how for now and only consider the what.

- The server's task is to send and receive data from a client
- Provide data that is relevant to the request
- Handle all the routes that are expected or redirect the client otherwise

### What protocol are we using?

Depending on the protocol the methods by which we communicate with the server may be different. It is just a set of rules that we have to follow to ensure proper interaction between the client and the server.
Most commonly http and https, which is a textual protocol. Though it may be cryptic, it is readable.

### How does it all work?

Servers can accomplish very complex task but in principle the main steps are few and pretty simple.

- Someone/something needs some data from a source
- The source has defined a set of demands ( GET, POST, PUT, ...) that it's willing to accept.
- By putting together the type of http verb, the path and sometimes some parameters, the server can know what the client is asking for.
  -- The client targets a specific route, giving all expect parameters using the right actions
  -- The server receives that request gets all the pertinent data and sends it back to the client
  [URL](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_URL), [HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview), [What is a Server](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_web_server)

### Abstracting specific implementation of the server

Thinking of the server as a a large conditional statement can be helpful. Frameworks may abstract this away, by the use of different methods for all the functionality. But we can think of it as a set of **if else** statements for the routes and actions that we want to create.
The routes handled are: - **GET** and **POST** to '/classes/messages' - **GET** and **POST** to '/classes/users'

- An **action** that asks the **server** for some data
  - **GET** 'localhost:3000/classes/messages"
    - get me the messages from classes
    - the server will send back data to the client containing the messages
- An **action** that asks to save a message in the **server**
  - **POST** "localhost:3000/classes/messages"
    - save this message in the database
    - but what message? this is where request bodies or parameters come into play
    - the server may send some data back or not
- An **action** that asks for data from a different route
  - **GET** 'localhost:3000/about'
    - will return a **404** status because we're not handling such route in our server

### http.createServer or express()

There seems to be more work to do when using **createServer** instead of using **express**, but the principles are the same.
For the first, we invoke the method and pass a callback where we define all the logic for our server. In the second, there's a lot of abstraction taking the steps behind the scenes. It still comes down to handle all the possible routes that a client may use.

- createServer callback

  - each **path** ('/', '/classes/messages') gets an if block
    - each **action** for that path gets another conditional
    - if some data needs to be taken out of the request this is where it happens. **request.on('data')** which takes its own callback. Once all the work is done extracting the data and retrieving/saving information from/to a database
    - We send the response back, making sure to include status code, headers and data. **res.end()** closes the connection.
    - Any new request triggers the callback function we defined in **createServer** and the process starts again.

- const app = express()
  - doesn't take a callback inside the parenthesis
    - we use middleware to extract params and the data from the request with module like `body-parser`.
    - instead we have methods to invoke **app.get()**
    - we are no longer using conditionals for the routes but it is the same principle.
    - we give **.get()** a **path** as a first argument and a callback to trigger when a request comes to it
    - the callback will also have a **req** and **res** and we define what needs to be done in the server inside that function.
    - we use the data in **request.body** given to use by the middleware. Do any task needed, saving to a database for examples.
    - we close the connection by using **res.end()** or **res.send()**
