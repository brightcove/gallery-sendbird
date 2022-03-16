# Gallery - Sendbird Integration Demo

## Related
- https://brightcove.atlassian.net/browse/VALUEENG-479
- https://brightcove.atlassian.net/browse/VALUEENG-496

## Demo
- https://sbwidget.gallery.video/
- https://sblivechat.gallery.video/

These demos were created under a SendBird trial account with access to all features. As of this writing, the trial has ended and we've switched the account to the free "Developer plan", which has some limitations, such as a cap of 100 MAU.

---

## How-To
How to integrate a Sendbird _Live Chat_ into Gallery using the Sendbird SDK and sample app.

Recommended reading: https://sendbird.com/docs/chat/v3/javascript/quickstart/send-first-message

### Sendbird Dashboard
- Create a Senbird account if you do not have one. The developer plan allows for 100 MAU.
- Create an organization and generate an application (take note of the App ID) by going through the onboarding process.
- Set your allowed domains as appropiate in: App Settings > Application > Security > Allowed Domains.
- Create an Open Channel (take note of the channel URL.)

### Sendbird SDK and sample app.

Repo located at: https://github.com/sendbird/sendbird-javascript-samples 

Open the JavaScript `javascript-live-chat` sample in your editor.

On `webpack.config.js`:

```diff
'use strict';
const path = require('path');

module.exports = {
  entry: {
-    liveChat: ['babel-polyfill', './src/js/chat.js'],
+    liveChat: ['./src/js/chat.js'],
  },
...
```

Run `npm start` to build and start the local web server.

You'll need the following files for the Gallery integration:
- SendBird.min.js
- liveChat.SendBird.js

*Note:* 
- You must `build` or `npm start`.
- You can use different SDK versions by replacing `SendBird.min.js`.

### Gallery Catalogue Experience example

#### Custom Header HTML
Add the following to your custom header section:

```
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script src="https://my-url.example.com/SendBird.min.js"></script>
<script src="https://my-url.example.com/liveChat.SendBird.js"></script>

<script>
  setTimeout(() => {
    const sbChat = window.liveChat;

    const appId = 'my-app-ID';
    const channelUrl = 'my-channel-URL';

    var container = document.getElementsByClassName('home-carousel-info bcg-video-active bcg-fade-in-info')[0];

    const liveChatPoc = document.createElement('div');
    liveChatPoc.id = 'sb_chat';

    container.appendChild(liveChatPoc);

    sbChat.start(appId, channelUrl);

  }, 3000);
</script>

```


