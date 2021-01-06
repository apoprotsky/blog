# Настройка shell пользователя

В `UNIX` системах как правило принято, что настройки оболочки \(`shell`\) пользователя определяются в файле `/etc/passwd`. В `macOS` он присутствует, но изменение настроек в нем не оказывает влияние. Для настройки используется команда `dscl`. ****Команда `dscl` предназначена для конфигурирования параметров `Directory Service` - базы данных учетных записей, групп и пр. В нашем случае - локальных учетных записей.

## Настройка оболочки пользователя

### **Получение текущей оболочки**

```text
dscl . -read /Users/root UserShell
```

### **Установка оболочки пользователя**

```text
dscl . -change /Users/root UserShell /bin/sh /bin/csh
```

## Ссылки

[https://superuser.com/questions/626391/change-the-sudo-su-shell](https://superuser.com/questions/626391/change-the-sudo-su-shell)[https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/dscl.1.html](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/dscl.1.html)

