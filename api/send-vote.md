---
description: Allows you send votes to a server as a player.
---

# Send Vote

## Overview

The method below allows you to send a vote to a server as a player. A server plugin such as [NuVotifier](https://www.spigotmc.org/resources/nuvotifier.13449/) is required in order for it to work. You must also know the token configured in the Votifier plugin configuration for security purposes.

## Methods

### `sendVote()`

This method allows you to send a vote to a server. This method does not support SRV records, so the actual IP address of the server is required. The service name is optional, but it should describe the name of the application that is sending a vote. The player UUID is also optional, but it is strongly recommended to be included. This UUID should include hyphens in standard Mojang UUID format.

```javascript
const util = require('minecraft-server-util');

util.sendVote('localhost', 8192, {
    token: '', // the token configured in the server plugin
    username: 'PassTheMayo',
    serviceName: 'my-application',
    uuid: '85e5f06e-ff89-4c11-8050-329e8fdc29de', // player UUID, recommended but optional
    timestamp: Date.now(), // current time
    timeout: 1000 * 5 // timeout in milliseconds
})
    .catch((error) => console.error(error));
```

The method should return a promise that resolves to undefined if the vote was successful. If the vote was not successful, then the promise will reject.
