[![npm](https://img.shields.io/npm/v/whatsapp-web-electron.js)](https://www.npmjs.com/package/whatsapp-web-electron.js) [![Depfu](https://badges.depfu.com/badges/4a65a0de96ece65fdf39e294e0c8dcba/overview.svg)](https://depfu.com/github/pedroslopez/whatsapp-web.js?project_id=9765) ![WhatsApp_Web 2.2126.14](https://img.shields.io/badge/WhatsApp_Web-2.2126.14-brightgreen.svg)  

# whatsapp-web-electron.js

A WhatsApp API client that connects through the WhatsApp Web browser app

It uses Puppeteer to run a real instance of Whatsapp Web to avoid getting blocked.

This is an electron wrapper for [whatsapp-web.js](https://github.com/pedroslopez/whatsapp-web.js) which connect using [puppeteer-in-electron](https://github.com/TrevorSundberg/puppeteer-in-electron).

**NOTE:** I can't guarantee you will not be blocked by using this method, although it has worked for me. WhatsApp does not allow bots or unofficial clients on their platform, so this shouldn't be considered totally safe.

## Installation

The module is now available on [npm](https://npmjs.org/package/whatsapp-web-electron.js)! `npm i whatsapp-web-electron.js`

Please note that Node v12+ is required.

## Example usage

```js
const { app, BrowserWindow } = require('electron');
const puppeteer = require('puppeteer-core');
const pie = require('puppeteer-in-electron');
const { Client } = require('whatsapp-web-electron.js');

const window = new BrowserWindow({
    // your options...
});

pie.connect(app, puppeteer).then((pieBrowser) => {
    const client = new Client(pieBrowser, window);

    // No need to listen for "qr" event as you can scan
    // the qr code directly in electron window

    client.on('ready', () => {
        console.log('Client is ready!');
    });

    client.on('message', msg => {
        if (msg.body == '!ping') {
            msg.reply('pong');
        }
    });

    client.initialize();
});
```

Take a look at [whatsapp-web.js example.js](https://github.com/pedroslopez/whatsapp-web.js/blob/master/example.js) for another example with more use cases. The only difference should be the initialization process and a few feature (explained below).

## Remote Access and Docker

The original [whatsapp-web.js](https://github.com/pedroslopez/whatsapp-web.js) has remote access feature and supports docker which is irrelevant for an electron project, that's why I didn't include it here.

## Sending Arbitrary Image as Sticker

Sending image as sticker requires [sharp](https://github.com/lovell/sharp/releases) package and it's difficult to package with electron, so I choose to remove it. Feel free to open a PR if you can fix this issue.

## Supported features

| Feature  | Status |
| ------------- | ------------- |
| Send messages  | ✅  |
| Receive messages  | ✅  |
| Send media (images/audio/documents)  | ✅  |
| Send media (video)  | ✅ [(requires google chrome)](https://guide.wwebjs.dev/features/handling-attachments#caveat-for-sending-videos-and-gifs)  |
| Send stickers | ✅ [(can't send arbitrary image)](#sending-arbitrary-image-as-sticker) |
| Receive media (images/audio/video/documents)  | ✅  |
| Send contact cards | ✅ |
| Send location | ✅ |
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

## whatsapp-web.js Links

* [Reference](https://docs.wwebjs.dev/)
* [Guide](https://guide.wwebjs.dev/) _(work in progress)_
* [GitHub](https://github.com/pedroslopez/whatsapp-web.js)
* [npm](https://npmjs.org/package/whatsapp-web.js)

## Contributing

Pull requests are welcome! If you see something you'd like to add, please do. For drastic changes, please open an issue first.

## Disclaimer

This project is not affiliated, associated, authorized, endorsed by, or in any way officially connected with WhatsApp or any of its subsidiaries or its affiliates. The official WhatsApp website can be found at https://whatsapp.com. "WhatsApp" as well as related names, marks, emblems and images are registered trademarks of their respective owners.

## License

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this project except in compliance with the License.
You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0.

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
