# Служба Spotlight

Служит для быстрого поиска данных. Поиск осуществляется не только по названиям файлов, но и по их содержимому, а также по данным интернет-сервисов, например [Wikipedia](https://wikipedia.com). Окно поиска вызывается комбинацией клавиш `Ctrl + Пробел`.Для ускорения поиска служба постоянно индексирует содержимое носителей информации, запуская при этом несколько процессов `mdworker`, которые довольно часто отъедают приличную часть процессорного времени и подгружают дисковую подсистему. Если Вы не используете функции `Spotlight`, то отключить службу можно следующей командой

```bash
sudo launchctl unload \
  -w /System/Library/LaunchDaemons/com.apple.metadata.mds.plist
```

Возвратить работу службы можно следующей командой

```bash
sudo launchctl load \
  -w /System/Library/LaunchDaemons/com.apple.metadata.mds.plist
```

## Ссылки

[http://osxdaily.com/2011/12/10/disable-or-enable-spotlight-in-mac-os-x-lion/](http://osxdaily.com/2011/12/10/disable-or-enable-spotlight-in-mac-os-x-lion/)
