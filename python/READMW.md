# Виртуальное окружение

- `2018_Python_Tricks_-_Dan-Bader.pdf` p.271
- [Pipenv & Virtual Environments](https://docs.python-guide.org/dev/virtualenvs/) (EN)
- [Виртуальная среда Python – Основы](https://python-scripts.com/virtualenv)
- [Виртуальные среды](https://codecamp.ru/documentation/python/868/virtual-environments)
- [pyenv - Simple Python version management](https://github.com/pyenv/pyenv)
  - [https://khashtamov.com/ru/pyenv-python/](Pyenv: удобный менеджер версий python)
  - [PyEnv - Менеджер версий python](https://habr.com/ru/post/203516/) Habr
  - [Использование нескольких версий Python на unix-подобных операционных системах](https://ru.hexlet.io/blog/posts/ispolzovanie-neskolkih-versiy-python-na-unix-podobnyh-operatsionnyh-sistemah) 


## Установка pyenv

- https://github.com/pyenv/pyenv#installation
- https://github.com/pyenv/pyenv/blob/master/COMMANDS.md

Должны быть установлены curl, git и gcc

На странице проекта ссылка на автоматический инсталлятор https://github.com/pyenv/pyenv-installer

Ссылка на запуск инсталлятора:

    $ curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash

Возможно, понадобится дописать в конец указанных файлов (.bash_profile / .bashrc) ...

### Manjaro

**.bash_profile**

```bash
export PATH="$HOME/.pyenv/bin:$PATH"
if command -v pyenv 1>/dev/null 2>&1; then
  eval "$(pyenv init -)"
fi
```
и выполнить

    $ exec $SHELL

### Linux Lite

**.bashrc**

```bash
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
and finally, restart your shell:
```
и выполнить

    $ exec $SHELL

