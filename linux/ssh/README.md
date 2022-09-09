# SSH

- [Застосування](#usage)
- [Помилки](#errors)
  - [SSH не заходить на потрібний пост з помилкою: Unable to negotiate with...](#err_unable_to_negotiate_with)

## Застосування {#usage}

{% include cl.htm cmd="ssh user@66.225.228.206" %}

или в **/home/user/.ssh/config**

```
Host a
    Hostname admin.mail-ua
    User mailua
Host root
    Hostname 66.225.228.206
    User root
Host user
    Hostname 66.225.228.206
```

и тоді так:

{% include cl.htm cmd="ssh a
ssh root
ssh user" %}

## Помилки {#errors}

### SSH не заходить на потрібний пост з помилкою: Unable to negotiate with...  {#err_unable_to_negotiate_with}

{% include cl.htm cmd="ssh SOMEHOSTNAME"
out="Unable to negotiate with 1.2.3.4 port 22: no matching host key type found. Their offer: ssh-rsa,ssh-dss" %}

#### Рішення:

[askubuntu.com](https://askubuntu.com/questions/836048/ssh-returns-no-matching-host-key-type-found-their-offer-ssh-dss)

Версія OpenSSH, включена в 16.04, відключає `ssh-dss`. Є акуратна сторінка зі застарілою інформацією, яка містить цю проблему: http://www.openssh.com/legacy.html  
Коротше кажучи, вам слід додати опцію `-oHostKeyAlgorithms=+ssh-dss` до SSH-команди:

{% include cl.htm cmd="ssh -oHostKeyAlgorithms=+ssh-dss root@192.168.8.109" %}

Ви також можете додати шаблон хоста у свій **~/.ssh/config**, щоб вам не потрібно було щоразу вказувати ключовий алгоритм:

```
Host SHORTNAME
  HostName 1.2.3.4
  HostKeyAlgorithms=+ssh-dss
```

Це має додаткову перевагу, що вам не потрібно вводити IP-адресу. Замість цього ssh розпізнає хост SHORTNAME і знатиме, куди підключитися. Звичайно, замість нього можна використовувати будь-яку іншу назву.

`UPD`: Остання версія OpenSSH вимикає RSA, якщо зараз ви зіткнетеся з помилкою, вам слід використовувати `+ssh-rsa` замість `+ssh-dss`.

`UPD2`: Спробував поставити глобально, теж працює:

```
HostKeyAlgorithms=+ssh-dss

Host SHORTNAME
  HostName 1.2.3.4
```
Але, можливо, не всім хостам прописаним у **~/.ssh/config** це потрібно
