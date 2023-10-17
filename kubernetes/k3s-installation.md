# Установка k3s

[K3S](https://k3s.io) - более легковесный вариант Kubernetes. Список доступных релизов можно посмотреть на странице [https://github.com/k3s-io/k3s/releases](https://github.com/k3s-io/k3s/releases). Рассмотрим процесс установки кластера из одного узла.

## Подготовка

### Скрипт для установки

Для установки достаточно загрузить скрипт для установки [https://get.k3s.io](https://get.k3s.io/), например, с помощью `curl`

```sh
curl https://get.k3s.io -o install.sh
chmod u+x install.sh
```

### Файл конфигурации

По умолчанию при установке будет использоваться файл конфигурации `/etc/rancher/k3s/config.yaml` (подробнее см. [Configuration File](https://docs.k3s.io/installation/configuration#configuration-file))

{% code title="config.yaml" fullWidth="false" %}
```yaml
tls-san:
  - k8s.example.com
  - n1.k8s.example.com
```
{% endcode %}

### Прокси сервер

Если для загрузки образов требуется использовать прокси сервер, его можно указать в файле `/etc/systemd/system/k3s.service.env` (подробнее см. [Configuring an HTTP proxy](https://docs.k3s.io/advanced#configuring-an-http-proxy))

{% code title="k3s.service.env" %}
```ini
HTTP_PROXY=http://your-proxy.example.com:8888
HTTPS_PROXY=http://your-proxy.example.com:8888
NO_PROXY=127.0.0.0/8,10.0.0.0/8,172.16.0.0/12,192.168.0.0/16
```
{% endcode %}

Поскольку файл `/etc/systemd/system/k3s.service.env` перезаписывается в процессе выполнения скрипта установки install.sh, для добавления значений указанныж переменных их нужно определить при запуске процесса установки (см. параграф [Установка](k3s-installation.md#ustanovka))

### Сертификаты

При установке k3s будут сгенерированы необходимые сертификаты. Для создания сертификатов с пользовательскими параметрами можно воспользоваться скриптом [https://github.com/k3s-io/k3s/blob/master/contrib/util/generate-custom-ca-certs.sh](https://github.com/k3s-io/k3s/blob/master/contrib/util/generate-custom-ca-certs.sh) (подробнее см. [Using Custom CA Certificates](https://docs.k3s.io/cli/certificate#using-custom-ca-certificates)). Необходимые параметры можно изменить в скрипте и сгенерировать сертификаты:

```sh
./generate-custom-ca-certs.sh
```

Файлы сертификатов будут записаны в каталог `/var/lib/rancher/k3s/server/tls` . После выполнения скрипта в консоль будет выведено предупреждение:

> For security purposes, you should make a secure copy of the following files and remove them from cluster members:
>
> /var/lib/rancher/k3s/server/tls/intermediate-ca.crt
>
> /var/lib/rancher/k3s/server/tls/intermediate-ca.key
>
> /var/lib/rancher/k3s/server/tls/intermediate-ca.pem
>
> /var/lib/rancher/k3s/server/tls/root-ca.crt
>
> /var/lib/rancher/k3s/server/tls/root-ca.key
>
> /var/lib/rancher/k3s/server/tls/root-ca.pem

Перечисленные файлы необходимо перенести в надежное хранилище

## Установка

После подготовки можно запустить процесс установки

```sh
./install.sh
```

Для определения параметров прокси сервера нужно указать соответствующие переменные

```bash
HTTP_PROXY=http://your-proxy.example.com:8888 \
HTTPS_PROXY=http://your-proxy.example.com:8888 \
NO_PROXY=127.0.0.0/8,10.0.0.0/8,172.16.0.0/12,192.168.0.0/16 \
./install.sh
```

После установки `kubeconfig` будет записан в файл `/etc/rancher/k3s/k3s.yaml`

## Удаление

Для удаления сервера [K3S](https://k3s.io) необходимо запустить скрипт `/usr/local/bin/k3s-uninstall.sh`, созданный в процессе установки:

```bash
/usr/local/bin/k3s-uninstall.sh
```

## Ссылки

[https://docs.k3s.io](https://docs.k3s.io/)
