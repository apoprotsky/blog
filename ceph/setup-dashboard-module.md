# Настройка модуля Dashboard

## Установка пакетов

```shell
apt install ceph-mgr-dashboard
```

## Настройка модуля Dashboard

Включение модуля

```
ceph mgr module enable dashboard
```

Создание самоподписанного сертификата

```
ceph dashboard create-self-signed-cert
```

Добавление пользователей

```
ceph dashboard ac-user-create admin -i password_file administrator
```

## Ссылки

[https://forum.proxmox.com/threads/nautilus-activating-ceph-dashboard.85961](https://forum.proxmox.com/threads/nautilus-activating-ceph-dashboard.85961)\
[https://docs.ceph.com/en/latest/mgr/dashboard](https://docs.ceph.com/en/latest/mgr/dashboard)
