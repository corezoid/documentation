# Библиотеки JavaScript

1.   [Работа с датой/временем (moment.js)](#moment)
2.   [SHA1 функция](#sha1)
3.   [HMAC-SHA функция](#sha)
4.   [MD5 функция](#md5)
5.   [Base64](#base64)
6.  [AES](#aes)
7.  [DES](#des)
8.  [3DES](#3des)
9.  [Moment-timezone](#moment-timezone)
10. [Sha512](#sha512)


## Работа с датой/временем {#moment}

Для работы с датой/временем используется библиотека [moment.js](http://momentjs.com)

1. Пример получения текущей даты/времени в формате 'MMMM Do YYYY, h:mm:ss a':
```js
require("libs/moment.js");
data.datetime = moment().format('MMMM Do YYYY, h:mm:ss a');
```
результат выполнения кода:
```js
{
     "datetime": "February 3rd 2017, 9:47:28 am"
}
```

2. Пример получения текущей даты/времени в формате **unixtime**
```js
require("libs/moment.js");
data.datetime = moment().unix();
```
результат выполнения кода:
```js
{
     "datetime": 1486115313
}
```

3. Пример получения текущей даты/времени в формате 'YYYY-MM-DD HH:mm:ss' с добавлением 4 минут в часовм поясе UTC +5 час:
```js
require("libs/moment.js");
data.datetime = moment().utcOffset('+05:00').add(4, 'minutes').format('YYYY-MM-DD HH:mm:ss');
```
результат выполнения кода:
```js
{
    "datetime": "2017-02-03 14:33:54"
}
```


С полным списком возможностей библиотеки Вы можете ознакомиться на сайте [moment.js](http://momentjs.com)

> **local** поддерживается только **en**

## SHA1 функция {#sha1}

```js
require("libs/sha1.js");
data.sha1 = CryptoJS.SHA1(data.variable).toString();
```

`data.variable` - параметр заявки, который нужно хешировать (параметр "data.variable" использован для примера)

Результатом вызова функции будет новый параметр заявки `sha1`, содержащий хеш переданной строки (значения параметра), вычисленный по алгоритму sha1.

## HMAC-SHA функция {#sha}

```js
require("libs/hmac-sha256.js");
var hash = CryptoJS.HmacSHA256("Message", "secret");
data.hashInHex = hash.toString(CryptoJS.enc.Hex);
```

## MD5 функция {#md5}

```js
require("libs/md5.js");
data.md5 = CryptoJS.MD5(data.variable).toString();
```
`data.variable` - параметр заявки, который нужно хешировать (параметр "data.variable" использован для примера)

Результатом вызова функции новый параметр заявки `md5`, содержащий хеш переданной строки (значения параметра), вычисленный по алгоритму md5.

## Base64 {#base64}

### Кодирование
```js
require("libs/base64.js");
var wordArray = CryptoJS.enc.Utf8.parse(data.words);
data.base64 = CryptoJS.enc.Base64.stringify(wordArray);
```
`data.words` - переменная заявки, которую нужно перевести в формат base64 (параметр "data.words" использован для примера)

Результатом вызова функции будет новый параметр заявки `base64`, содержащий значение параметра  "words" в формате base64.

### Декодирование

```js
require("libs/base64.js");
var words = CryptoJS.enc.Base64.parse(data.base64);
data.parsedStr = words.toString(CryptoJS.enc.Utf8);
```
`data.base64` - параметр заявки в формате base64 (параметр "data.base64" использован для примера)

Результатом вызова функции будет новый параметр заявки `parsedStr`, содержащий раскодированное значение параметра "base64".


## AES {#aes}

### Кодирование

```js
require("libs/aes.js");
data.encrypted = CryptoJS.AES.encrypt(data.message, data.password).toString();
```
`data.message` - параметр заявки, который нужно зашифровать;

`data.password` - параметр заявки, содержащий пароль.

> параметры "data.message" и "data.password" использованы для примера

Результатом вызова функции будет новый параметр заявки `encrypted`, содержащий зашифрованное значение параметра "variable" по алгоритму AES.

### Декодирование
```js
require("libs/aes.js");
data.decrypted = CryptoJS.AES.decrypt(data.encrypted, data.password).toString(CryptoJS.enc.Utf8);
```
`data.encrypted` - параметр заявки, который нужно расшифровать;

`data.password` - параметр заявки, содержащий пароль.

> параметры "data.encrypted" и "data.password" использованы для примера

Результатом вызова функции будет новый параметр заявки `decrypted`, содержащий расшифрованное значение параметра "encrypted" по алгоритму AES.

## DES {#des}

### Кодирование
```js
require("libs/tripledes.js");
data.encrypted = CryptoJS.DES.encrypt(data.message, data.password).toString();
```
`data.message` - параметр заявки, который нужно зашифровать;

`data.password` - параметр заявки, содержащий пароль.

> параметры "data.message" и "data.password" использованы для примера

Результатом вызова функции будет новый параметр заявки `encrypted`, содержащий зашифрованное значение параметра "variable" по алгоритму DES.

### Декодирование
```js
require("libs/tripledes.js");
data.decrypted = CryptoJS.DES.decrypt(data.encrypted, data.password).toString(CryptoJS.enc.Utf8);
```
`data.encrypted` - параметр заявки, который нужно расшифровать;

`data.password` - параметр заявки, содержащий пароль.

> параметры "data.encrypted" и "data.password" использованы для примера

Результатом вызова функции будет новый параметр заявки `decrypted`, содержащий расшифрованное значение параметра "encrypted" по алгоритму DES.

## 3DES {#3des}

### Кодирование
```js
require("libs/tripledes.js");
data.encrypted = CryptoJS.TripleDES.encrypt(data.message, data.password).toString();
```
`data.message` - параметр заявки, который нужно зашифровать;

`data.password` - параметр заявки, содержащий пароль.

> параметры "data.variable" и "data.password" использованы для примера

Результатом вызова функции будет новый параметр заявки `encrypted`, содержащий зашифрованное значение параметра "variable" по алгоритму 3DES.

### Декодирование
```js
require("libs/tripledes.js");
data.decrypted = CryptoJS.TripleDES.decrypt(data.encrypted, data.password).toString(CryptoJS.enc.Utf8);
```

`data.encrypted` - параметр заявки, который нужно расшифровать;

`data.password` - параметр заявки, содержащий пароль.

> параметры "data.encrypted" и "data.password" использованы для примера

Результатом вызова функции будет новый параметр заявки `decrypted`, содержащий расшифрованное значение параметра "encrypted" по алгоритму 3DES.



## Moment-timezone


```js
 require("libs/moment-timezone.js");
 data.date = moment().tz('Europe/Kiev').format("DD-MM-YYYY HH:mm:ss");
```


## Sha512


```js
 require("libs/sha512.js"); 
 data.sha512 = CryptoJS.SHA512("test").toString();
```

