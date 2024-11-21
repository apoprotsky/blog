# Работа с контейнером p12

## Просмотр информации

Для просмотра содержимого контейнера `p12` можно воспользоваться следующей командой

```
openssl pkcs12 -in in.p12 -info
```

## Экспорт сертификатов и ключей&#x20;

Для экспорта клиентского сертификата можно воспользоваться следующей командой

```sh
openssl pkcs12 -in in.p12 -out out.crt -clcerts -nokeys
```

Для экспорта закрытого ключа можно воспользоваться следующей командой

```shell
openssl pkcs12 -in in.p12 -out out.key -nocerts -noenc
```

## Работа с устаревшими алгоритмами шифрования

Если при выполнении команд встречаются ошибки наподобие следующей

> Error outputting keys and certificates 40CF050602000000:error:0308010C:digital envelope routines:inner\_evp\_generic\_fetch:unsupported:crypto/evp/evp\_fetch.c:355:Global default library context, Algorithm (RC2-40-CBC : 0), Properties ()

можно попробовать добавить ключ `-legacy`

## Ссылки

[https://stackoverflow.com/questions/15144046/converting-pkcs12-certificate-into-pem-using-openssl](https://stackoverflow.com/questions/15144046/converting-pkcs12-certificate-into-pem-using-openssl)
