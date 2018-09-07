# Zingle Web Messenger

The Zingle Web Messenger will add live web messaging to your website or web app.

## Usage

### Script Tag

Add the following code towards the end of the `head` section on your page and replace `<app-id>` with your app id at the end of the script.

```html
<script>
    !function(e,n,t,r){function s(){try{var e;if((e="string"==typeof this.response?JSON.parse(this.response):this.response).url){var t=n.getElementsByTagName("script")[0],r=n.createElement("script");r.async=!0,r.src=e.url,t.parentNode.insertBefore(r,t)}}catch(e){}}var o,i,p,a=[],c=[];e[t]={init:function(){o=arguments;var e={then:function(n){return c.push({type:"t",next:n}),e},catch:function(n){return c.push({type:"c",next:n}),e}};return e},on:function(){a.push(arguments)},render:function(){i=arguments},destroy:function(){p=arguments}},e.__onWebMessengerHostReady__=function(n){if(delete e.__onWebMessengerHostReady__,e[t]=n,o)for(var r=n.init.apply(n,o),s=0;s<c.length;s++){var u=c[s];r="t"===u.type?r.then(u.next):r.catch(u.next)}i&&n.render.apply(n,i),p&&n.destroy.apply(n,p);for(s=0;s<a.length;s++)n.on.apply(n,a[s])};var u=new XMLHttpRequest;u.addEventListener("load",s),u.open("GET","https://cdn.zingle.me/web-chat/loader.json",!0),u.responseType="json",u.send()}(window,document,"Zingle");
</script>
```

then initialize the Web Messenger by placing this snippet towards the end of the `body` section of your page.

```html
<script>
    Zingle.init({appId: '<app-id>'}).then(function() {
        // Your code after init is complete
    });
</script>
```

## Browser support

Web Messenger supports all popular browsers.

#### Desktop versions

- Chrome: Latest and one major version behind
- Edge:  Latest and one major version behind
- Firefox:  Latest and one major version behind
- Internet Explorer: 11+
- Safari:  Latest and one major version behind

#### Mobile versions

- Stock browser on Android 4.1+
- Safari on iOS 8+

#### Other browsers

Web Messenger is likely compatible with other and older browsers but we only test against the versions above.

## API

### Individual functions

#### init(options)
Initializes the Zingle widget in the web page using the specified options. It returns a promise that will resolve when the Web Messenger is ready. Note that except`on` and `off`, all methods needs to be called after a successful `init`.

##### Options

| Option | Optional? | Default value | Description |
| --- | --- | --- | --- |
| appId | No | - | Your app id |
| jwt | Yes | - | Token to authenticate your communication with the server
| userId | Yes | - | User's id |
| locale | Yes | `en-US` | Locale used for date formatting using the `<language>-<COUNTRY>` format. Language codes can be found [here](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) and country codes [here](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). <br /> **Note 1 : ** The country part is optional, and if a country is either not recognized or supported, it will fallback to using the generic language. If the language isn't supported, it will fallback to `en-US`. <br /> **Note 2:** this is *only* used for date formatting and doesn't provide built-in translations for Web Messenger. |
| soundNotificationEnabled | Yes | `true` | Enables the sound notification for new messages |
| imageUploadEnabled | Yes | `true` | Enables the image upload feature. |
| embedded | Yes | False | Tells the widget it will be embedded. (see Embedded section below) |
| customText | Yes | See the example below | Strings used in the widget UI. You can use these to either customize the text or translate it. If something is between `{}`, it's a variable and needs to stay in your customized text if you want to use it. |

