# react-express-socketio-nocorserror
A boilerplate with an example of react express and socketio without cors error in development mode

## How to run it

Open two terminals

In one just go to backend folder and run
`yarn start`

In the another go to frontend folder and run
`yarn start`

## Why is not giving cors error if server is like the one i have????

Just check the `frontend/src/App.js`, there you can see the line 14 where socketio client is beign loaded in websocket transport mode.

This mode is not being checked by cors, so it will not give the problem.

Notice also that in the server, to make any cors work, is required to add it to express (line 4):
`app.use(cors({origin: null}))`

## So, to be more explicit, it works because

In server you allowed cors from any source:
```
const app = require('express')();
const cors = require('cors');

app.use(cors({origin: null}))
```

And in client, you used the websocket transport when you connect to sockets:
```
import iocli from 'socket.io-client'
socket = iocli('localhost:4000', {transports: ['websocket']})
```
