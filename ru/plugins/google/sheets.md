# Sheets

Пример добавления записей в заранее созданную таблицу.

Cоздадим скрипт внутри таблицы.

Для этого откроем редактор
![google]

И вставим в появившемся окне следующий скрипт, который добавляет записи `name` и `price` в таблицу
```javascript
function doGet(request) {


   var row = [];
   row.push(request.parameter.name);
   row.push(request.parameter.price);

   

   var ss = SpreadsheetApp.openById("Sheet_id")
   var sheet = ss.getSheetByName("Sheet_name");
   sheet.appendRow(row);

   var result = {"result":"ok"};

   return ContentService.createTextOutput(JSON.stringify(result))
     .setMimeType(ContentService.MimeType.JSON);
}
```

Теперь заменим текст `Sheet_name` на название листа Вашей таблицы, а `Sheet_id` на ее ID.

Скопируем ID из URL таблицы (выделенно желтым цветом)
![google](../img/google/URL_id_sheet.png)

Скрипт для записи данных в таблицу из Corezoid готов.

Опубликуем его и запустим из Corezoid.

###Публикация скрипта


Теперь публикуем наш код как веб-приложение с доступом всем:
![google](../img/google/sheet_public_script.jpg)


После публикации нам доступен URL, на который необходимо методом GET отправлять JSON с данными для сохранения
![google](../img/google/Fusion_tables_script_publish_2.png)

Пример, настроенной логики Api Call

![google](../img/google/api_call.jpg)

Результат обработки в процессе

![google](../img/google/api_call_result.jpg)

Результат обработки в таблице

![google](../img/google/sheet_result.jpg)




