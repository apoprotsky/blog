---
description: Overlay network
---

# Nebula

## Сертификаты

Сначала необходимо создать корневой сертификат

```c
./nebula-cert ca -duration 87600h -name "Orion-Media, LLC" \
    -out-crt ca.crt -out-key ca.key
```

Далее с создаем сертификаты узлов сети и подписываем их с помощью корневого сертификата

```c
./nebula-cert sign -ca-crt ca.crt -ca-key ca.key -ip 10.10.10.1/24 -name server \
    -out-crt server.crt -out-key server.key -groups linux,server
```

## Файл конфигурации

```yaml
pki:
  ca: ca.crt
  cert: server.crt
  key: server.key

static_host_map:
  10.10.10.1: [server.om.ua:4242]

lighthouse:
  am_lighthouse: true
  hosts:
  - 10.10.10.1

listen:
  host: 0.0.0.0
  port: 4242

tun:
  disabled: false
  dev: tun0

firewall:
  outbound:
    - port: any
      proto: any
      host: any
  inbound:
    - port: any
      proto: any
      host: any
```

Для корректного функционирования сети должен присутствовать хотя бы один узел с функцией `lighthouse`. На других узлах маяк необходимо указать в списке `static_host_map` а также в списке `lighthouse.hosts`

## Запуск

```shell
nebula -config config.yml
```

## Ссылки

[https://www.defined.net/nebula/quick-start](https://www.defined.net/nebula/quick-start/#/)
