# Синхронизация форка с основным проектом

## Добавление источника основного проекта

Для начала необходимо добавить еще один внешний источник. Делается один раз для рабочей копии.

```csharp
git remote add upstream https://git.example.com/group/project.git
```

## Синхронизация изменений

Получение данных нового источника.

```csharp
git fetch upstream
```

Объединение изменений с рабочей копией.

```csharp
git merge upstream/master
```

После объединения изменений можно опубликовать изменения основного проекта в `origin` форка \(принимается, что `origin` - это название источника форка в локальной копии\) .

```csharp
git push origin master
```

## Ссылки

[http://chriscase.cc/2011/02/syncing-a-forked-git-repository-with-a-master-repositorys-changes](http://chriscase.cc/2011/02/syncing-a-forked-git-repository-with-a-master-repositorys-changes)

