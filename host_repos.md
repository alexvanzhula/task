[< Вернуться к содержанию](./readme.md)

Так как Git это распределённая СКВ вы можете работать не только с локальными но и с внешними репозиториеми.

Удалённые репозитории представляют собой версии вашего проекта, сохранённые на внешнем сервере.

Для работы с внешними репозиториями используйте:

```
git remote [<options>]
```
Если вы с клонировали репозитории через http URL то у вас уже имеется ссылка на внешний. В другом случае вы можете добавить её с помощью

```
git remote add [<options>] <name> <adres>
```
Вы можете тут же извлечь внешние ветки с помощью -f, --fetch (вы получите имена и состояние веток внешнего репозитория). Вы можете настроить репозитории только на отправку или получение данных с помощью --mirror[=(push|fetch)]. Для получения меток укажите --tags.

Для просмотра подключённых внешних репозиториев используйте git remote без аргументов или git remote -v для просмотра адресов на отправку и получение данных от репозитория.

Для отслеживания веток используйте git branch -u <rep/br> где rep это название репозитория, br название внешней ветки, а branch название локальной ветки. Либо
```
 git branch --set-upstream local_br origin/br 
 ```
 для того что бы указать какая именно локальная ветка будет отслеживать внешнюю ветку.

Когда ваша ветка отслеживает внешнюю вы можете узнать какая ветка (локальная или внешняя) отстаёт или опережает и на сколько коммитов. К примеру если после коммита вы не выполняли git push то ваша ветка будет опережать внешнюю на 1 коммит. Вы можете узнать об этом выполнив git branch -vv, но прежде выполните git fetch [remote-name] (--all для получения обновления со всех репозиториев) что бы получить актуальные данные из внешнего репозитория. Для отмены отслеживания ветки используйте
``` 
git branch --unset-upstream [<local_branch>].
```
Для загрузки данных с внешнего репозитория используйте git pull [rep] [branch]. Если ваши ветки отслеживают внешние, то можете не указывать их при выполнение git pull. По умолчанию вы получите данные со всех отслеживаемых веток.

Для загрузки веток на новую ветку используйте 
```
git checkout -b <new_branch_name> <rep/branch>.
```
Для отправки данных на сервер используйте

```
git push [<rep>] [<br>]
```
где rep это название внешнего репозитория, а br локальная ветка которую вы хотите отправить. Также вы можете использовать такую запись git push origin master:dev. Таким образом вы выгрузите вашу локальную ветку master на origin (но там она будет называется dev). Вы не сможете отправить данные во внешний репозитории если у вас нет на это прав. Также вы не сможете отправить данные на внешнюю ветку если она опережает вашу (в общем то отправить вы можете используя -f, --forse в этом случае вы перепишите историю на внешнем репозитории). Вы можете не указывать название ветки если ваша ветка отслеживает внешнюю.

Для удаления внешних веток используйте

```
git push origin --delete branch_name
```

Для получения подробной информации о внешнем репозитории (адреса для отправки и получения, на что указывает HEAD, внешние ветки, локальные ветки настроенные для git pull и локальные ссылки настроенные для git push)

```
git remote show <remote_name>
```

Для переименования названия внешнего репозитория используйте

```
git remote rename <last_name> <new_name>
```

Для удаления ссылки на внешний репозитории используйте

```
git remote rm <name>
```