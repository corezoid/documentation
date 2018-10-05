# WeatherBot

Clone ["WeatherBot" template](https://admin.corezoid.com/folder/conv/59753)

![](../img/botweather_copy.png)


Connect to Telegram by specifying your Bot's key.

![](../img/botweather_key.png)

In order to receive Bot's key, there's a need to send `/newbot` command to chat with @BotFather. Then, specify the name and name of Bot's user. You will get:

![](../img/botweather_keybot.png)

##Integration with OpenWeatherMap

For user's comfort, test access key for OpenWeatherMap API was added to [WeatherBot template](https://admin.corezoid.com/folder/conv/59753).

In order to receive your access key to OpenWeatherMap API, go to [the link](http://openweathermap.org/register) and register.

![](../img/weather_key.png)

In `Set APPID_key` node replace test key by the one that you received in `APPID_key` parameter value.

![](../img/botweather_set.png)


##What WeatherBot does

By `/start`  command, it sends a message with Bot's information to the chat. 

![](../img/botweather_start.png)


Receives city name or user coordinates, by it receives air temperature and sends a message.

In case is city or coordinates are specified incorrectly and also if there's an error occurred in process - it sends appropriate message.

![](../img/botweather_send.png)


##Testing and launch

Just add your bot to the Telegram and start chat.

Go to `View` or `Debug` mode,

![](../img/botweather_view.png)

in order to receive request flow, its moving and distributing it by process nodes.

![](../img/botweather_view1.png)
