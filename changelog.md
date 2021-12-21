---
description: A change log of all releases to the library.
---

# Changelog

## [v5.2.4](https://github.com/PassTheMayo/minecraft-server-util/tree/4a3bef82e40306d998c9b0def9d2631d44ba4829)

Adjusted support for `statusLegacy()` which now allows retrieving the status of all Java Edition Minecraft servers. Please note that this method does not return a favicon, and in some cases neither a version.

## [v5.2.3](https://github.com/PassTheMayo/minecraft-server-util/tree/36d8bce0fc9cc64f172af640d079d5b389c958e0)

This version adds support for the `parseAddress()` method which parses the host and port out of an address string.

## [v5.2.2](https://github.com/PassTheMayo/minecraft-server-util/tree/c367afd5138c006f9a0f697bbe3d4109bdc01dbb)

This version fixes a memory leak issue within the TCP and UDP sockets with the event emitters. It also removes `eventemitter2` as a dependency.

## [v5.2.1](https://github.com/PassTheMayo/minecraft-server-util/tree/a3426c8909bd4fb18ebebaea453e2ebb2a950803)

This version fixes a minor bug in `statusLegacy()` that makes the version property null in most all cases.

## [v5.2.0](https://github.com/PassTheMayo/minecraft-server-util/tree/0f7f2ff7e668a901ff83afb6f32d112e6986095f)

This version adds a new status method called `statusLegacy()` which allows retrieving the status of any legacy Minecraft server (1.6.4 and below). The credit for this implementation is owed to [fabianwennink](https://github.com/fabianwennink/minecraft-server-util/blob/master/src/statusFE01All.ts) for his fork of the repository. All previous legacy status methods have been deprecated in favor of this single uniform status method.

## [v5.1.3](https://github.com/PassTheMayo/minecraft-server-util/tree/6100e720b1501ec2718b04bea3ccc2eb6a1203cd)

This version adds proper timeouts to all methods that utilize sockets to prevent any hanging or never-resolving methods. This also adds an options argument to `RCON#login()` as well as a `client.isConnected` property to the RCON client.

## [v5.1.2](https://github.com/PassTheMayo/minecraft-server-util/tree/3d7d21cef0abe4cb4ce11af9c810abc812c10b8c)

This version adds backwards compatibility support with Node v10 and v12. It fixes some invalid syntax errors when compiling from TypeScript.

## [v5.1.1](https://github.com/PassTheMayo/minecraft-server-util/tree/aa6c23a1b7f785edf120c87f05aa4615dadb3e58)

This version properly adds support for handling a connection timeout when attempting to connect to the server. Keep in mind that the timeout duration specified in the options is only used when connecting, and not for the entire status method.

## [v5.1.0](https://github.com/PassTheMayo/minecraft-server-util/tree/5266fe82e0af840447d8a1b3c4b8b2b9cfeef812)

This version adds support for servers with SRV records. This also introduces a new `enableSRV` option within all status method options object, and a `srvRecord` property within the responses.

## [v5.0.2](https://github.com/PassTheMayo/minecraft-server-util/tree/37690a67f825d56ca69804a49e6e8d1658875158)

This version contains no code changes, but cleans old remaining files from previous versions the `dist` directory.

## [v5.0.1](https://github.com/PassTheMayo/minecraft-server-util/tree/62ef29602e282ae0de0f903535630732a3b415d4)

This version is simply a republish with an updated version and no code changes to fix the README file on the npm page. This likely occurred after GitHub went down for several hours, causing issues on npm's side.

## [v5.0.0](https://github.com/PassTheMayo/minecraft-server-util/tree/9c9ed66aaaece0cf4d76ecb643e8f31bceec4fd1)

The fifth major release of the package rewritten from the ground up with better error handling.
