# TwitterBot

Clone ["TwitterBot" template](https://admin.corezoid.com/folder/conv/5837)

![](../img/twitterbot_copy.png)

Connect to Telegram by specifying your bot key

![](../img/twitterbot_key.png)

In order to receive Bot's key you need to send `/newbot` command to chat with @BotFather. Then specify the name and bot's user name . You will get:

![](../img/botweather_keybot.png)


##Integration with Twitter

Create Twitter application on [https://apps.twitter.com](https://apps.twitter.com)

![](../img/twit_app.png)

After creation you will get a key `consumer_key`) and password (`consumer_secret`) of your application.

![](../img/twit_key.png)

In `Set twitter key & secret` node, set received values of `consumer_key` and `consumer_secret`.

![](../img/twitterbot_set.png)


##What TwitterBot does

- By `/start` command, sends a welcome message to the chat

- Receives search request that needs to be monitored in Twitter and sends to the chat all founded twits and retwits at the moment of request.

![](../img/twitterbot_chat.png)

- Further, once a day, searches for new and sends the list to the chat, if found


##Testing and launch

Just add your Bot to Telegram and start chat.

Go to `View` or `Debug` mode,

![](../img/twitterbot_debug.png)

in order ti see request flow, its moving and distributing by process nodes.
![](../img/twitterbot_view.png)
