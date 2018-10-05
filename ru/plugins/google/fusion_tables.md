# Fusion Tables

Рассмотрим пример сохранение данных в таблицу Fusion Tables следующего вида:
*   Text
*   Number
*   Location
*   Date

![google](../img/google/fusion_tables_example.png)

Для этого мы создадим [Google Apps Script](appscripts.md)

![google](../img/google/select_google_script.png)

Сразу переименуем проект в "Fusion tables"
![google](../img/google/rename_script.png)

И включим доступ к Fusion Tables из Google Apps Script
![google](../img/google/advance_google_service.png)

![google](../img/google/advance_google_service_2.png)

Дополнительно необходимо перейти в Google Developers Console и включить режим API для Fusion Tables
![google](../img/google/admin_console_fusion_tables_find.png)

![google](../img/google/admin_console_fusion_tables_enable.png)

После этого вставляем код следующего вида:
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

В переменной `table` заменяем текст `Insert ID Table` на ID таблицы, который необходимо скопировать как указано ниже
![google](../img/google/menu_fusion_tables.png)
![google](../img/google/fusion_tables_id.png)

###Публикация скрипта

Теперь публикуем наш код как веб-приложение с доступом всем:
![google](../img/google/Fusion_tables_script_publish_1.png)


После публикации нам доступен URL, на который необходимо методом POST отправлять JSON с данными для сохранения
![google](../img/google/Fusion_tables_script_publish_2.png)

Имена ключей в JSON должны соответствовать полям в Fusion Tables. В нашем случае JSON для отправки на API будет выглядеть следующим образом:
```json
{
  "Text":"d",
  "Number":1,
  "Location":24.5455545,
  "Date":"2016-01-01"
}
```
