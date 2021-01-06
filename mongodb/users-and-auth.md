# Пользователи и авторизация

После установки в `MongoDB` отсутствуют учетные записи пользователей. СУБД может работать в двух режимах: с авторизацией доступа и без. По умолчанию авторизация отключена, но даже с включенной авторизацией пока нет ни одного пользователя разрешены подключения с `localhost`.  
Для включения режима авторизации можно использовать ключ `--auth` или добавить в файл конфигурации строку `auth = true`.  
Для отключения опции авторизации можно использовать ключ `--noauth` или добавить в файл конфигурации строку `noauth = true`.

## Создание учетной записи администратора

```text
use admin;
db.createUser({
    user: "root",
    pwd: "password",
    roles: [ { role: "root", db: "admin" } ]
});
```

## Создание учетной записи пользователя для одной базы данных

```text
use test;
db.createUser({
    user: "user",
    pwd: "password",
    roles: [ { role: "readWrite", db: "test" } ]
});
```

## Удаление учетной записи

```text
use test;
db.dropUser("user");
```

## Просмотр списка учетных записей пользователей в базе данных

```text
use test;
db.getUsers();
```

## Добавление ролей учетной записи пользователя

```text
use test;
db.grantRolesToUser(
    "user",
    [ { role: "readWrite", db: "logs" } ]
); 
```

## Изменение пароля учетной записи

```text
use test;
db.changeUserPassword( "user", "new_password" );
```

## Авторизация

```text
use test;
db.auth( "user", "password" );
```

## Ссылки

[http://docs.mongodb.org](http://docs.mongodb.org/)

