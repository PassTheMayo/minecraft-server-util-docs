---
description: Retrieve advanced information about a Java Edition Minecraft server.
---

# Query

## Overview

Query is a new protocol introduced in version 1.9 that allows services such as Minecraft server listings to better retrieve information about servers, including more information than a regular status method would return. It also uses UDP instead of the TCP format which helps separate the main connection protocol and the status retrieval protocol.

## Methods

### `queryBasic()`

This method will return some basic information about the server, but still more than a status method would return. Query has to be enabled on the server for this to work, by setting `enable-query` to `true` in the `server.properties` file.

```javascript
const util = require('minecraft-server-util');

const options = {
    sessionID: 1, // a random 32-bit signed number, optional
    enableSRV: true // SRV record lookup
};

// The port and options arguments are optional, the
// port will default to 25565 and the options will
// use the default options.
util.queryBasic('localhost', 25565, options)
    .then((result) => console.log(result))
    .catch((error) => console.error(error));
```

```json
{
        "motd": {
                "raw": "§fA Minecraft Server",
                "clean": "A Minecraft Server",
                "html": "<span><span style=\"color: #FFFFFF;\">A Minecraft Server</span></span>"
        },
        "gameType": "SMP",
        "map": "world",
        "players": {
                "online": 0,
                "max": 20
        },
        "hostPort": 25565,
        "hostIP": "127.0.0.1",
        "srvRecord": { "host": "...", "port": 25565 }
}
```

### `queryFull()`

This method will return the most information about a Java Edition Minecraft server. Query has to be enabled on the server for this to work, by setting `enable-query` to `true` in the `server.properties` file.

```javascript
const util = require('minecraft-server-util');

const options = {
    sessionID: 1, // a random 32-bit signed number, optional
    enableSRV: true // SRV record lookup
};

// The port and options arguments are optional, the
// port will default to 25565 and the options will
// use the default options.
util.queryFull('localhost', 25565, options)
    .then((result) => console.log(result))
    .catch((error) => console.error(error));
```

```json
{
        "motd": {
                "raw": "§fA Minecraft Server",
                "clean": "A Minecraft Server",
                "html": "<span><span style=\"color: #FFFFFF;\">A Minecraft Server</span></span>"
        },
        "version": "1.17.1",
        "software": "Paper on 1.17.1-R0.1-SNAPSHOT",
        "plugins": [],
        "map": "world",
        "players": {
                "online": 1,
                "max": 20,
                "list": [
                        "PassTheMayo"
                ]
        },
        "hostIP": "127.0.0.1",
        "hostPort": 25565,
        "srvRecord": { "host": "...", "port": 25565 }
}
```
