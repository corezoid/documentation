# p2p


Шаблон процесса p2p - [Процесс 11719](https://www.corezoid.com/admin/edit_conv/11719)

Он доступн у Вас в папке `"Examples - LiqPay - p2p"`.

Для того чтобы начать работу с ним, клонируйте шаблон следующим образом
![](../img/mandrill_copy_conveyor.png)

Вставьте Ваш `private key` из LiqPay в поле `Secret key`:
![](../img/LiqPay_insert_key.png)

Сгенерируйте callback URL для возврата из LiqPay результатов платежа
![](../img/LiqPay_callback_url.png)

нажав на кнопку "Create callback url"
![](../img/LiqPay_callback_url_generate.png)

Вы получаете URL и в поле `Path to task_id` нужно указать значение `obj_id`
![](../img/LiqPay_callback_url_copy.png)

После чего скопировать URL и вставить его в поле `callback` логики API, который находится в zoid'е `Call api LiqPay`.
![](../img/LiqPay_callback_url_insert.png)

Перейдите в режим `dashboard` и нажмите кнопку `Add task` - чтобы добавить тестовую заявку.

![](../img/mandrill_dashboard.png)

В открывщейся форме укажите параметры платежа и нажмите "Send task".

Процесс подготовлен к использованию из других процессов через логику RPC. Список исходящих параметров:
*   В случае ошибки
    *   `err_description` - описание ошибки
    *   `err_code` - код ошибки
*   В случае успеха
    *   `result` - будет содержать значение `success`

