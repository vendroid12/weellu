[![npm](https://img.shields.io/npm/v/whatsapp-web.js.svg)](https://www.npmjs.com/package/whatsapp-web.js) [![Depfu](https://badges.depfu.com/badges/4a65a0de96ece65fdf39e294e0c8dcba/overview.svg)](https://depfu.com/github/pedroslopez/whatsapp-web.js?project_id=9765) ![WhatsApp_Web 2.2206.5](https://img.shields.io/badge/WhatsApp_Web-2.2206.5-brightgreen.svg) [![Discord Chat](https://img.shields.io/discord/698610475432411196.svg?logo=discord)](https://discord.gg/H7DqQs4)  

# Weellu
An extended module for whatsapp-web.js a WhatsApp API client that connects through the WhatsApp Web browser app

It uses Puppeteer to run a real instance of Whatsapp Web to avoid getting blocked.

**NOTE:** I can't guarantee you will not be blocked by using this method, although it has worked for me. WhatsApp does not allow bots or unofficial clients on their platform, so this shouldn't be considered totally safe.

## Quick Links

* [Guide / Getting Started](https://wwebjs.dev/guide) _(work in progress)_
* [Reference documentation](https://docs.wwebjs.dev/)
* [GitHub](https://github.com/pedroslopez/whatsapp-web.js)
* [npm](https://npmjs.org/package/whatsapp-web.js)

## Installation

The module is now available on npm! `npm i weellu`

Please note that Node v13+ is required.

## Example usage

```js
const { Client, WelluMessage } = require('weellu');

const client = new Client();
let socket;

client.on('qr', (qr) => {
    // Generate and scan this code with your phone
    console.log('QR RECEIVED', qr);
});

client.on('ready', () => {
    console.log('Client is ready!');
    // Connect to  Websocket
    socket = io(SOCKET_URl, {transports: ['websocket']});
});

client.on('message', msg => {
    if (msg.body == '!ping') {
        msg.reply('pong');
    }
});

//depending on your configuration of your nodeApplication
//By Socket.io
socket.on('message', msg => {
	//whatsApp message from your database or json file
    let wMessage = new WelluMessage(client, msg);
    wMessage.reply("HI");
});

socket.on('deleteMessage', msg => {
	//whatsApp message from your database or json file
    let wMessage = new WelluMessage(client, msg);
    //delete message
    wMessage.delete(true);
});

//By express route
app.get('/message', (req, res) => {
  let msg = req.body.message;//whatsApp message format
  let wMessage = new WelluMessage(client, msg);
    wMessage.reply("HI");
})

client.initialize();
```

Take a look at [Message](https://docs.wwebjs.dev/Message.html) that explains clearly how you should format your message object, be for storing in your database or just a json file.

Take a look at [example.js](https://github.com/pedroslopez/whatsapp-web.js/blob/master/example.js) for another example with more use cases.

For more information on saving and restoring sessions, check out the available [Authentication Strategies](https://wwebjs.dev/guide/authentication.html).


## Supported features

| Feature  | Status |
| ------------- | ------------- |
| Multi Device  | ✅  |
| Send messages  | ✅  |
| Reply messages (New)  | ✅  | New
| Delete messages (New) | ✅  | New
| Support Backend (New) | ✅  |  New
| Receive messages  | ✅  |
| Send media (images/audio/documents)  | ✅  |
| Send media (video)  | ✅ [(requires google chrome)](https://wwebjs.dev/guide/handling-attachments.html#caveat-for-sending-videos-and-gifs)  |
| Send stickers | ✅ |
| Receive media (images/audio/video/documents)  | ✅  |
| Send contact cards | ✅ |
| Send location | ✅ |
| Send buttons | ✅ |
| Send lists | ✅ (business accounts not supported) |
| Receive location | ✅ | 
| Message replies | ✅ |
| Join groups by invite  | ✅ |
| Get invite for group  | ✅ |
| Modify group info (subject, description)  | ✅  |
| Modify group settings (send messages, edit info)  | ✅  |
| Add group participants  | ✅  |
| Kick group participants  | ✅  |
| Promote/demote group participants | ✅ |
| Mention users | ✅ |
| Mute/unmute chats | ✅ |
| Block/unblock contacts | ✅ |
| Get contact info | ✅ |
| Get profile pictures | ✅ |
| Set user status message | ✅ |

Something missing? Make an issue and let us know!

## Contributing

Pull requests are welcome! If you see something you'd like to add, please do. For drastic changes, please open an issue first.

## Supporting the project

You can support the maintainer of this project through the links below

- [Support via GitHub Sponsors](https://github.com/sponsors/pedroslopez)
- [Support via PayPal](https://www.paypal.me/psla/)
- [Sign up for DigitalOcean](https://m.do.co/c/73f906a36ed4) and get $100 in credit when you sign up (Referral)

## Disclaimer

This project is not affiliated, associated, authorized, endorsed by, or in any way officially connected with WhatsApp or any of its subsidiaries or its affiliates. The official WhatsApp website can be found at https://whatsapp.com. "WhatsApp" as well as related names, marks, emblems and images are registered trademarks of their respective owners.

## License

Copyright 2022 Eric weeb

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this project except in compliance with the License.
You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0.

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
