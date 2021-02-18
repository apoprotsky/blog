# Локализация каталогов

В случае наличия в каталоге файла `.localized` `Finder` попытается отобразить локализованное имя. Локализация производится посредством файлов `SystemFolderLocalizations.strings`.  
Файл русской локализации располагается в каталоге `/System/Library/CoreServices/SystemFolderLocalizations/ru.lproj/`.

## Добавление своих строк

Запускаем окно терминала  
Делаем копию файла `SystemFolderLocalizations.strings`, например в каталог Документы:

```bash
cp /System/Library/CoreServices/SystemFolderLocalizations/ \
  ru.lproj/SystemFolderLocalizations.strings ~/Documents
```

Переходим в каталог Документы и преобразовываем файл в `xml` формат:

```bash
cd ~/Documentsplutil -convert xml1 -e xml SystemFolderLocalizations.strings
```

Преобразованный файл будет сохранен с именем `SystemFolderLocalizations.xml`. Открываем `SystemFolderLocalizations.xml` в любом текстовом редакторе и добавляем желаемые строки. Преобразовываем файл из фрмата `xml` в plist:

```bash
plutil -convert binary1 -e binary SystemFolderLocalizations.xml
```

Преобразованный файл будет сохранен под именем `SystemFolderLocalizations.binary`. Заменяем оригинальный файл своим. Для копирования необходимы права root-а:

```bash
sudo cp ~/Dociments/SystemFolderLocalizations.binary \
  /System/Library/CoreServices/SystemFolderLocalizations/ \
  ru.lproj/SystemFolderLocalizations.strings
```

Перезапускаем `Finder`:

```bash
killall Finder
```

Теперь чтобы локализовать название каталоге остается создать файл `.localized`

```bash
cd /some/dir
touch .localized
```

