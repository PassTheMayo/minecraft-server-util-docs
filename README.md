---
description: >-
  A Node.js package for interacting with Java and Bedrock Edition Minecraft
  servers.
---

# 🏠 Home

{% hint style="warning" %}
**Please note!** This library will be deprecated in the near future, meaning that it will no longer be actively maintained or support any future updates. It has been deprecated in favor of my other service, [mcstatus.io](https://mcstatus.io/), which is an online API for retrieving the status of any Minecraft server. This service has greatly improved reliability over this library, and has more features as well.
{% endhint %}

## Overview

The goal of this package is to make it easier for developers to interact with Minecraft servers, such as retrieving their status, sending a Votifier vote, executing RCON commands, etc. The API is clear and easy to understand, making it simple for inexperienced developers to do even the simplest tasks.

## Features

* Retrieve the status of Java Edition servers
  * Support for all Minecraft servers
* Retrieve the status of Bedrock Edition servers
* Query a Minecraft server for more information
  * Basic and full query support
* Execute remote console commands with RCON
* Send a Votifier vote

## Installation

Installing this package requires that both [Node.js](https://nodejs.org/) and [npm](https://www.npmjs.com/) are installed. npm is required to be located within the `PATH` variable in order for the installation command to work. Simply run the below command within your project's root directory and ensure a `package.json` file exists by using `npm init` beforehand.

```shell
npm install minecraft-server-util
```

## TypeScript Support

This module is written purely in TypeScript, but is compiled to JavaScript as a CommonJS module. In previous versions, you could simply import by using the following code:

```typescript
// INCORRECT!!!
import util from 'minecraft-server-util';
```

... but with the recent `v5.0.0` release, the import syntax has changed. You can import the method you need directly from the module or import everything:

```typescript
import * as util from 'minecraft-server-util';

// or

import { status } from 'minecraft-server-util';
```

## Bug Reports

You can report bugs by [opening a new issue](https://github.com/PassTheMayo/minecraft-server-util/issues/new/choose) on GitHub. Make sure to include as much detail as possible to get the issue resolved in the least amount of time. I will try to get the bug resolved as soon as I can, but just remember that I have responsibilities outside of sitting at my computer 24/7.

## Discord Server

There is a public Discord server for users of this library. You can report bugs, suggest features, and give feedback on the library here. Make sure to read the rules before chatting to avoid any unnecessary staff interaction.

[https://discord.gg/e7jgDYY](https://discord.gg/e7jgDYY)
