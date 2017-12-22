WebSocket Client & Server Implementation for Node **For Intrising**
=================================================
For some specific product, we need to use node `v0.6.10` and create a websocket client. Therefore, this project needs to roll back to the relevant version, which is `v1.0.3` to be executable.

However, this version's functionality is not completed... For example, the **PONG** handler in `/lib/WebSocketConnection` will do nothing when receiving pong messages.

To solve the problem, we add the handler and pass the pong frame (`0x0A`) as the normal message frame (`0x01`) and create a new type called `pongMessgae` so that we can receive **PONG** directly.

## Here is how it worked.
start at `/lib/WebSocketConnection.js` line 425.
```js
  var pongMessage = frame.binaryPayload.toString('utf8');
  this.emit('message', {
      type: 'pongMessage',
      utf8Data: pongMessage
  });
```