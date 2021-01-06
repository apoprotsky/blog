# Установка XOrg и Gnome

Очень часто псевдопакеты тянут за собой множество зависимостей, которые не востребованы и  которые не очень-то хотелось устанавливать. Поэтому, немного поэкмпериментировав, решил собрать минимальный список пакетов для запуска окружения `Gnome` на `FreeBSD 10`.

## Минимальный набор пакетов для установки XOrg

```text
pkg install xorg-minimal
```

Или еще меньше

```text
pkg install xorg-server
pkg install xorg-init
pkg install xf86-input-keyboard
pkg install xf86-input-mouse
```

Для установки на виртуальной машине `VMWare`

```text
pkg install xf86-video-vmware
pkg install xf86-input-vmmouse
```

Для установки на виртуальной машине `VirtualBox`

```text
pkg install virtualbox-ose-additions
```

## Минимальный набор пакетов для установки окружения Gnome

```text
pkg install gnome3-lite
```

Или еще меньше

```text
pkg install dbus
pkg install gdm
pkg install gnome-shell-extensions
pkg install gnome-tweak-tool
pkg install gnome-terminal 
```

## Не критичные для работы пакеты, но на них есть ссылки

```text
pkg install gnome-power-manager
```

## Полезные программы

```text
pkg install doublecmd
pkg install chromium
pkg install firefox
pkg install libreoffice
pkg install ru-libreoffice
pkg install pidgin
pkg install gimp
pkg install blender
pkg install gnome-system-monitor
```

## Украшательства

```text
pkg install gnome-backgrounds
pkg install numix-theme
```

## Проблемы и решения

#### Проблема

Сообщение об ошибке `gkbd-keyboard-display failed` при выборе опции в меню выбора языка ввода `Show keyboard layout`

#### Решение

Установить недостающую библиотеку `libgnomekbd`

```text
pkg install libgnomekbd
```

#### Проблема

Не изменяется язык интерфейса Gnome и приложений

#### Решение

Измените языковые настройки в файле `/usr/local/etc/gdm/locale.conf`

