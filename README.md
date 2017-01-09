# Botkit Middleware for multilingual projects with Wit.ai
[![npm](https://img.shields.io/npm/dt/botkit-witai.svg)]() [![npm](https://img.shields.io/npm/l/botkit-witai.svg?style=flat)]() [![GitHub stars](https://img.shields.io/github/stars/mrbot-ai/botkit-witai-multilingual.svg?style=social&label=Star)]()

Unleash the power of Wit.ai's Natural Language Processing to your Botkit bot with this middleware. All incoming text messages (by default it filters payload derived from Facebook Messenger buttons like *Quick Replies* and *Postbacks*) will go through Wit.ai's API to extract useful *entities* that will be added to the message object so they can be used in the controller.


## Installation
In order to utilize wit.ai's service you will need to create an account at [Wit.ai](https://wit.ai/). Grab the *access token* at Settings as shown below:

![Screenshot](https://s30.postimg.org/5o330d21t/Wit_ai_screenshot.png)


Next you will need to add botkit-witai as a dependency to your Botkit bot:

```
npm install --save botkit-witai
```

Enable the middleware with the following options:
* `tokens` - (**required**) Tokens to use Wit.ai API
* `minConfidence` - (*optional*) Minimum Wit.ai's entities confidence value to be considered. Valid value range is from **0.1** to **1**. **0.5** is the default.
* `logLevel` - (*optional*) Log level for the middleware. Valid values are: **'debug', 'info', 'warning', 'error'**.

Example:
```js
var wit = require('botkit-witai')({
    tokens:{
     default: <my_witai_default_token>,
     fr_CA: <my_witai_fr_CA_token>
    }
    minConfidence: 0.6,
    logLevel: 'debug'
});

controller.middleware.receive.use(wit.receive);
```
## Usage
You will receive in the callback of the `controller.hears` the Wit.ai's entities defined in your panel as shown below that match the message received:

![Screenshot](https://s24.postimg.org/3xbepffo5/Wit_ai_screenshot_2.png)

Example:

```js
controller.hears(['spa'], 'message_received', wit.hears, function (bot, message) {
      console.log("Wit.ai detected entities", message.entities);
      //Example message: "I want a spa treatment"
      //    {
      //      "spa": [
      //        {
      //          "confidence": 1,
      //          "type": "value",
      //          "value": "spa"
      //        }
      //      ]
      //    }

      //Your code here
});
```
##Roadmap

* Wit.ai's conversation actions linked to Botkit's conversation steps.
* Functional testing coverage.

##Author
**Rafael Casuso**

Github: [@RafaelCasuso](https://github.com/RafaelCasuso)

Twitter: [@Rafael_Casuso](https://twitter.com/rafael_casuso)
