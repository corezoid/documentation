# BitcoinBot

Clone ["BitcoinBot" template](https://admin.corezoid.com/folder/conv/59749)

![](../img/bitcoinbot_clone.png)

Connect to Telegram by specifying your Bot's key

![](../img/bitcoinbot_key.png)

To receive Bot's key there's a need to send `/newbot` command to the chat with BotFather. Then specify name and bot's user name. You will got:

![](../img/botweather_keybot.png)


##What BitcoinBot does 

By `/start` command it sends message with Bot's information to chat

![](../img/bitcoinbot_start.png)


After choosing the currency to receive bitcoin convertation rates, it makes a request to blockchain API and sends a message with purchase and sell rate in selected currency.

![](../img/bitcoinbot_rate.png)


Sends appropriate message, in case if  uncertain command was received and if the error appears in process.

![](../img/bitcoinbot_send.png)


##Testing and launch

Just add your Bot to Telegram and start chat.

Go to `View` or `Debug` mode,

![](../img/botweather_view.png)

to see task flow, their moving and distributing by process nodes.

![](../img/bitcoinbot_view.png)
