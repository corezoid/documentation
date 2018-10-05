# JavaScript library

1.   [Work with date/time (moment.js)](#moment)
2.   [SHA1 function](#sha1)
3.   [HMAC-SHA function](#sha)
4.   [MD5 function](#md5)
5.   [Base64](#base64)
6.  [AES](#aes)
7.  [DES](#des)
8.  [3DES](#3des)

## Work with date/time {#moment}

In order to work with date/time there's a library [moment.js](http://momentjs.com)

Example of getting current date/time in 'Month:Day:Year: Do YYYY, h:mm:ss a':
```js
require("libs/moment.js");
data.datetime = moment().format('MMMM Do YYYY, h:mm:ss a');
```

Example of getting current date/time in unixtime:
```js
require("libs/moment.js");
data.datetime = moment().unix();
```

The whole list of possibilities of the library is available on website [moment.js](http://momentjs.com)

> **local** supported only **en**

## SHA1 function {#sha1}

```js
require("libs/sha1.js");
data.sha1 = CryptoJS.SHA1(data.variable).toString();
```

`data.variable` - task parameter, that is needed to hash ("data.variable" parameter is used for example)

Function call result will be new `sha1` task parameter that contains hash of the passed line (parameter's value),  calculated according to the sha1 algorithm.
 
## HMAC-SHA function {#sha}

```js
require("libs/hmac-sha256.js");
var hash = CryptoJS.HmacSHA256("Message", "secret");
data.hashInHex = hash.toString(CryptoJS.enc.Hex);
```

## MD5 function {#md5}

```js
require("libs/md5.js");
data.md5 = CryptoJS.MD5(data.variable).toString();
```
`data.variable` - task parameter that is needed to ba hashed ("date.variable" parameter is used for example)

Result of function call is new `md5` task parameter, that contains hash of the passed line (parameter value), calculated by md5 algorithm.

## Base64 {#base64}

### Encoding
```js
require("libs/base64.js");
data.base64 = CryptoJS.enc.Base64.stringify(data.words);
```
`data.words` - task's variable, that is needed to convert to "base64" format ("data.words" parameter is used for example)

Result of function call is new `base64` task parameter that contains value of "words" parameter in base64 format.

### Decoding

```js
require("libs/base64.js");
data.words = CryptoJS.enc.Base64.parse(data.base64);
```
`data.base64` - tasks parameter in base64 format ("data.base64" parameter is used for example)

Result of function call is new `words` task parameter that contains decoded value of "base64" parameter.


## AES {#aes}

### Encoding

```js
require("libs/aes.js");
data.encrypted = CryptoJS.AES.encrypt(data.message, data.password).toString();
```
`data.message` - tasks parameter that is needed to be encrypted;

`data.password` - task parameter that contains the password.

> "data.message" and "data.password" parameters are used for example

Function call result will be new parameter of `encrypted` task that contains encrypted value of "variable" parameter by AES algorithm.

### Decoding
```js
require("libs/aes.js");
data.decrypted = CryptoJS.AES.decrypt(data.encrypted, data.password).toString(CryptoJS.enc.Utf8);
```
`data.encrypted` - task parameter that is needed to be decrypted;

`data.password` - task parameter that contains password.

>"data.encrypted" and "data.password" parameters are used for example

Function call result will be new parameter of `decrypted` task that contains decrypted value of "encrypted" parameter with AES algorithm.

## DES {#des}

### Encoding
```js
require("libs/tripledes.js");
data.encrypted = CryptoJS.DES.encrypt(data.message, data.password).toString();
```
`data.message` - tasks parameter that is needed to be encrypted;

`data.password` - task parameter that contains the password.

>"data.message" and "data.password" are used for example

Result of functions call will be the new parameter of `encrypted` task that contains encrypted value for "message" parameter by DES algorithm.

### Decoding
```js
require("libs/tripledes.js");
data.decrypted = CryptoJS.DES.decrypt(data.encrypted, data.password).toString(CryptoJS.enc.Utf8);
```
`data.encrypted` - tasks parameter that needed to be decrypted;

`data.password` - tasks parameter that contains password.

>"data.DESencrypted" and "data.password" parameters are used for example

Result of functions call will be new `decrypted` task parameter that contains decrypted value of "encrypted" parameter by DES algorithm.

## 3DES {#3des}

### Encoding
```js
require("libs/tripledes.js");
data.encrypted = CryptoJS.TripleDES.encrypt(data.message, data.password).toString();
```
`data.message` - tasks parameter that is needed to be encrypted

`data.password` - tasks parameter that contains password

>"data.variable" and "data.password" are used for example

Result of functions call  will be new parameter of `encrypted` task that contains encrypted value for "message" parameter by 3DES algorithm.

### Decoding
```js
require("libs/tripledes.js");
data.decrypted = CryptoJS.TripleDES.decrypt(data.encrypted, data.password).toString(CryptoJS.enc.Utf8);
```
`data.encrypted` - tasks parameter that needed to be decrypted

`data.password` -  tasks parameter that contains password.

>"data.DES3encrypted" and "data.password" parameters are used for example

Result of functions call will be new `decrypted` task parameter that contains decrypted value of "encrypted" parameter by 3DES algorithm.