```javascript
var skPromise = Zingle.init({
    appId: '<app-id>',
    // For authenticated mode
    jwt: 'your_jwt',
    userId: 'user_id',
    locale: 'en-US',
    customText: {
        actionPaymentCompleted: 'Payment Completed',
        actionPaymentError: 'An error occurred while processing the card. <br> Please try again or use a different card.',
        actionPostbackError: 'An error occurred while processing your action. Please try again.',
        clickToRetry: 'Message not delivered. Click to retry.',
        connectNotificationText: 'Be notified inside your other apps when you get a reply.',
        conversationTimestampHeaderFormat: 'MMMM D YYYY, h:mm A',
        fetchHistory: 'Load more',
        fetchingHistory: 'Retrieving history...',
        frontendEmailChannelDescription: 'To talk to us using email just send a message to our email address and we\'ll reply shortly:',
        headerText: 'How can we help?',
        inputPlaceholder: 'Type a message...',
        introAppText: 'Message us below or from your favorite app.',
        introductionText: 'We\'re here to talk, so ask us anything!',
        invalidFileError: 'Only images are supported. Choose a file with a supported extension (jpg, jpeg, png, gif, or bmp).',
        lineChannelDescription: 'To talk to us using LINE, scan this QR code using the LINE app and send us a message.',
        locationNotSupported: 'Your browser does not support location services or it’s been disabled. Please type your location instead.',
        locationSecurityRestriction: 'This website cannot access your location. Please type your location instead.',
        locationSendingFailed: 'Could not send location',
        locationServicesDenied: 'This website cannot access your location. Allow access in your settings or type your location instead.',
        messageError: 'An error occured while sending your message. Please try again.',
        messageIndicatorTitlePlural: '({count}) New messages',
        messageIndicatorTitleSingular: '({count}) New message',
        messageRelativeTimeDay: '{value}d ago',
        messageRelativeTimeHour: '{value}h ago',
        messageRelativeTimeJustNow: 'just now',
        messageRelativeTimeMinute: '{value}m ago',
        messageTimestampFormat: 'hh:mm A',
        messengerChannelDescription: 'Connect your Facebook Messenger account to be notified when you get a reply and carry the conversation on Facebook Messenger.',
        notificationSettingsChannelsDescription: 'You can also talk to us from your favorite app or service.',
        notificationSettingsChannelsTitle: 'Other Channels',
        notificationSettingsConnected: 'Connected',
        notificationSettingsConnectedAs: 'Connected as {username}',
        sendButtonText: 'Send',
        settingsHeaderText: 'Settings',
        smsBadRequestError: 'We were unable to communicate with this number. Try again or use a different one.',
        smsCancel: 'Cancel',
        smsChangeNumber: 'Change my number',
        smsChannelDescription: 'Connect your SMS number to be notified when you get a reply and carry the conversation over SMS.',
        smsChannelPendingDescription: 'Check your messages at {number} to confirm your phone number.',
        smsContinue: 'Continue',
        smsInvalidNumberError: 'Your phone number isn\'t valid. Please try again.',
        smsLinkCancelled: 'Link to {appUserNumber} was cancelled.',
        smsLinkPending: 'Pending',
        smsPingChannelError: 'There was an error sending a message to your number.',
        smsSendText: 'Send me a text',
        smsStartTexting: 'Start Texting',
        smsTooManyRequestsError: 'A connection for that number was requested recently. Please try again in {minutes} minutes.',
        smsTooManyRequestsOneMinuteError: 'A connection for that number was requested recently. Please try again in 1 minute.',
        smsUnhandledError: 'Something went wrong. Please try again.',
        tapToRetry: 'Message not delivered. Tap to retry.',
        telegramChannelDescription: 'Connect your Telegram account to be notified when you get a reply and carry the conversation on Telegram',
        transferError: 'An error occurred when attempting to generate a link for this channel. Please try again.',
        viberChannelDescription: 'Connect your Viber account to be notified when you get a reply and carry the conversation on Viber. To get started, scan the QR code using the Viber app.',
        viberChannelDescriptionMobile: 'Connect your Viber account to be notified when you get a reply and carry the conversation on Viber. To get started, install the Viber app and tap Connect.',
        viberQRCodeError: 'An error occurred while fetching your Viber QR code. Please try again.',
        wechatChannelDescription: 'Connect your WeChat account to be notified when you get a reply and carry the conversation on WeChat. To get started, scan this QR code using the WeChat app.',
        wechatChannelDescriptionMobile: 'Connect your WeChat account to be notified when you get a reply and carry the conversation on WeChat. To get started, save this QR code image and upload it in the <a href=\'weixin://dl/scan\'>QR code scanner</a>.',
        wechatQRCodeError: 'An error occurred while fetching your WeChat QR code. Please try again.'
    }
}).then(function() {
    // Your code after init is complete
});


initPromise.then(function() {
    // do something
});

// pass it around...

initPromise.then(function() {
    //do something else
});

```

#### open()
Opens the conversation widget (noop when embedded)

