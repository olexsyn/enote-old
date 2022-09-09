# Віртуальне оточення

    python3 -m venv .env
    source .env/bin/activate

каталоги Python зазвичай:

```
'/home/user/www/site/cgi-bin/test' - каталог скрипта
'/usr/lib/python310.zip'
'/usr/lib/python3.10'
'/usr/lib/python3.10/lib-dynload'
'/usr/local/lib/python3.10/dist-packages'
'/usr/lib/python3/dist-packages'
```

каталоги Python з вірт. оточенням **/work/www/site/.venv**  
(останні два пішло, новий додався): 

```
'/home/user/www/site/cgi-bin/test' - каталог скрипта
'/usr/lib/python310.zip'
'/usr/lib/python3.10'
'/usr/lib/python3.10/lib-dynload'
'/home/user/www/site/.venv/lib/python3.10/site-packages'
```

## Почитати

- `2018_Python_Tricks_-_Dan-Bader.pdf` p.271
- {% include a.htm url="https://docs.python-guide.org/dev/virtualenvs/" text="Pipenv & Virtual Environments" %} (EN)
- {% include a.htm url="https://python-scripts.com/virtualenv" text="Виртуальная среда Python – Основы" %}
  - задача **pyvenv** - разделять модули  `sudo apt install python3-venv`
  - задача **pyenv** – разделять версии Python
    - {% include a.htm url="https://github.com/pyenv/pyenv" text="pyenv - Simple Python version management" %}
    - {% include a.htm url="https://khashtamov.com/ru/pyenv-python/" text="Pyenv: удобный менеджер версий python" %}
    - {% include a.htm url="https://habr.com/ru/post/203516/" text="PyEnv - Менеджер версий python" %} Habr
    - {% include a.htm url="https://ru.hexlet.io/blog/posts/ispolzovanie-neskolkih-versiy-python-na-unix-podobnyh-operatsionnyh-sistemah" text="Использование нескольких версий Python на unix-подобных операционных системах" %} 


## Установка pyenv

- {% include a.htm url="https://github.com/pyenv/pyenv#installation" %}
- {% include a.htm url="https://github.com/pyenv/pyenv/blob/master/COMMANDS.md" %}

Должны быть установлены curl, git и gcc

На странице проекта ссылка на автоматический инсталлятор {% include a.htm url="https://github.com/pyenv/pyenv-installer" %}

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

#### Примечание для Linux Lite

При попытке инсталлировать необходимую версию Питона через **pyenv**, оказалось, не хватает модулей CPython. Пришлось его ставить...

    $ git clone https://github.com/python/cpython

Потом делаем это:

```
sudo apt install build-essential python-dev python-setuptools python-pip python-smbus
sudo apt install libncursesw5-dev libgdbm-dev libc6-dev
sudo apt install zlib1g-dev libsqlite3-dev tk-dev
sudo apt install libssl-dev openssl
sudo apt install libffi-dev

cd ~/cpython
./configure
make
sudo make altinstall
```
Ждем долго и нудно, в итоге получаем свежайшую версию Питона в `/usr/local/bin/` и нужные модули для установки различных версий Питона через **pyenv**.

Получил варнинги:

WARNING: The directory '/home/olex/.cache/pip/http' or its parent directory is not owned by the current user and the cache has been disabled. Please check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.

WARNING: The directory '/home/olex/.cache/pip' or its parent directory is not owned by the current user and caching wheels has been disabled. check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.

Просто создал эти директории: `.cache/pip/http`

## После установки

Смотрим, что мы можем установить:

    pyenv install --list

И устанавливаем, например:

    pyenv install 3.7.2

<span class="info">i</span> Простой способ заставить выполнятся скрипты на нужной версии Питона - создать файл **.python-version** в директории скриптов в котором прописать необходимую версию, например: 
```
3.7.2
```
