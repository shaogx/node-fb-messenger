# fb-messenger [![npm](https://img.shields.io/npm/v/fb-messenger.svg)](https://www.npmjs.com/package/fb-messenger) [![npm](https://img.shields.io/npm/dm/fb-messenger.svg)](https://www.npmjs.com/package/fb-messenger) [![npm](https://img.shields.io/npm/l/fb-messenger.svg)](LICENSE) 
#### Facebook Messenger Platform NodeJS API Wrapper

[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com/) [![Greenkeeper badge](https://badges.greenkeeper.io/DiegoRBaquero/node-fb-messenger.svg)](https://greenkeeper.io/) [![Codacy Badge](https://api.codacy.com/project/badge/Grade/b3cbd4666fa54722b38288c98cd5e8c1)](https://www.codacy.com/app/diegorbaquero/node-fb-messenger?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=DiegoRBaquero/node-fb-messenger&amp;utm_campaign=Badge_Grade) [![Code Climate](https://codeclimate.com/github/DiegoRBaquero/node-fb-messenger/badges/gpa.svg)](https://codeclimate.com/github/DiegoRBaquero/node-fb-messenger)

## Installation

**Requires Node 8+**

```bash
npm install fb-messenger --save
```

## API

You must require fb-messenger and create an instance

```js
// Constructor
const FBMessenger = require('fb-messenger')
const messenger = new FBMessenger({token, notificationType}) // notificationType is optional, default = 'REGULAR'

// Methods (notificationType is optional)
messenger.sendTextMessage({id, message, notificationType}) // Sends a text message

messenger.sendImageMessage({id, imageURL, notificationType}) // Sends an image from URL

messenger.sendHScrollMessage({id, elements, notificationType}) // Sends an H-SCroll generic message

messenger.sendButtonsMessage({id, message, buttons, notificationType}) // Sends a buttons message

messenger.sendListMessage({id, elements, buttons, top_element_type, notificationType}) // Sends a list message

messenger.sendReceiptMessage({id, payload, notificationType}) // Sends a receipt message (No need for template_type in payload) 

messenger.sendQuickRepliesMessage({id, attachment, quickReplies, notificationType}) // Sends a Quick Replies Message

messenger.sendMessage({id, data, notificationType}) // Send a message from custom data

messenger.sendAction({id, actionType}) // Send an action type (One of 'mark_seen', 'typing_on', 'typing_off')

messenger.getProfile(id) // Gets user information

messenger.setWelcomeMessage({pageId, message}) // Sets Page's Welcome Message (message can be a text string or a strucuted message)

messenger.setGreetingText ({pageId, message}) // Sets Page's Greeting Text

messenger.setPersistentMenu ({pageId, menuItems}) // Set's Page's Persistent Menu

messenger.setDomainWhitelist ({pageId, domains}) // Set's Page's Whitelisted Domains 

messenger.sendThreadSettingsMessage ({pageId, body}) // Send Manually Page's Thread Settings
```

#### Notification Types:
 - REGULAR
 - SILENT_PUSH
 - NO_PUSH

## Examples

### Basic Example

```js
const FBMessenger = require('fb-messenger')
const messenger = new FBMessenger({token: '<YOUR TOKEN>'})

messenger.sendTextMessage({id: '<ID>', text: 'Hello'})
```

### Catch errors Example

```js
const FBMessenger = require('fb-messenger')
const messenger = new FBMessenger({token: '<YOUR TOKEN>'})

try {
  const response = await messenger.sendTextMessage({id: '<ID>', text: 'Hello'})
  console.log(response)
} catch (e) {
  console.error(e)
}
```

### No push Example

```js
const FBMessenger = require('fb-messenger')
const messenger = new FBMessenger({token: '<YOUR TOKEN>'})

messenger.sendTextMessage({id: '<ID>', text: 'Hello', notificationType: 'NO_PUSH'})
```

### Default to silent push Example

```js
const FBMessenger = require('fb-messenger')
const messenger = new FBMessenger({token: '<YOUR TOKEN>', notificationType: 'SILENT_PUSH'})
```

### Complete Example

```js
const FBMessenger = require('fb-messenger')
const messenger = new FBMessenger({token: '<YOUR TOKEN>', notificationType: 'NO_PUSH'})

try {
  await messenger.sendTextMessage({id: '<ID>', text: 'Hello'}) // Send a message with NO_PUSH, ignoring response
  console.log('Sent successfully')
} catch(e) {
  console.error(e)
}

// Send an image overriding default notification type with callback
try {
  const response = await messenger.sendImageMessage({id: '<ID>', url: '<IMG URL>', notificationType: 'REGULAR'})
  console.log('Sent image, response:')
  console.dir(response)
} catch(e) {
  console.error(e)
}
```

## License

MIT. Copyright © [Diego Rodríguez Baquero](https://diegorbaquero.com)
