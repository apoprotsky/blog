---
description: Пакетный менеджер Debian / Ubuntu
---

# APT

## Установка пакетов

При установке пакетов также по умолчанию устанавливаются рекомендуемые пакеты. Для отключения установки рекомендуемых пакетов нужно добавить флаг `--no-install-recommends`. Также для исключения установки дополнительно предлагаемых пакетов можно добавить флаг `--no-install-suggests`.

Поведение по умолчанию можно изменить, указав соответствующие настройки в файлах конфигурации `APT`

{% code title="/etc/apt/apt.conf.d/00no-install.conf" %}
```cpp
APT::Get::Install-Recommends "false";
APT::Get::Install-Suggests "false";
```
{% endcode %}

## Ссылки

[https://askubuntu.com/questions/179060/how-to-not-install-recommended-and-suggested-packages](https://askubuntu.com/questions/179060/how-to-not-install-recommended-and-suggested-packages)

