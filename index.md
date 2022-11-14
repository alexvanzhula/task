[< Вернуться к содержанию](./readme.md)

Надеюсь вы поняли, как выглядит жизненный цикл git репозитория. Теперь разберём как вы можете управлять индексом и файлами в вашем git репозитории.

Индекс — промежуточное место между вашим прошлым коммитом и следующим. Вы можете добавлять или удалять файлы из индекса. Когда вы делаете коммит в него попадают данные из индекса, а не из рабочей области.

Что бы просмотреть индекс, используйте git status.

Что бы добавить файлы в индекс используйте </br></br>

```
git add [<опции>]
```

Полезные параметры команды git add:

-f, --force — добавить также игнорируемые файлы</br>
-u, --update — обновить отслеживаемые файлы</br></br>

Что бы удалить файлы из индекса вы можете использовать 2 команды git reset и git restore.
git-restore — восстановит файлы рабочего дерева.
git-reset — сбрасывает текущий HEAD до указанного состояния.
По сути вы можете добиться одного и того же с помощью обеих команд.

Что бы удалить из индекса некоторые файлы используйте: </br></br>

```
git restore --staged <file>
```

таким образом вы восстановите ваш индекс (или точнее удалите конкретные файлы из индекса), будто бы git add после последнего коммита не выполнялся для них. С помощью этой команды вы можете восстановить и рабочую директорию, что бы она выглядела так, будто бы после коммита не выполнялось никаких изменений. Вот только эта команда имеет немного странное поведение — если вы добавили в индекс новую версию вашего файла вы не можете изменить вашу рабочую директорию, пока индекс отличается от HEAD. Поэтому вам сначала нужно восстановить ваш индекс и только потом рабочую директорию. К сожалению сделать это одной командой не возможно так как при передаче обеих аргументов (git restore -SW) не происходит ничего. И точно также при передаче -W тоже ничего не произойдет если файл в индексе и HEAD разный. Наверное, это сделали для защиты что бы вы случайно не изменили вашу рабочую директорию. Но в таком случае почему аргумент -W передаётся по умолчанию? В общем мне не понятно зачем было так сделано и для чего вообще была добавлена эта команда. По мне так reset справляется с этой задачей намного лучше, да и еще и имеет более богатый функционал так как может перемещать индекс и рабочую директорию не только на последний коммит но и на любой другой.

Но собственно разработчики рекомендуют для сброса индекса использовать именно git restore -S . Вместо git reset HEAD .

С помощью git status вы можете посмотреть какие файлы изменились но если вы также хотите узнать что именно изменилось в файлах то воспользуйтесь командой:</br></br>

```
git diff [<options>]
```

таким образом выполнив команду без аргументов вы можете сравнить ваш индекс с рабочей директорией. Если вы уже добавил в индекс файлы, то используйте git diff --cached что бы посмотреть различия между последним коммитом (или тем который вы укажите) и рабочей директории. Вы также можете посмотреть различия между двумя коммитами или ветками передав их как аргумент. Пример: git diff 00656c 3d5119 покажет различия между коммитом 00656c и 3d5119.
