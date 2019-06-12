# Copy the folder to company

[Process template](https://admin.corezoid.com/folder/conv/103787) to copy to your account.

>Example assumes that:

* there's a process and dashboard in the copied folder

* new folder, process and dashboard need to be renamed (for example, name it as a clinet)

* Called process needs to return process id located in new folder е

## Description of parameters

* `login` - user login with API type
* `secret_key` - user key with type of API******
* `copy_folder_id` - copied folder id
* `company_id` - company id, where folder should be copied.

If the folder's  copy is needed in "MY COREZOID", value of company_id = **null**
* `to_folder_id` - folder where another folder should be copied 
* `folder_new_name` - new folder name 
* `dashboard_new_name` - new dashboard name
* `process_new_name` - new process name 

`folder_new_name`, `dashboard_new_name`, `process_new_name` processes can be replaced by other parameters of current request.

For example,

"{{folder_new_name}}" -> "{{public_key}}"

"{{dashboard_new_name}}" -> "Dashboard-{{public_key}}"

"{{process_new_name}}" -> "Process-{{public_key}}"


>****** `secret_key` is required to be added in every node with Corezoid API calling:

>Additionally -> Sign the request by secret key

![](img/secret_key.png)
