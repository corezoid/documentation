# Gmail  
  
**Gmail** — это бесплатная почтовая служба от компании Google.  
  
**Gmail** позволяет использовать [REST API](https://ru.wikipedia.org/wiki/REST), c помощью которого можно работать с почтовым ящиком, в том числе получать непрочитанные входящие письма.  
  
**Gmail API** дает доступ к ресурсам, таким как **[Threads](https://developers.google.com/gmail/api/v1/reference/users/threads), [Messages](https://developers.google.com/gmail/api/v1/reference/users/messages), [Labels](https://developers.google.com/gmail/api/v1/reference/users/labels), [Drafts](https://developers.google.com/gmail/api/v1/reference/users/drafts)** или **[History](https://developers.google.com/gmail/api/v1/reference/users/history)**. Например, стороннее приложение может запросить доступ только на отправку писем, но без чтения; или только на чтение, но без отправки.  
  
Перед настройкой процесса рекомендуем изучить документацию **Gmail API** по ссылке Перед настройкой процесса рекомендуем изучить документацию **Gmail API** по ссылке [https://developers.google.com/gmail/api/v1/reference/users/drafts](https://developers.google.com/gmail/api/v1/reference/users/drafts)
                 
С помощью этого туториала Вы научитесь использовать **Gmail API** для получения неотвеченных писем и их деталей из почтового ящика. Для этого мы построим 3  процесса: **Init, Reading, Message Info**.  
  
  1. **Init** - процесс для запуска подпроцесса **Reading**, который будет вычитывать почту. Процесс **Init** будет работать циклически, чтобы раз в Х минут получать новые сообщения из почты.  
    
  2. **Reading** - процесс получает непрочитанные сообщения и по одному отправляет их id в процессе **Message Info** для получения детальной информации, а также помечает сообщение прочитанным (снимает с сообщения метку "UNREAD").  
   
  3. **Message Info** - получает детальную информацию о письме по ID.  
   
На рисунке ниже Вы можете видеть взаимодействие процессов Corezoid с **Gmail API**.
   
   ![img](en/plugins/google/gmail/img/../../../../../img/basic-scheme.png)  
    
  Прежде чем вы начнете, убедитесь, что у Вас есть действующий почтовый ящик @gmail или Google-аккаунт. Если почтового ящика @gmail или Google-аккаунта у Вас нет, то вы можете завести его по ссылке [http://gmail.com](http://gmail.com).  
   
 Как любое Google API, для вызова **Gmail API** нужно авторизоваться с помощью протокола OAuth 2.0. Увидеть пример подключения к Google OAuth 2.0 Вы можете в туториале [Google OAuth 2.0](../ouath/README.md).
 
 > Важно! Для продолжения работы Вам необходимо пройти туториал [Google OAuth 2.0](../ouath/README.md).
 
  
### Получение списка непрочитанных писем  
  
1. Перед тем, как мы начнем строить процесс получения списка непрочитанных писем, для удобства работы создайте папку с именем **Gmail**  
  
    ![img](en/plugins/google/gmail/img/../../../../../img/create-gmail-folder.png)  
    
    ![img](en/plugins/google/gmail/img/../../../../../img/enter-gmail-folder.png)  

2. Теперь зайдите в созданную папку **Gmail** и создайте процесс **Reading**. Он будет вызывать **Gmail API** для получения списка непрочитанных писем.  
  
    ![img](en/plugins/google/gmail/img/../../../../../img/create-reading-process.png)  
  
3. Добавьте в процессе **Reading** узел **API Call** c именем **Get UNREAD message IDs**  

    3.1. Для этого в узле **API Call** в поле **URL** укажите ссылку: https://www.googleapis.com/gmail/v1/users/{{email}}/messages?q=is%3Aunread
   
    Установите следующие значения в настройках узла **API Call**:  
    ```   
     Request format: Default  
     Request method: GET  
     Content-Type: Application/Json  
    ```

    3.2. В разделе ***Additionally*** поставьте галочку напротив **Header parameters**.  
 и добавьте параметр **Authorization** со значением **Bearer {{token}}**.   
 
    ```
    {  
        "Authorization": "Bearer {{token}}"  
    }  
    ```
    
    В переменную **{{token}}** Вы будете передавать **ACCESS_TOKEN** из диаграммы состояний **Token Storage**, из туториала [Google OAuth 2.0](Google OAuth 2.0)  

    ![img](en/plugins/google/gmail/img/../../../../../img/google-api-auth.png)  
  
    3.3. Для обработки ответа **Gmail API** об отсутствии непрочитанных писем добавьте узел **Condition** c именем **Is UNREAD?**, который будет переводить заявку в финальный узел, если в почтовом ящике закончились непрочитанные сообщения. Для этого добавьте условие```resultSizeEstimate == 0```
  
   ![img](en/plugins/google/gmail/img/../../../../../img/check-result-size.png)  
  
    3.4. Для получения ID непрочитанных писем перейдите в режим **VIEW** и создайте заявку с двумя параметрами: **email** и **token**.   
 
    3.5. В параметре `email` передавайте адрес почтового ящика из аккаунта **Google**, на котором Вы генерировали `ACCESS_TOKEN`. В параметре `token` укажите полученный `ACCESS_TOKEN`

    3.6. В случае положительного ответа от **Gmail API**, Ваша заявка будет находиться в узле **Final**. Нажав на него, в параметре **messages** Вы увидите массив с ID непрочитанных писем.  
  
    Пример массива:  
    ```
    messages": [  
         { "id": "16c24fa1a4eedf28", "threadId": "16c24fa1a4eedf28" }, 
         { "id": "16c24fa196122fc3", "threadId": "16c24fa189a65201" }, 
         { "id": "16c24fa189a65201", "threadId": "16c24fa189a65201" }
     ]  
    ```

    ![img](en/plugins/google/gmail/img/../../../../../img/show-unread-messages.png) 
  
Процесс для получения ID непрочитанных писем у Вас готов!  
  
### Получить информацию о письме по ID  
  
1. Создайте процесс **Message Info** для получения информации о непрочитанном письме по его ID через **Gmail API**.  
  
    ![img](en/plugins/google/gmail/img/../../../../../img/create-message-info-process.png)  
  
    1.1. Для этого в процессе **Message Info** создайте узел **API Call** с именем **Getting Info**, в котором Вы будете вызывать **Gmail API**.   
  
    1.2. В поле **URL API** добавьте ссылку [https://www.googleapis.com/gmail/v1/users/{{email}}/messages/{{messd}}](https://www.googleapis.com/gmail/v1/users/{{email}}/messages/{{messd}})  
    и установите следующие значения в настройках узла **API Call**:  
     ``` 
    Request format: Default  
    Request method: GET  
    Content-Type: Application/Json  
    ```
    
    1.3. В разделе **Parameters** добавьте 2 параметра :
    ```
    "email": "{{email}}
    "message_id": "{{message_id}}"

    ```
 
    1.4. В разделе ***Additionaly*** добавьте чекбокс напротив **Header parameters**. В появившемся поле добавьте параметр **Autorization** cо значением **Bearer {{token}}**.  
    ```
    {  
        "Authorization": "Bearer {{token}}"  
    }  
      ```

    ![img](en/plugins/google/gmail/img/../../../../../img/google-auth-to-get-message-info.png)  
  

2. После того, как Вы настроили вызов **Gmail API**, можете отправить заявку для получения инфорамции о непрочитанном письме.  

    2.1 В режиме **View** нажмите кнопку **New Task**  

    2.2. В окне **Task** заполните указанные ниже поля и нажмите **Add task**:  
  
    - **message_id** - cкопируйте его из финального узла процесса **Reading**  
    - **token** - токен вызова Gmail API.  
    - **email** - укажите email, по которому Вы получили ID непрочитанных писем.  
      
    ![img](en/plugins/google/gmail/img/../../../../../img/create-new-task.png)  
  
    Если **Gmail API** вернет успешный ответ, то заявка с деталями письма появится в узле **Final**.  
  
    2.3. Для просмотра информации о письме перейдите в режим **View**   
    
    2.4. Кликните на узел **Final**. В появившемся окне Вы можете изучить структуру параметров письма.  
  
    ![img](en/plugins/google/gmail/img/../../../../../img/get-info-by-message-id.png)  
  
### Изменение статуса письма на “Прочитано”  
  
1. Для того, чтобы после получения информации о письме поставить ему флаг о прочтении, в процессе **Message Info** после узла **Getting Info** добавьте узел **API Call**  
    
    1.1. В поле **URL API** добавьте ссылку: 
    `https://www.googleapis.com/gmail/v1/users/{{email}}/messages/{{message_id}}/modify`
    
    1.2. В настройках узла *API Call* добавьте следующие настройки:
    
    ``` 
    Request format: Default
    Request method: POST
    Content-Type: Application/Json
    ```
  
    1.3. В разделе ***Parameters*** добавьте:  
  
    ```
    {  
        "removeLabelIds": ["UNREAD"]
    }  
     ``` 
  
    1.4. В разделе ***Additionally*** поставьте чекбокс напротив ***Header parameters***.  
и добавьте параметр ***Authorization*** со значением ***Bearer {{token}}***. В переменную ***{{token}}*** Вы будете передавать **ACCESS_TOKEN** из диаграммы состояний **Token Storage** из туториала **Google OAuth 2.0**  
    ```
    {  
        "Authorization": "Bearer {{token}}"  
    }  
    ```

    ![img](en/plugins/google/gmail/img/../../../../../img/get-unread-messages-api-call.png)  
    
    При поступлении заявки с ID сообщения в процесс **Message Info** Вы будете получать детали письма и менять статус письма на “Прочитанное”.  
    
 ### Обработка непрочитанных писем

1. Для того, чтобы каждый раз не создавать вручную заявки для получения деталей письма, Вам необходимо подключить процесс **Message Info** к процессу **Reading**. Это позволит сразу после получения списка непрочитанных писем в процессе **Reading** запускать процесс **Message info** для получения информации о письме.

    1.1. Для этого перейдите в процесс **Reading** 
    
    1.2. После узла **Condition** добавьте узел **Copy task** и подключите к нему процесс **Message Info** для отправки копии заявок cо списком ID писем.

    В поле **Reference** укажите: 

    ```
    {{root.ref}}{{message_id}}
    ```

    Во вкладке **Parameters** добавьте:
    
     ```
    {
    "email": "{{email}}",
    "message_id": "{{message_id}}",
    "token": "{{token}}"
    }   
    ```
    
    ![img](en/plugins/google/gmail/img/../../../../../img/get-message-info.png)  
    
2. Как Вы уже видели в разделе [Получение списка непрочитанных писем](#получение-списка-непрочитанных-писем), заявка со списком писем приходит из Gmail API в виде массива.
 
    Чтобы получить информацию о каждом письме, нам нужно поочередно отправлять по 1 письму из полученого списка в процесс **Message info.**  
    
    2.1. Для этого между узлом **Сondition** и **Сopy Task** cоздайте узел **Сode** для добавления в него небольшого JavaScript-кода, который будет выбирать по 1 письму из списка и отправлять их в процесс **Message info**:  
    
    ```
    if (data.index == undefined)
    {
        data.index = 0;
    } else {
        data.index = data.index+1;
    }
    data.length_list = data.messages.length-1;
    data.message_id = data.messages[data.index].id;
    ```
    
    ![img](en/plugins/google/gmail/img/../../../../../img/setup-code-node.png)
    
    Когда Вы закончите перебор всех писем, заявка автоматически перейдет в узел **Final**. 
    
    2.2. Для того, чтобы после завершения перебора писем заявка переходила в узел **Final**, добавьте после узла **Copy task** узел **Condition** с названием **Messages ended** с условием:```
    {{index}} == {{length_list}}```
    
    где:  
    - **index** - это порядковым номера письма, который передается в процесс **Message info**.  
    - **length_list** - это общее количество писем в списке.
       
    Если текущий порядковый номер письма меньше, чем общее кол-во писем в списке, то заявка проходит снова в узел **Code** и берет следующее письмо, а если порядковым номер больше, чем общее кол-во заявок в списке, то заявка уходит в финальный узел.  
    
    2.2. Подключите узел **Condition** к узлу **Code**, как на изображении ниже.  
      
    ![img](en/plugins/google/gmail/img/../../../../../img/cycle.png)  
  
    Теперь у Вас готов процесс с функциями:  
    - Получение списка с ID непрочитанных писем  
    - Передача каждого отдельного ID сообщения в процесс **Message Info**  
    - Получение информации о письме по его ID с помощью процесса **Message Info**  
  
### Настройка цикла обработки почты  
  
1. Если на Вашем email-адресе появятся новые неотвеченные письма, то в процесс Corezoid они поступят только в том случае, если Вы вручную создадите заявку в процессе **Reading**. При этом нужно каждый раз указывать **email** для вычитки и **ACCESS_TOKEN**. Для автоматизации выгрузки непрочитанных писем создайте процесс с именем **Init**.  

    ![img](en/plugins/google/gmail/img/../../../../../img/create-init-process.png)  
  
2. В процессе **Init** создайте узел **Set Parametеr** c названием **Set email & token** и добавьте в нем два параметра: **email** и **token**.  

    2.1. В параметре **email** передавайте адрес почтового ящика для вычитки.  

    2.2. В параметре **token** укажите путь к параметру заявки процесса, в котором хранится **ACCESS_TOKEN**.  
    Пример:  
    ```
    {  
        "email": "здесь укажите адрес электронной почты",  
        "token": "{{conv[DIAGRAM_ID].ref[REFERENCE].access_token}}"   
    }
    ```
    где:
    - **DIAGRAM_ID** - ID диаграммы состояний **Token Storage**.  
    - **REFERENCE** - референс заявки, в которой находится активный **ACCESS_TOKEN** 
    - **access_token** - параметр заявки, в котором хранится активный **ACCESS_TOKEN**  
      
    ![img](en/plugins/google/gmail/img/../../../../../img/get-credentials.png)  
  
3. Для вызова **Gmail API** все символы кроме латинского алфавита, десятичных цифр и - _ . ! ~ * ' ( ). из email-адреса должны быть преобразованы в юникод UTF-8 для более компактной передачи данных. Это позволяет серверу с **Gmail API** избегать получение некорректных запросов от пользователей.  

    Для этого Вы можете использовать метод _encodeURIComponent_ из JavaScript для кодирования символов в UTF-8.  
    
    3.1 Добавьте узел **Code** и укажите в нем следующий код:    
    
    ```
    data.encoded_email = encodeURIComponent(data.email);  
    ```
    
    Тем самым создается новый параметр с именем **encoded_email**, в котором символ “@” будет заменен на “%40”. Это позволит беспрепятственно отправить запрос в **Gmail API**.  
      
    ![img](en/plugins/google/gmail/img/../../../../../img/encode-email.png)  
      
    После того, как в заявке получен **ACCESS_TOKEN** и преобразован **email**, эти данные нужно передать в процесс вызова **Gmail API**.  
  
4. В процессе **Init** добавьте узел **Copy task** и подключите к нему процесс **Reading** для передачи заявки.  
  
    В поле **Reference** укажите:
        
    ```
    {{root.task_id}}  
    ```
    
    В разделе **Parameters** добавьте:  
    ```
    {  
        "email": "{{encoded_email}}",  
        "token": "{{token}}"  
    }  
    ```
    ![img](en/plugins/google/gmail/img/../../../../../img/call-reading-process.png)      

5. Настройте с какой периодичностью Вы планируете вызывать процесс **Reading** для получения непрочитанных писем. Для этого добавьте нам нужно будет добавить 2 узла, которые будут отвечать за циклический вызов процесса. 

    5.1. Добавьте узел **Delay** и назовите его **Wait**. Сразу после узла **Wait** добавье еще один узел **Copy Task**, и назовите его **Recursion**.  
 
    На рисунке ниже Вы можете видеть как взаимодействует логика для циклического движения заявки по процессу. 

    ![img](en/plugins/google/gmail/img/../../../../../img/read-wait-logic.png)  
  
    5.2. В узле Wait нажмите на ***Additionally*** и поставьте галочку напротив **Limit the time of the task in the node**. В появившемся поле для ввода задайте значение таймера, например, поставьте 10 минут.  
  
    ![img](en/plugins/google/gmail/img/../../../../../img/add-delay-node.png)  
  
    5.3. Для циклического движения заявки в процессе каждые 10 минут, подключите в узле **Сopy task** отправку копии заявки в этот же **Init**. Рекурсивный подход позволит увидеть в финальном узле общее кол-во запросов на вычитку почты за выбранный период времени.  
  
    В поле **Reference** укажите: 
    ```
    {{root.task_id}},  
    ```
    
    В разделе **Parameters** добавьте:  
    ```
    {  
        "email": "{{email}}"  
    }  
    ```
     
    ![img](en/plugins/google/gmail/img/../../../../../img/init-recursion.png)  
  
    Процесс **Init** для отправки сигнала на вычитку почты готов.   
  
    Перейдите в режим **View**, нажмите кнопку **New Task** и отправьте пустую заявку.
       
    Отправленная Вами заявка обеспечит работу процесса по выгрузке неотвеченных писем в процесс **Message Info**. На Ваше усмотрение Вы можете строить дальнейшие логики обработки почты с использованием Corezoid.  
  
**Поздравляем! Вы научились создавать процессы с вызовом Gmail API**  
  
  