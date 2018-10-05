#Getting the temperature by coordinates

http://openweathermap.org/api - full description of API capabilities.

[Process template](https://www.corezoid.com/admin/edit_conv/136513/92753) for getting air temperature by the coordinates is accessible in folder `"Examples - Open Weather"`.

To start working with the process, clone the template as follows

![](../img/mandrill_copy_conveyor.png)

Go to `dashboard` and click `Add task` - to add the request.

![](../img/mandrill_dashboard.png)

In the opened window specify the required parameter:
*   `lat` - latitude
*   `lon` - longitude

After the parameters of the request are specified, press the button `Send task`.

As a result of processes work the request will be passing along the process and then will be transferred to one of the final states (red color node):

|State|Description|Return variables|
|-|-|-|
|Success|Temperature by city name received successfully|`temp` - temperature|
|Error call API| Error of API call OpenWeather|`code` = 1 and error text|
|Error convert temp |Could not convert the resulting temperature into a number|`code` = 2 and error text|
|Error - Point is out of bounds for spherical query |Specified coordinates are out of bounds of normal values|`code` = 3 and error text|


