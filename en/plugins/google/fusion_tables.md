# Fusion Tables

Let's concider the example of saving data into Fusion tables :
*   Text
*   Number
*   Location
*   Date

![google](../img/google/fusion_tables_example.png)

For this we'll create [Google Apps Script](appscripts.md)

![google](../img/google/select_google_script.png)

Immidiately rename project in "Fusion tables"
![google](../img/google/rename_script.png)

And turn on access to Fusion Tables from Google Apps Script
![google](../img/google/advance_google_service.png)

![google](../img/google/advance_google_service_2.png)

Additionaly it's neccessary to go to Google Developers Console and turn on API mode for Fusion Tables
![google](../img/google/admin_console_fusion_tables_find.png)

![google](../img/google/admin_console_fusion_tables_enable.png)

After this, put the following code:
```js
function doPost(request) {

  var table = "Insert ID Table";

  var content = JSON.parse(request.postData.contents);

  var column = "";
  var value = "";
  for (var elem in content) {
    column += elem + ",";
    value += "'" + content[elem] + "',";
  }

  column = column.substr(0, column.length-1);
  value = value.substr(0, value.length-1);

  var sql = "INSERT INTO " + table
  + " ( " + column + ") "
  + " VALUES (" + value + ")";

  Logger.log(sql);

  var sqlResult = FusionTables.Query.sql(sql);

  var result = {"result":"ok"};

  return ContentService.createTextOutput(JSON.stringify(result))
    .setMimeType(ContentService.MimeType.JSON);
}
```

In variable value`table` replace text `Insert ID Table` by ID tables, which are required to copy as it shown below:
![google](../img/google/menu_fusion_tables.png)
![google](../img/google/fusion_tables_id.png)

###Script publication

Now let's publish our code as web-application with access for all:
![google](../img/google/Fusion_tables_script_publish_1.png)


After publication  we have an access to URL, where we need to send JSON with data for save using POST method.
![google](../img/google/Fusion_tables_script_publish_2.png)

Names of the keys on JSON should match with Fusion Tables fields. In this particular case, JSON for sending to API will look the following way:
```json
{
  "Text":"d",
  "Number":1,
  "Location":24.5455545,
  "Date":"2016-01-01"
}
```
