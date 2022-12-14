# 14. Перемещение указателей

***

Перемещение указателей

В книге Pro git приводится очень хороший пример того как вы можете управлять вашим репозиторием поэтому я тоже буду придерживается его. Представите что Git управляет содержимым трех различных деревьев. Здесь под “деревом” понимается “набор файлов”.
В своих обычных операциях Git управляет тремя деревьями:

**HEAD — Снимок последнего коммита, родитель следующего**

**Индекс — Снимок следующего намеченного коммита**

**Рабочий Каталог — Песочница**

Собственно git предоставляет инструменты для манипулировании всеми тремя деревьями. Далее будет рассмотрена команда git reset, позволяющая работать с тремя деревьями вашего репозитория.

Используя различные опций этой команды вы можете:


**--soft — Cбросить только HEAD**

**--mixed — Cбросить HEAD и индекс**

**--hard — Cбросить HEAD, индекс и рабочий каталог**


Под сбросить понимается переместить на указанный коммит. По умолчанию выполняется --mixed.

Примеру 1. Вы сделали 3 лишних коммита каждый из которых приносит маленькие изменения и вы хотите сделать из них один, таким образом вы можете с помощью git reset --soft переместить указатель HEAD при этом оставив индекс и рабочий каталог нетронутым и сделать коммит. В итоге в вашей истории будет выглядеть так, что все изменения произошли в одном коммите.

Пример 2. Вы добавили в индекс лишние файлы и хотите их от туда убрать. Для этого вы можете использовать git reset **HEAD <files...>**. Или вы хотите что бы в коммите файлы выглядели как пару коммитов назад. Как я уже говорил ранее вы можете сбросить индекс на любой коммит в отличий от git restore который сбрасывает только до последнего коммита. Только с опцией mixed вы можете применить действие к указанному файлу!

Пример 3. Вы начали работать над новой фичей на вашем проекте, но вдруг работодатель говорит что она более не нужна и вы в порыве злости выполняете git reset --hard возвращая ваш индекс, файлы и HEAD к тому моменту когда вы ещё не начали работать над фичей. А на следующей день вам говорят, что фичу всё таки стоит запилить. Но что же делать? Как же переместится вперёд ведь вы откатили все 3 дерева и теперь в истории с помощью git log их не найти. А выход есть — это журнал ссылок git reflog. С помощью этой команды вы можете посмотреть куда указывал HEAD и переместится не только вниз по истории коммитов но и вверх. Этот журнал является локальным для каждого пользователя.

В общем думаю вы сможете придумать намного больше примеров чем я. В заключение скажу, что с помощью git reset можно творить магию…



## [< Вернуться к содержанию](./readme.md)