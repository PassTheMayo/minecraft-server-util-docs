---
description: Miscellaneous but useful methods and functions.
---

# Miscellaneous

## Methods

### `parseAddress()`

This method will parse the host and port out of an address string. For example, parsing `play.hypixel.net` will return `{ host: 'play.hypixel.net', port: 25565 }`. The default port is configurable by the second parameter, which may be adjusted if parsing the address for anything other than a Java Edition Minecraft server.

```javascript
const util = require('minecraft-server-util');

const defaultPort = 25565;

// defaultPort is an optional parameter and defaults to 25565 for Java
// Edition Minecraft servers.
const result = util.parseAddress('play.hypixel.net', defaultPort);

console.log(result);
```

```json
{
    "host": "play.hypixel.net",
    "port": 25565
}
```
