# Getting an access to API

1.  [App registration and getting RSA Private key](#app-registration-and-getting-rsa-private-key)
2.  [Login and password](#Login-and-password)
3.  [Certificate](#certificate)

## App registration and getting RSA Private key

Create new application and don't forget to mark API's you need to get access to. Otherwise you'll have to register new application..

After app creation you will see the window with RSA PRIVATE KEY:
![](../img/visa/private_rsa.png)

It' s necessary to copy the received private key and save it in file.You will need it for getting VISA API.

Key content starts and ends the following way
```
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```

## Login and password

![](../img/visa/user_id.png)


## Certificate

Certificate is required to download and rename in .txt extension file. You will need file content in order to set API running.

![](../img/visa/visa_cert.png)

It is required to copy the whole file content
```
-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----
```
