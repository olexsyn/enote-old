# Git

- [GitHub](github)
  - [Jekyll конструктор](github/pages/jekyll)
- [Книга Pro Git](#progit)

## TODO!

### клонувати репозиторій

{% include cl.htm cmd="git clone git@github.com:NICKNAME/REP.git" %}

Також можна змінювати назву директорії проекту локально, налаштування репозиторію та сам локальний репозиторій не злетять - всі ці речі зберігаються в директорії `.git`, за назвою директорії проекту git не стежить, важливі лише зміни самих файлів у робочій директорії.

А взагалі можна відразу клонувати в потрібну вам директорію, на кшталт `git clone https://site.com site_from_github`

### перегляд віддалених репозиторіїв

{% include cl.htm cmd="git remote"
out="origin" %}

Если вы клонировали репозиторий, то увидите как минимум `origin` -- имя по умолчанию, которое Git дает серверу, с которого производилось клонирование. Можно также указать ключ `-v`, чтобы просмотреть адреса для чтения и записи, привязанные к репозиторию:

{% include cl.htm cmd="git remote -v"
out="origin	git@github.com:olexsyn/e-note.git (fetch)
origin	git@github.com:olexsyn/e-note.git (push)"
%}

[подробнее...](https://git-scm.com/book/ru/v2/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%A0%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D1%83%D0%B4%D0%B0%D0%BB%D1%91%D0%BD%D0%BD%D1%8B%D0%BC%D0%B8-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F%D0%BC%D0%B8)

### добавить отдаленный репозиторий и присвоить ему имя (shortname)

{% include cl.htm cmd="git remote add SHORTNAME URL" %}

{% include cl.htm cmd="git remote add e-note git@github.com:olexsyn/e-note.git" %}

Теперь вместо указания полного пути мы можем использовать 'e-note'.

### получение изменений с сервера

{% include cl.htm cmd="git fetch origin" %}

Команда `git fetch` забирает данные в ваш локальный репозиторий, но не сливает их с какими-либо вашими наработками и не модифицирует то, над чем вы работаете в данный момент. Вам необходимо вручную слить эти данные с вашими, когда вы будете готовы.

Команда `git pull`, как правило, извлекает (fetch) данные с сервера и автоматически пытается слить (merge) их с кодом, над которым вы в данный момент работаете.

## отправка изменений на сервер

Когда вы хотите поделиться своими наработками, вам необходимо отправить их в удаленный репозиторий.

{% include cl.htm cmd="git push REMOTE-NAME BRANCH-NAME" %}

Чтобы отправить вашу ветку main на сервер origin (клонирование обычно настраивает оба этих имени автоматически), вы можете выполнить следующую команду для отправки ваших коммитов:

{% include cl.htm cmd="git push origin main" %}


### Сокращенный вывод статуса

`-s` или `--short`

{% include cl.htm cmd="git status -s"
out=" M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt
" %}

В выводе два столбца: в левом - статус, в правом - (не)модифицирован

- `??` - новые неотслеживаемые файлы
- <code>A&middot;</code> - файлы добавленные в отслеживаемые
- <code>&middot;M</code> - модифицирован и НЕ проиндексирован
- <code>M&middot;</code> - модифицирован и проиндексирован
- `MM` - модифицирован, проиндексирован и еще раз модифицирован, т.е. на данный момент у него есть изменения которые попадут в коммит и те которые не попадут


{% include cl.htm cmd="git add file1.ext file2.ext ..." %}

{% include cl.htm cmd="git add --all" %}

## Коммит

{% include cl.htm cmd="git commit -m 'Commit comment'" %}

### Добавить файл(ы) в последний коммит

Сначала добавляем в индекс файлы, которые необходимо присоединить к последнему коммиту, затем выполнить команду `commit`:

{% include cl.htm cmd="git add --all
git commit --amend --no-edit" %}

- `--amend` - при использовании этого ключа, на самом деле удаляется последний коммит и создается новый. Поэтому нельзя выполнять `--amend` для коммитов, которые уже были отправлены на удаленный репозиторий (для которых был выполнен `git push`).
- `--no-edit` - позволяет оставить текущей комментарий к коммиту без изменений

Если необходимо также изменить и комментарий, то:

{% include cl.htm cmd="git commit -m 'New commit comment' --amend" %}

### Просмотр истории коммитов

{% include cl.htm cmd="git log
git log --stat"%}


#### TODO!


`git commit -m "description" filename.ext` | коммит только одного файла


#### Просмотр индексированных и неиндексированных изменений

{% include cl.htm cmd="git diff
git diff --staged
git diff --cached
" %}

#### Выбор программы для сравнения

Посмотреть, что уже установлено, и что можно можно установить:

{% include cl.htm cmd="git difftool --tool-help" %}

Установить для git программу сравнения, например, _meld_

{% include cl.htm cmd="git difftool --tool=meld" %}

#### Принудительно обновить отдаленный репозиторий:

{% include cl.htm cmd="git push -f origin master" %}

<span class="warn">!</span> Но, следует понимать, что на сервере затрутся все изменения в файлах, которые были сделаны после последнего `git push`, даже если ты отправляешь всего один файл.

## <a name="progit"></a> Книга Pro Git

[Pro Git book](https://git-scm.com/book/ru/v2)

- [Запись изменений в репозиторий](https://git-scm.com/book/ru/v2/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%97%D0%B0%D0%BF%D0%B8%D1%81%D1%8C-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D0%B9-%D0%B2-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B9)
- [Игнорирование файлов](https://git-scm.com/book/ru/v2/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%97%D0%B0%D0%BF%D0%B8%D1%81%D1%8C-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D0%B9-%D0%B2-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B9#r_ignoring) см. также [.gitignore templates](https://github.com/github/gitignore)
- [Удаление больших объектов из истории](https://git-scm.com/book/ru/v2/Git-%D0%B8%D0%B7%D0%BD%D1%83%D1%82%D1%80%D0%B8-%D0%A3%D1%85%D0%BE%D0%B4-%D0%B7%D0%B0-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B5%D0%BC-%D0%B8-%D0%B2%D0%BE%D1%81%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85#r_removing_objects)
- [Работа с отдаленными репозиториями](https://git-scm.com/book/ru/v2/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%A0%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D1%83%D0%B4%D0%B0%D0%BB%D1%91%D0%BD%D0%BD%D1%8B%D0%BC%D0%B8-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F%D0%BC%D0%B8)


## Другие ссылки

- [Изучаем команды pull и push](https://monsterlessons.com/project/lessons/git-izuchaem-komandy-pull-i-push)
- [7 советов по повышению производительности](https://nuancesprog.ru/p/5142/)
- [Очистить историю коммитов](https://www.shellhacks.com/ru/git-remove-all-commits-clear-git-history-local-remote/)




