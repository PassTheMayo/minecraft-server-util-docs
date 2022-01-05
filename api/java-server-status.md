---
description: Retrieve the status of a Java Edition Minecraft server.
---

# Java Server Status

## Overview

The methods documented below are used for different versions of Minecraft servers. The protocol that Minecraft uses has changed a lot over the years, meaning the data sent back and forth has changed for the different versions of Minecraft. The table below contains the information you need to choose which method is right depending on the server you are retrieving the status of.

## Protocol Methods

| Minecraft Version | status()             | statusLegacy()              |
| ----------------- | -------------------- | --------------------------- |
| 1.7.2 - Latest    | :white\_check\_mark: | :white\_check\_mark: (\*)   |
| 1.6.1 - 1.6.4     | :x:                  | :white\_check\_mark: (\*)   |
| 1.4.2 - 1.5.2     | :x:                  | :white\_check\_mark: (\*)   |
| Beta 1.8 - 1.3.2  | :x:                  | :white\_check\_mark: (\*\*) |

**(\*)** Favicon and sample players are not available for this protocol method and version.

**(\*\*)** Favicon, sample players, and version information are not available for this protocol method and version.

## Methods

### `status()`

This method is used for retrieving the status of any Java Edition Minecraft server above and including 1.7.2. It will return basic information such as players online, max players, MOTD, favicon, version, etc.

```javascript
const util = require('minecraft-server-util');

const options = {
    timeout: 1000 * 5, // timeout in milliseconds
    enableSRV: true // SRV record lookup
};

// The port and options arguments are optional, the
// port will default to 25565 and the options will
// use the default options.
util.status('play.hypixel.net', 25565, options)
    .then((result) => console.log(result))
    .catch((error) => console.error(error));
```

```json
{
        "version": {
                "name": "Requires MC 1.8 / 1.17",
                "protocol": 47
        },
        "players": {
                "online": 56196,
                "max": 200000,
                "sample": []
        },
        "motd": {
                "raw": "§f             §aHypixel Network  §c[1.8-1.17]\n                 §c§lBLACK FRIDAY SALE",
                "clean": "             Hypixel Network  [1.8-1.17]\n                 BLACK FRIDAY SALE",
                "html": "<span><span style=\"color: #FFFFFF;\">             </span><span style=\"color: #55FF55;\">Hypixel Network  </span><span style=\"color: #FF5555;\">[1.8-1.17]\n                 </span><span style=\"color: #FF5555; font-weight: bold;\">BLACK FRIDAY SALE</span></span>"
        },
        "favicon": "data:image/png;base64,...",
        "srvRecord": { "host": "...", "port": 25565 }
}
```

### ~~`statusFE01FA()`~~ **DEPRECATED**

This method is used for retrieving the status of any Java Edition Minecraft server between versions 1.6.1 and 1.6.4. It will return basic information such as players online, max players, MOTD, favicon, version, etc. This method is deprecated in favor of `statusLegacy()` which provides status support for all legacy Minecraft servers.

```javascript
const util = require('minecraft-server-util');

const options = {
    timeout: 1000 * 5, // timeout in milliseconds
    enableSRV: true // SRV record lookup
};

// The port and options arguments are optional, the
// port will default to 25565 and the options will
// use the default options.
util.statusFE01FA('localhost', 25565, options)
    .then((result) => console.log(result))
    .catch((error) => console.error(error));
```

```json
{
        "protocolVersion": 78,
        "version": "1.6.4",
        "players": {
                "online": 0,
                "max": 20
        },
        "motd": {
                "raw": "§fA Minecraft Server",
                "clean": "A Minecraft Server",
                "html": "<span><span style=\"color: #FFFFFF;\">A Minecraft Server</span></span>"
        },
        "srvRecord": { "host": "...", "port": 25565 }
}
```

### ~~`statusFE01()`~~ **DEPRECATED**

This method is used for retrieving the status of any Java Edition Minecraft server from version 1.4.2. It will return basic information such as players online, max players, MOTD, favicon, version, etc. This method is deprecated in favor of `statusLegacy()` which provides status support for all legacy Minecraft servers.

```javascript
const util = require('minecraft-server-util');

const options = {
    timeout: 1000 * 5, // timeout in milliseconds
    enableSRV: true // SRV record lookup
};

// The port and options arguments are optional, the
// port will default to 25565 and the options will
// use the default options.
util.statusFE01('localhost', 25565, options)
    .then((result) => console.log(result))
    .catch((error) => console.error(error));
```

```json
{
        "protocolVersion": 78,
        "version": "1.6.4",
        "players": {
                "online": 0,
                "max": 20
        },
        "motd": {
                "raw": "§fA Minecraft Server",
                "clean": "A Minecraft Server",
                "html": "<span><span style=\"color: #FFFFFF;\">A Minecraft Server</span></span>"
        },
        "srvRecord": { "host": "...", "port": 25565 }
}
```

### ~~`statusFE()`~~ **DEPRECATED**

This method is used for retrieving the status of any Java Edition Minecraft server from versions beta 1.8 to 1.6.4. It will only return basic information about the server like players online, max players, version, etc. This method is deprecated in favor of `statusLegacy()` which provides status support for all legacy Minecraft servers.

```javascript
const util = require('minecraft-server-util');

const options = {
    timeout: 1000 * 5, // timeout in milliseconds
    enableSRV: true // SRV record lookup
};

// The port and options arguments are optional, the
// port will default to 25565 and the options will
// use the default options.
util.statusFE('localhost', 25565, options)
    .then((result) => console.log(result))
    .catch((error) => console.error(error));
```

```json
{
        "players": {
                "online": 0,
                "max": 20
        },
        "motd": "A Minecraft Server",
        "srvRecord": { "host": "...", "port": 25565 }
}
```

### `statusLegacy()`

This method allows pinging of all Java Edition Minecraft servers. The response is consistent through all versions except for 1.3.2 and any previous version, in which the version property will be `null`. This method is encouraged over any other legacy status method and the other methods will be removed in the next major release. **Please note** that this method does not support returning a favicon since this is a legacy protocol.

```javascript
const util = require('minecraft-server-util');

const options = {
    timeout: 1000 * 5, // timeout in milliseconds
    enableSRV: true // SRV record lookup
};

// The port and options arguments are optional, the
// port will default to 25565 and the options will
// use the default options.
util.statusLegacy('localhost', 25565, options)
    .then((result) => console.log(result))
    .catch((error) => console.error(error));
```

```json
{
        "version": {
                "name": "1.6.4",
                "protocol": 78
        },
        "players": {
                "online": 0,
                "max": 20
        },
        "motd": {
                "raw": "§fA Minecraft Server",
                "clean": "A Minecraft Server",
                "html": "<span><span style=\"color: #FFFFFF;\">A Minecraft Server</span></span>"
        },
        "srvRecord": null
}
```
