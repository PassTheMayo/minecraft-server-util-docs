---
description: A list of frequently asked questions and answers about the library.
---

# Frequently Asked Questions

## How do I check if the server is up/down?

Every status method exported from the library returns a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Promise), which means that you need to wait for the data to return from the server before being able to see the response. If this promise successfully resolves, then it means that the server is online and the status was retrieved. If the promise rejects (or errors), then it means the server was offline or there was an error retrieving the status.

```javascript
const util = require('minecraft-server-util');

util.status('play.hypixel.net')
    .then((result) => {
        // Server is online
    })
    .catch((error) => {
        // Server is offline
    });
```

Or using async/await:

```javascript
const util = require('minecraft-server-util');

// Make sure this is within an async context
try {
    const result = await util.status('play.hypixel.net');
    
    // Server is online
} catch (e) {
    // Server is offline
}
```

## How do I use this library in the browser?

This library cannot be used in the browser because TCP and UDP sockets are not supported in the browser environment. You will likely receive an error such as `Cannot find module 'net'` or `Cannot find module 'dgram'` when you attempt to bundle it. Instead, you can create a Node.js server that receives HTTP requests and send the status on the server-side. If you do not want to do this, I would recommend a quick service like [mcsrvstat.us](https://mcsrvstat.us) instead.

## Why am I getting weird values?

All of the data sent back in the server response are provided by the server itself, and the library has no control of incorrect or unexpected data sent by the server. If you believe there is an issue with the library, you can [open a new issue](https://github.com/PassTheMayo/minecraft-server-util/issues/new/choose) on GitHub explaining your findings.

## Why is the sample players array empty?

Most large servers will not send a sample player list within any of the status methods because they do not want to show their player list, or they will send customized text to do cool hover effects on the server listing. If you want a reliable way of getting all the players, use `queryBasic()` or `queryFull()` instead.

## Why am I getting errors and/or unexpected results after updating?

This is because you updated the package to the next major release without checking the change log. Every major release (for example, `v4.5.1` -> `v5.0.0`) contains breaking changes which is not compatible with the last release. You can configure your `package.json` file to strictly use the currently major version to prevent unexpected breaking changes updates.

## What is the `requestID` in RCON messages?

The request ID is the ID of the response from the server. It is the same as the return value from `client.run()` to better identify what responses came from what command. A command may return multiple response messages, so correctly waiting for all messages to come in before closing the client is necessary. The request ID is also used within `client.execute()` to wait for the proper response from the server before returning the message. Note that `client.execute()` will only wait for one message to return before resolving, so commands with multiple responses will not work well with this method.

## How do I send the favicon within a Discord embed?

This question is generally outside the scope of this library, but since it is so frequently asked, I will post an answer here. The following code is written for Discord.js, and you may make adjustments as necessary. You will need to attach the `attachment` to the message whenever you are sending it.

```javascript
const embed = new Discord.MessageEmbed()
	.setThumbnail('attachment://favicon.png')
	// ...

channel.send({
	files: [
		{
			attachment: Buffer.from(result.favicon.split(',')[1], 'base64'),
			name: 'favicon.png'
		}
	],
	embeds: [
		embed
	]
});
```
