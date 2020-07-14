# git-issue-lost-changes

Когда мержим `master` в `bad-branch` специально ошибаемся и затираем `good` из `1.txt`

Гит это воспринимает как намеренное действие.

В результате, когда мержим `bad-branch` в `master` конфликта не происходит. Ничего не происходит. Потому что "общий предок" - это как раз коммит после мержа с ошибкой. Для гита - это явно сделанные изменения.

Но по результату мержа `bad-branch` в `master` видим разную историю файла с отслеживанием по переименованию (`--follow`).

#### А где мои изменения?
```
$ git log -- 1.txt
commit 7bf2c33678a611b60091c8a4b7b81b1d48379bf5
Author: Dmitry Klimenko
Date:   Tue Jul 14 14:05:44 2020 +0300

    1
```

#### А почему текущий файл не такой как в последнем коммите в истории?
```
$ git log --follow -- 1.txt
commit 06707cf573500d1b3b4629773b03ad0d51f4f82c
Author: Dmitry Klimenko 
Date:   Tue Jul 14 14:29:00 2020 +0300

    add good to 1

commit 7bf2c33678a611b60091c8a4b7b81b1d48379bf5
Author: Dmitry Klimenko 
Date:   Tue Jul 14 14:05:44 2020 +0300

    1
```
