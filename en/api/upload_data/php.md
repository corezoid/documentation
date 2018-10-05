# PHP

SDK for the work Corezoid.com

https://github.com/corezoid/sdk-php

Example of loading request into the process ID 1635:

```PHP
include_once('Corezoid.php'); // Corezoid class

// API user settings
$api_login = '1234';
$api_secret = 'Iw5N12MYleOULxdfMH43SK9ZAmjPyFKtdhToiL38xIBz6ecdZxW';

// Init Corezoid class
$CZ = new Corezoid($api_login, $api_secret);

// Add new task
$ref1    = time().'_'.rand();
$task1   = array('phone' => '+380989055434', 'nick' => 'Test Nick');
// ID process
$process_id = 1635;

$CZ->add_task($ref1, $process_id, $task1);

// Send all tasks to Corezoid.com
$res = $CZ->send_tasks();
```