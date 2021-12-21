---
description: Send and receive remote console commands via RCON.
---

# RCON

## Overview

RCON allows you to send and receive console commands by interfacing with the server over a remote connection. RCON is secured using a password and a port (typically changed from the default `25575`). RCON is dangerous because it allows you to execute commands with unrestricted privilege, such as if you were an operator on the server.

## Workflow

1. `const client = new util.RCON();`
2. `await client.connect(host, port);`
3. `await client.login('mypassword');`
4. `await client.run('time query daytime');`
5. _Wait for a response from the server_
6. `await client.close()`

## Examples

### Multiple Responses

```javascript
const util = require('minecraft-server-util');

const client = new util.RCON();

client.on('message', async (data) => {
    console.log(data);

    // Close the client whenever necessary. Make sure
    // that all responses have been read from the server
    // before closing to ensure they fire this event.
    await client.close();
});

const connectOpts = {
    timeout: 1000 * 5
    // ... any other connection options specified by
    // NetConnectOpts in the built-in `net` Node.js module
};

const loginOpts = {
    timeout: 1000 * 5
};

(async () => {
    await client.connect('localhost', 25575, connectOpts);
    await client.login('mypassword', loginOpts);
    await client.run('time query daytime');
})();
```

```javascript
{ requestID: 1, message: 'The time is 4853' }
```

### Single Response

```javascript
const util = require('minecraft-server-util');

const client = new util.RCON();

const connectOpts = {
    timeout: 1000 * 5
    // ... any other connection options specified by
    // NetConnectOpts in the built-in `net` Node.js module
};

const loginOpts = {
    timeout: 1000 * 5
};

(async () => {
    await client.connect('localhost', 25575, connectOpts);
    await client.login('mypassword', loginOpts);
    
    const message = await client.execute('time query daytime');
    console.log(message);
    
    await client.close();
})();
```

```javascript
'The time is 4853'
```

## Methods

### `new util.RCON()`

This method creates a new RCON client and returns its class. You will need to connect and login before you can start running commands.

```javascript
const util = require('minecraft-server-util');

const client = new util.RCON();

// Connect
// Login
// Run command
```

### `client.connect()`

Connects to the specified server using the host and port provided in the arguments.

```javascript
const options = {
    timeout: 1000 * 5
    // ... any other connection options specified by
    // NetConnectOpts in the built-in `net` Node.js module
};

await client.connect('localhost', 25575, options);
```

### `client.login()`

Logs into the server by using the password specified by the server. You will need to call `client.connect()` and wait for it to resolve before trying to log in.

```javascript
await client.login('mypassword');
```

### `client.run()`

This method will execute the command on the server and return without waiting for a response. This is typically used if the server sends more than one response for the specified command you are trying to run. You will need to connect then login before trying to run any commands. The return value is the request ID, an incremented counter for identifying what responses from the server are associated with the command request. You can use this request ID to identify what messages returning from the server are a response to this command.

```javascript
const requestID = await client.run('time query daytime');
```

### `client.execute()`

This method is the same as `client.run()`, except it will wait to return until it receives a message from the server about the output from the command. If the command you are running outputs more than one message, or you are missing some of the output, please use `client.run()` instead and use the client events to read all the messages.

```javascript
const message = await client.execute('time query daytime');

console.log(message);
```

```javascript
'The time is 4853'
```

### `client.close()`

This will close the connection to the server. Make sure that you wait until you receive a response from the server for any queued executed commands before closing, as you will not receive them if closed before receiving the response.

```javascript
await client.close();

```

## Events

### `client.on('message')`

This event is emitted whenever there is a message returned from the server after executing an RCON command. A single command may output multiple messages depending on the plugin or command used, so the first message received may not be the entire output.

```javascript
client.on('message', (message) => {
    console.log(message);
});
```

```javascript
{
    requestID: 1,
    message: 'Hello, world!' // the output of the command
}
```

