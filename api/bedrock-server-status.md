---
description: Retrieve the status of a Bedrock Edition Minecraft server.
---

# Bedrock Server Status

## Overview

There is only one method for retrieving the status of a Bedrock Edition Minecraft server, unlike the many methods used by Java Edition. The documentation below will show you how to use the method, and its return value.

## Methods

### `statusBedrock()`

This will retrieve the status of any version Bedrock Edition Minecraft server.

```javascript
const util = require('minecraft-server-util');

const options = {
    enableSRV: true // SRV record lookup
};

// The port and options arguments are optional, the
// port will default to 19132.
util.statusBedrock('localhost', 19132, options)
    .then((result) => console.log(result))
    .catch((error) => console.error(error));
```

```json
{
        "edition": "MCPE",
        "motd": {
                "raw": "§fDedicated Server\nBedrock level",
                "clean": "Dedicated Server\nBedrock level",
                "html": "<span><span style=\"color: #FFFFFF;\">Dedicated Server\nBedrock level</span></span>"
        },
        "version": {
                "name": "1.17.41",
                "protocol": 471
        },
        "players": {
                "online": 0,
                "max": 10
        },
        "serverGUID": "-7097232759481786137",
        "serverID": "11349511314227765479",
        "gameMode": "Survival",
        "gameModeID": 1,
        "portIPv4": 19132,
        "portIPv6": 19133,
        "srvRecord": { "host": "...", "port": 25565 }
}
```
