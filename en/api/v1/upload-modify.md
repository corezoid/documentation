# Creating and modifying data

 * [Create](#сreate)
 * [Modify](#modify)


## Create

Adding new tasks to a Corezoid process.

*   [Basic description](#basic-description)
*   Examples:
    *   [Erlang](#erlang)
    *   [Java](#java)
    *   [PHP](#php)
    *   [BASH](#bash)
    *   [PYTHON](#python)

## Basic description

Let us add (create) three tasks to "Test" process (process ID 1234) from API user (user ID 13000).

> By default, all new tasks fall into the starting node called "Login"(node_id="n10221").

URL example for making request: https://api.corezoid.com/api/1/json/13000/{GMT_UNIXTIME}/{SIGNATURE}

**Request**

```json
 {
    "ops":[
    {
        "ref":"130605ref1",
        "type":"create",
        "obj":"task",
        "conv_id":"1234",
        "data":{
            "phone":"380501234561",
            "card":"4134000011112221"
            }
    },
    {
        "ref":"130605ref2",
        "type":"create",
        "obj":"task",
        "conv_id":"1234",
        "data":{
            "phone":"380661234562",
            "card":"4134000011112222"
            }
    },
    {
        "ref":"130605ref3",
        "type":"create",
        "obj":"task",
        "conv_id":"1234",
        "data":{
            "phone":"380661234563",
            "card":"4134000011112223"
            }
    }
    ]
}
```

`ref` - external (for process) task identifier, optional parameter. Used in case of reverse interaction with a system that created request.

**Response** in case of successful operation:

```json
{
    "request_proc":"ok",
    "ops":[
        {
            "ref":"130605ref1",
            "obj":"task",
            "obj_id":"t71001",
            "proc":"ok"
        },
        {
            "ref":"130605ref2",
            "obj":"task",
            "obj_id":"t71012",
            "proc":"ok"
        },
        {
            "ref":"130605ref3",
            "obj":"task",
            "obj_id":"t71013",
            "proc":"ok"
        }
    ]
}
```

### Erlang

```Erlang
-module(test).

-export([send_to_conv/6, test/0]).

test() ->
%Conveyor url
  ConvUrl = "https://api.corezoid.com",

%Conveyor ID
  ConvId = <<"5555">>,

%API user login (Conveyor with given ConvId has to be shared for this API user)
  ApiUser = "555",

%API User Secret Key
  ApiSecret = <<"qjVXiaXFazSCtIvMTjW29cZbPkzeYUzCzGmmrcJtIIj2eqceUm">>,

  % unique task reference, optional
  Reference = integer_to_binary(random:uniform(100000000)),

% Data for processing
  Data = <<"{\"phone\":\"client_phone\",\"name\":\"client_name\"}">>,

  {ok, Response} = send_to_conv(ConvUrl, ConvId, ApiUser, ApiSecret, Reference, Data),

  Response.


-spec send_to_conv(ConvUrl, ConvId, ApiUser, ApiSecret, Reference, Data) -> {ok, binary()} when
  ConvUrl :: list(),
  ConvId :: binary(),
  ApiUser :: list(),
  ApiSecret :: binary(),
  Reference :: binary(),
  Data :: binary().

send_to_conv(ConvUrl, ConvId, ApiUser, ApiSecret, Reference, Data) ->

% start inets app for httpc client
  application:start(inets),

%Time in unix format
  Time = erlang:integer_to_binary(unixtime()),

%Request with one element (could be many) in ops array for task create
  Request = <<"{\"ops\":[{\"ref\":\"", Reference/binary, "\",\"type\":\"create\",\"obj\":\"task\",\"conv_id\":\"",
  ConvId/binary, "\",\"data\":", Data/binary, "}]}">>,

%Generate Sign
  Sign = create_sign(<<Time/binary, ApiSecret/binary, Request/binary, ApiSecret/binary>>),
  Url = ConvUrl ++ "/api/1/json/" ++ ApiUser ++ "/" ++ binary_to_list(Time) ++ "/" ++ binary_to_list(Sign),

  {ok, {{_, 200, _}, _, Response}} = httpc:request(post, {Url, [], "application/octet-stream", Request}, [{timeout, 10000}], []),

  {ok, Response}.


unixtime()->
  {A,B,_C} = now(),
  A*1000000 + B.

create_sign(Bin) ->
  list_to_binary(list_to_hexstr(binary_to_list(crypto:hash(sha, Bin)))).


list_to_hexstr([]) ->
  [];
list_to_hexstr([H|T]) ->
  to_hex(H) ++ list_to_hexstr(T).


to_hex(N) when N < 256 ->
  [hex(N div 16), hex(N rem 16)].


hex(V) ->
  if
    V < 10 ->
      $0 + V;
    true ->
      $a + (V - 10)
  end.
```

### Java

SDK for the work middleware.biz

https://github.com/corezoid/sdk-java/releases/tag/v2.1

```Java

import com.corezoid.sdk.entity.CorezoidMessage;
import com.corezoid.sdk.entity.RequestOperation;
import com.corezoid.sdk.utils.HttpManager;
import java.util.Arrays;
import java.util.List;
import java.util.Random;
import net.sf.json.JSONObject;
import org.apache.http.HttpException;

public class MiddlewareCreate {

    public static void main(String[] args) {
        try {
            // ID process
            String conv_id = "15476";
            // API user settings
            String apiLogin = "5965";
            String apiSecret = "VjKyfIuVAFOGGZwLLFfkHvrTPFUTBBP6E3A8596vIj5jiwqSsK";
            // Create task
            JSONObject data = new JSONObject()
                    .element("phone", "+380989055434")
                    .element("nick", "Test Nick");
            String ref = "test" + System.currentTimeMillis() + new Random(System.currentTimeMillis()).nextInt(1000);
            RequestOperation operation = RequestOperation.create(conv_id, ref, data);
            // Add task to list
            List<RequestOperation> ops = Arrays.asList(operation);
            // Build a Message
            ConveyorMessage message = ConveyorMessage.request(apiSecret, apiLogin, ops);
            // Create HttpManager instance
            HttpManager http = new HttpManager();
            // Send all tasks to Middleware
            String answer = http.send(message);
        } catch (HttpException ex) {
            System.out.println(ex);
        }
    }

}

```
### PHP

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

### BASH

Example create task with reference ref_32353 to the process 1664 from the user ID 985:

```bash
#!/bin/sh

CONV_ID=1664
CONV_USER_ID='985'
CONV_USER_PASS='***'
API_URL='https://api.corezoid.com/api/1/json/'
TIME=$(echo $(($(date +%s))))

JSON="{
    \"ops\" : [{
    \"ref\" : \"ref_32353\",
   \"type\" : \"create\",
    \"obj\" : \"task\",
\"conv_id\" : ${CONV_ID},
   \"data\" : {\"key1\" : \"val1\", \"key2\" : \"val2\"}
  }]
}"

SIGNATURE=$(echo -n "${TIME}${CONV_USER_PASS}${JSON}${CONV_USER_PASS}" | openssl dgst -sha1 | awk '{print $NF}')

REQ=$(curl --silent -XPOST ${API_URL}${CONV_USER_ID}/${TIME}/${SIGNATURE} --data "${JSON}")
echo "Result: ${REQ}"
```

### PYTHON

SDK for the work Corezoid.com

https://github.com/MaxBondar/Corezoid

This module helps you sending and modifying tasks to Corezoid processes.

```PYTHON
from Corezoid import Corezoid

# Insert Corezoid Process credentials
# Learn more about credentials: https://doc.corezoid.com/en/interface/access_management.html
API_KEY    = '<INSERT API KEY>' 
API_SECRET = '<INSERT API SECRET>'
PROCESS_ID = '<INSERT PROCESS ID>'

# Initialize Corezoid SDK
c = Corezoid(API_KEY, API_SECRET, PROCESS_ID)

# There are 2 methods available: send and modify tasks.
# Learn more about Corezoid API: https://doc.corezoid.com/en/api/upload_data/

# Send a new task to Corezoid process
def send_task(ref, data):
    # ref: string. Can be a custom value. By default it's a timestamp. 
    # data: JSON. Must be a JSON object.

    c.create_task(ref, data)

# Modify an existing task by ref at Corezoid process
def modify_task(ref, data):
    # ref: string. Can be a custom value. By default it's a timestamp. 
    # data: JSON. Must be a JSON object.

    c.modify_task(ref, data)
```


## Modify

Modifying task by it's reference (sending callback).

Request with reference `130605ref1` sent for processing to http://my.api.com/getData via [api](external_api.md) method. Processing of request on api.my.com resource is made asynchronously, therefore after processing process receives callback with results.
**Example of callback to a process:**

Example of URL to which requests will be sent to: https://api.corezoid.com/api/1/json/13000/{GMT_UNIXTIME}/{SIGNATURE}


```json
{
    "ops":[
        {
            "type":"modify",
            "obj":"task",
            "ref":"130605ref1",
            "conv_id":"1234",
            "data":{
                "checkedClient":"true"
            }
        }
    ]
}
```

**Response of a process after callback successfully accepted:**
```json
{
    "request_proc":"ok",
    "ops":[
        {
            "ref":"130605ref4",
            "proc":"ok"
        }
    ]
}
```

`"checkedClient":"true"` - this parameter and its value will be added to the request with `130605ref1` reference. After that request leaves standby mode in `api_callback` and proceeds to perform the following logics.

### Example of change task with the help of SDK Java

SDK for the work middleware.biz

https://github.com/corezoid/sdk-java/releases/tag/v2.1

```Java

import com.corezoid.sdk.entity.CorezoidMessage;
import com.corezoid.sdk.entity.RequestOperation;
import com.corezoid.sdk.utils.HttpManager;
import java.util.Arrays;
import java.util.List;
import net.sf.json.JSONObject;
import org.apache.http.HttpException;

public class MiddleWareModify {

    public static void main(String[] args) {
        try {
            // ID process
            String conv_id = "15476";
            // API user settings
            String apiLogin = "5965";
            String apiSecret = "VjKyfIuVAFOGGZwLLFfkHvrTPFUTBBP6E3A8596vIj5jiwqSsK";
            // ModifÏy task
            String ref = "test141874099180849";
            JSONObject data = new JSONObject()
                    .element("phone", "+380989055434")
                    .element("ref", "test141874099180849");
            RequestOperation operation = RequestOperation.modifyRef(conv_id, ref, data);
            // Add task to list
            List<RequestOperation> ops = Arrays.asList(operation);
            // Build a Message
            ConveyorMessage message = ConveyorMessage.request(apiSecret, apiLogin, ops);
            // Create HttpManager instance
            HttpManager http = new HttpManager();
            // Send all tasks to Middleware
            String answer = http.send(message);
        } catch (HttpException ex) {
            System.out.println(ex);
        }
    }

}

```


