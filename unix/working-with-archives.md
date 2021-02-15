# Работа с архивами

В unix-системах присутствует огромное множество консольных утилит и программ для работы с архивами, многие из которых обладают приличным набором параметров. Поскольку все сие великолепие запомнить и держать в голове сложно - пишем шпаргалку.

## Упаковка файлов

### Упаковка файлов в tar.gz

```bash
tar -cvzf file.tar.gz /path
```

## Распаковка файлов

### Распаковка tar.gz файлов

```bash
tar -xvzf file.tar.gz
```

### Распаковка файлов gz

```bash
gunzip file.log.gz
```

После выполнения команды файл `file.log.gz` будет заменен распакованным `file.log`

## Ссылки

[http://pingvinus.ru/answers/844](http://pingvinus.ru/answers/844)  
[http://www.electronick.org.ua/articles/linux/kak\_sozdat\_arhiv\_tar\_gz\_v\_luboy\_versii\_linux](http://www.electronick.org.ua/articles/linux/kak_sozdat_arhiv_tar_gz_v_luboy_versii_linux)

