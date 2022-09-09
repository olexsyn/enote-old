# Підключення до GitHub через SSH

[docs.githubh](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh)

Використовуючи протокол SSH, ви можете підключатися та аутентифікуватися на віддалених серверах і сервісах. За допомогою ключа SSH ви можете підключитися до GitHub без вказівок імені користувача або пароля, коли відправляєте локальні правки в репозиторії GitHub.

Перед створенням ключа SSH перевірте каталог **~/.ssh**, можливо, у вас вже є наявні ключі. Зазвичай імена відкритих (публічних) ключів мають розширення `.pub`

## Створення нового ключа SSH

[docs.github](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

Якщо у вас немає пари відкритих і закритих ключів або ви не хочете використовувати будь-які доступні для підключення до GitHub, то згенеруйте новий ключ SSH, використовуючи свій e-mail як ідентифікатор:

{% include cl.htm cmd='ssh-keygen -t ed25519 -C "nickname@example.com"' %}

> Примітка. Якщо ви використовуєте застарілу систему, яка не підтримує алгоритм Ed25519, використовуйте:  
> `$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

У вас буде запитано ім'я файлу (треба вводити повний шлях, бажано у `/home/user/.ssh/`), та пароль

{% include cl.htm cmd='ssh-keygen -t ed25519 -C "nickname@example.com"'
out="Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/user/.ssh/id_ed25519): /home/user/.ssh/nickname
Created directory '/home/user/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/user/.ssh/nickname
Your public key has been saved in /home/user/.ssh/nickname.pub
The key fingerprint is:
SHA256:DALKyEu8zwu08jo3gPcUVjmrjOXpP4wSUy27jQHNKf5 nickname@example.com
The key's randomart image is:
..." %}

## Додавання нового ключа SSH до вашого облікового запису GitHub

[docs.github](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

Скопіюйте вміст файлу **~/.ssh/nickname.pub** у буфер обміну. Це ваш публічний ключ SSH.

У верхньому правому куті сторінки вашого GitHub-аккаунта натисніть на фотографію свого профілю, потім натисніть «Settings».

На бічній панелі налаштувань користувача натисніть «SSH и GPG keys».

У полі «Title» додайте описову позначку для нового ключа.

Вставте з буферу обміну зміст свого публічного ключа у поле «Key», та натисніть «Add SSH key».

Якщо буде запропоновано, підтвердіть пароль свій пароль на GitHub.


## Зміна протоколу передачі даних репозиторію з HTTP на SSH


[help.github](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories#switching-remote-urls-from-https-to-ssh)


Відкрийте термінал. Перейдіть у свій свій локальний git-проект:

{% include cl.htm cmd="cd path/to/REPOSITORY" %}

Отримайте список посилань на віддалений репозиторій.
Перевіяємо, що поточний протокол **HTTP**: `origin  https:// ...`, який ми хочемо змінити:

{% include cl.htm cmd="git remote -v"
out="&gt; origin  https://github.com/USERNAME/REPOSITORY.git (fetch)
&gt; origin  https://github.com/USERNAME/REPOSITORY.git (push)" %}

Змінюємо протокол:

{% include cl.htm cmd="git remote set-url origin git@github.com:USERNAME/REPOSITORY.git" %}

Перевіряемо, що протокол змінився на **GIT**: `origin  git@github.com:`

{% include cl.htm cmd="git remote -v"
out="&gt; origin  git@github.com:USERNAME/REPOSITORY.git (fetch)
&gt; origin  git@github.com:USERNAME/REPOSITORY.git (push)" %}

Якщо раніше вводилася безпечна фраза-пароль, її може буде запитано під час команд `git pull`, `git push` і `git merge`.


## Додавання вашого ключа SSH до ssh-agent

[docs.github.com](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

Якщо ви не хочете вводити свою парольну фразу щоразу, коли надсилаєте або отримуєте дані з серверу GitHub, ви можете додати його до агента SSH, який керує вашими ключами і запам’ятовує вашу парольну фразу.

Запустіть ssh-агент у фоновому режимі.

{% include cl.htm cmd='eval "$(ssh-agent -s)"'
out='&gt; Агент pid 59566' %}

Додайте свій закритий (приватний) ключ SSH до ssh-agent:

{% include cl.htm cmd='ssh-add ~/.ssh/nickname' %}