```javascript
Zingle.open();
```

#### close()
Closes the conversation widget (noop when embedded)

```javascript
Zingle.close();
```

#### isOpened()
Tells if the widget is currently opened or closed.

```javascript
Zingle.isOpened();
```

#### login(userId , jwt)
Logs a user in the Web Messenger, retrieving the conversation the user already had on other browsers and/or devices. Note that you don't need to call this after `init` if you passed the user id and jwt already, it's done internally. This returns a promise that resolves when the Web Messenger is ready again.

```
Zingle.login('some-id', 'some-jwt');
```

#### logout()
Logs out the current user and reinitialize the widget with an anonymous user. This returns a promise that resolves when the Web Messenger is ready again.

```
Zingle.logout();
```

#### destroy()
Destroys the Web Messenger and makes it disappear. The Web Messenger has to be reinitialized with `init` to be working again because it also clears up the app id from the Web Messenger. It will also unbind all listeners you might have with `Zingle.on`.

```
Zingle.destroy();
```

#### sendMessage(message)
Sends a message on the user's behalf

```javascript
Zingle.sendMessage({
    type: 'text',
    text: 'hello'
});

// OR

Zingle.sendMessage('hello');
```

#### updateUser(user)
Updates user information. The 'properties' object specified contact field properties that should be updated.  Use the Contact Field name as the property name. 

```javascript
Zingle.updateUser({
    givenName: 'Updated',
    surname: 'Name',
    email: 'updated@email.com',
    properties: {
      'Room Number': 202
    }
});
```

#### getUser()
Returns the current user.

```javascript
var user = Zingle.getUser()
```

#### getConversation()
Returns the conversation if it exists

```javascript
var conversation = Zingle.getConversation();
```

#### startConversation()
Creates a user and conversation on the server, allowing the business to reach out proactively to the user via the public API.

It is strongly recommended to only call this method in the case where a message is likely to be sent.

This method is called automatically when starting a conversation via the `sendMessage` method, or when a user sends a message via the conversation view.

If a conversation already exists for the current user, this call is a no-op.

```javascript
Zingle.startConversation();
```

### Events
If you want to make sure your events are triggered, try to bind them before calling `Zingle.init`.

To bind an event, use `Zingle.on(<event name>, <handler>);`. To unbind events, you can either call `Zingle.off(<event name>, handler)` to remove one specific handler, call `Zingle.off(<event name>)` to remove all handlers for an event, or call `Zingle.off()` to unbind all handlers.

#### ready
```
// This event triggers when init completes successfully... Be sure to bind before calling init!
Zingle.on('ready', function(){
    console.log('the init has completed!');
});

Zingle.init(...).then(function() {
    // Your code after init is complete
});
```

#### destroy
```
// This event triggers when the widget is destroyed.
Zingle.on('destroy', function(){
    console.log('the widget is destroyed!');
});

Zingle.destroy();
```

#### message:received
```
// This event triggers when the user receives a message
Zingle.on('message:received', function(message) {
    console.log('the user received a message', message);
});
```

#### message:sent
```
// This event triggers when the user sends a message
Zingle.on('message:sent', function(message) {
    console.log('the user sent a message', message);
});
```

#### message
```
// This event triggers when a message was added to the conversation
Zingle.on('message', function(message) {
    console.log('a message was added to the conversation', message);
});
```

#### unreadCount
```
// This event triggers when the number of unread messages changes
Zingle.on('unreadCount', function(unreadCount) {
    console.log('the number of unread messages was updated', unreadCount);
});
```

#### widget:opened
```
// This event triggers when the widget is opened
Zingle.on('widget:opened', function() {
    console.log('Widget is opened!');
});
```

#### widget:closed
```
// This event triggers when the widget is closed
Zingle.on('widget:closed', function() {
    console.log('Widget is closed!');
});
```

### Embedded mode
As describe above, to activate the embedded mode, you need to pass `embedded: true` when calling `Zingle.init`. By doing so, you are disabling the auto-rendering mechanism and you will need to call `Zingle.render` manually. This method accepts a DOM element which will be used as the container where the widget will be rendered.

The embedded widget will take full width and height of the container. You must give it a height, otherwise, the widget will collapse.

## Acknowledgements

https://github.com/lipis/flag-icon-css
