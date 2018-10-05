* [App ID and Webhook](#appid)
* [Making BitcoinBot](#bitcoinbot)
* [Webhook set up](#webhook)
* [What BitcoinBot does](#do)
* [Testing and launch](#test)


###  App ID and Webhook {#appid}

1. Create the app in [Microsoft Bot Framework](https://dev.botframework.com/).
2. Go to **"Register a bot"** tab and register your bot.You can get extra info about bot registration in [Documentation](https://docs.botframework.com/en-us/skype/getting-started/#navtitle) tab.
3. Get your personal **Microsoft App ID** application key and **client_secret** password.
![](app_id.jpg)

4. Put the recieved url of WEatherBot process, in **"My bots"** tab, in **Messaging endpoint** field. Instruction how to get webhook-url is [here](#webhook).
![](mess_endpoint1.jpg)

5. Publish your bot by pressing button "Publish".
![](publish.jpg)


After bot creation you need to publish it, because otherwise the amount of visiters could be limited. 

Pay attention, after bot publication there's a need to disable  using of bot  in group chats.





### WeatherBot{#weatherbot} creation

Clone [folder with "WeatherBot_skype" process](https://admin.corezoid.com/folder/conv/111724).
![](clone_folder.jpg)

In ```"WeatherBot_skype" process```, in ```Set skype_authorization and APPID``` node, in variable values:
* **skype_authorization** - put this construction. 

```
{{conv[{{process_id}}].ref[{{ref}}].parameter_ID}}
```

* **APPID**- put test access key for OpenWeatherMap API.

![](set_param.jpg)

```"Skype authorization" process``` designed to recieve **access_token** for Skype API and, as far as exparation time of the key is 3600 sec, so after this exparation time process renews it and transfer valid access_token in ```"Skype storage" state diagram```.

 Using such construction as 
 ```
 {{conv[{{process_id}}].ref[{{ref}}].ID_параметра}}
 ```
 we make a request to "Skype storage" state diagram and recieve access_token.
 
  
 
### Webhook{#webhook} set up

Connect WeatherBot process to Skype using webhook-url. To get webhook-url of WeatherBot process, select "Connect to messenger":
![](connect_to_messenger.jpg)
![](skype.jpg)

Get webhook-url of WeatherBot process for SKYPE.

![](webhook.jpg)

In **Client ID** empty field put your personal code for **Microsoft App ID** application, the one that you recieved while Bot creation.
In **Client Secret** field put your password for application.

Specify recieved webhook-url of process in settings of your bot in **My bots** tab, in **Messaging endpoint** field. More details [here](#appid).


### What WeatherBot{#do} does

WeatherBot for new contacts sends information about Bot to ```Send info about bot.``` node.

WeatherBot - recieves webhook-s with city name , gets ait temperature with this and sends the message.

In case if message does not contain city name or city is specified incorrectly, also if there is some error in process, bot sends appropriate message. 

Also WeatherBot defines bot remove action and sends to ```Bot removed.``` node.



### Integration with OpenWeatherMap{#map}

For user's comfort, we added a test access key for OpenWeatherMap API to ["WeatherBot_skype" template](https://admin.corezoid.com/folder/conv/111724). To get your access key for OpenWeatherMap API, follow [link](https://home.openweathermap.org/users/sign_in) and register.
![](weather_key.png)

In **"Set skype_authorization and APPID"** node replace test OpenWeatherMAP API key by the one you received in **APPID** parameter's value. 



### Testing and launch{#test}
Just add your Bot to Skype by [link](https://join.skype.com/bot/e0a994fb-d527-4122-a92b-b91ae55910c2) or from [bot's catalog](https://bots.botframework.com/) (if bot has been published) and start chatting.
![](new_screen_weatherbot.jpg)

Switch to **View** or **Debug** mode  to see request flow, their transit and process nodes distribution. 
![](botweather_view.png)
