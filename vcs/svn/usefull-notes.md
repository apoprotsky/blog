# Полезные заметки

При работе с файлами, частом из изменении, изменении файлов группой авторов возникает потребность в отслеживании этих изменений, необходимость "откатиться" на прошлую версию файла, узнать кто и когда внес конкретные правки и т.д. На решение подобных задач направлены [системы управления версиями](https://ru.wikipedia.org/wiki/%D0%A1%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0_%D1%83%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F_%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D1%8F%D0%BC%D0%B8). Одна из популярных систем - [Subversion](https://subversion.apache.org/), сокращенно SVN.

## Получение справки по командам

```bash
svn help
svn help commit
```

## Управление атрибутами

### Установка прав выполнения

```bash
svn propset svn:executable path/file
```

### Добавление файлов и каталогов в список игнорирования

```bash
svn propset svn:ignore "*.sublime*"
svn propedit svn:ignore .
```

## Ссылки

[https://ru.wikipedia.org/wiki/Система\_управления\_версиями](https://ru.wikipedia.org/wiki/%D0%A1%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0_%D1%83%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F_%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D1%8F%D0%BC%D0%B8)  
[https://ru.wikipedia.org/wiki/Subversion](https://ru.wikipedia.org/wiki/Subversion)  
[https://subversion.apache.org](https://subversion.apache.org/)  
[http://stackoverflow.com/questions/86049/how-do-i-ignore-files-in-subversion](http://stackoverflow.com/questions/86049/how-do-i-ignore-files-in-subversion)

