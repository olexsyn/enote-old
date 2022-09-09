# Установка и настройка ProFTPd на Ubuntu Server

<https://www.dmosk.ru/miniinstruktions.php?mini=proftpd-ubuntu> (VPN)

Среди возможностей ProFTPd есть использование виртуальных пользователей с uid системных учетных записей, работа по FTP через TLS, использование виртуальных пользователей с хранением их в отдельном файле или базе данных. Мы рассмотрим настройку всех этих возможностей сервера FTP на примере Linux Ubuntu 18.04 и 20.04. Инструкция также, во многом, подойдет для настройки на Debian.

Подготовка системы
    Правильное время
    Правила фаервола
Базовая настройка
Настройка SSL
Виртуальные пользователи
    Хранение в файле
    Использование MySQL
Настройка прав для пользователей FTP
Настройка логов

## Настройка системы

Подготовим нашу операционную систему для корректной работы сервера FTP. Для этого настроим синхронизацию времени и правила в Firewall.

### 1. Время

Для корректного отображения времени создания файлов, необходимо синхронизировать его с внешним источником. Также необходимо задать корректный часовой пояс. Для этого вводим команду:

    timedatectl set-timezone Europe/Kyiv

* в данном примере мы задаем зону по киевскому времени. Список все доступных зон можно посмотреть командой timedatectl list-timezones.

Устанавливаем chrony:

    apt-get install chrony

... и разрешаем его запуск при загрузке системы:

    systemctl enable chrony

### 2. Брандмауэр

Если в нашем сервере используется фаервол (по умолчанию, он работает с разрешающими правилами), разрешаем порты:

- 20 — для передачи данных.
- 21 — для передачи команд.
- с 60000 по 65535 — набор для пассивного обмена FTP. Данный диапазон может быть любым из свободных, но практика показывает, что данные значения работают стабильнее.

В зависимости от утилиты управления брандмауэром, дальнейшие действия будут отличаться.

#### а) Iptables

Если для управления netfilter мы используем утилиту Iptables, то вводим команду:

    iptables -I INPUT -p tcp --match multiport --dports 20,21,60000:65535 -j ACCEPT

Для сохранения правил можно использовать утилиту:

    apt-get install iptables-persistent
    netfilter-persistent save

#### б) UFW

В ufw команда будет следующей:

    ufw allow 20,21,60000:65535/tcp

## Установка и запуск с базовыми параметрами

Установка ProFTPd на Ubuntu выполняется следующей командой:

    apt-get install proftpd

Открываем основной конфигурационный файл:

    nano /etc/proftpd/proftpd.conf

Редактируем значения для параметров:

    UseIPv6 off

- _где **UseIPv6** — разрешаем или запрещает использование IPv6. Если в нашей среде будет использоваться IP версии 6, то значение данной опции должно быть on_.

Снимаем комментарий для опции PassivePorts и задаем ей следующее значение:

    PassivePorts 60000 65535

- _где **60000 - 65535** — диапазон динамических портов для пассивного режима_.

Разрешаем автозапуск FTP-серверу и перезапускаем его:

    systemctl enable proftpd
    systemctl restart proftpd

Готово — пробуем подключиться к серверу, использую любые FTP-клиенты, например, FileZilla, Total Commander или браузер. В качестве логина и пароля используем учетную запись пользователя Ubuntu.

Если мы хотим использовать выделенную учетную запись для FTP, то создаем ее командой:

    useradd ftpuser -m

Задаем ей пароль:

    passwd ftpuser

Если мы хотим, чтобы учетная запись не могла покидать пределы своей домашней директории, в настройках ProFTPd снимаем комментарий с опции:

    nano /etc/proftpd/proftpd.conf

    DefaultRoot                     ~

И перезапускаем сервис:

    systemctl restart proftpd

## Шифрование при передаче данных

Следующим этапом настроим передачу данных через TLS.

В конфигурационном файле сервера ftp снимаем комментарий для строки:

    nano /etc/proftpd/proftpd.conf

    Include /etc/proftpd/tls.conf

Открываем конфигурационный файл **tls.conf**:

    nano /etc/proftpd/tls.conf

Снимаем комментарии для следующих настроек:

```
TLSEngine                       on
TLSLog                          /var/log/proftpd/tls.log
TLSProtocol                     SSLv23
...
TLSRSACertificateFile           /etc/ssl/certs/proftpd.crt
TLSRSACertificateKeyFile        /etc/ssl/private/proftpd.key
...
TLSOptions                      NoCertRequest EnableDiags NoSessionReuseRequired
...
TLSVerifyClient                 off
...
TLSRequired                     on
```

- _параметр **TLSRequired** можно задать в значение off, если мы не хотим требовать от клиента соединения по TLS_.

Приводим значение для одного из раскомментированных параметров к следующему:

    TLSProtocol                     SSLv23 TLSv1.2

* _мы добавили **TLSv1.2** для поддержки более актуального протокола шифрования. В противном случае, некоторые старые клиенты могут возвращать ошибку **Error in protocol version**_.

Генерируем сертификат:

    openssl req -x509 -nodes -newkey rsa:2048 -keyout /etc/ssl/private/proftpd.key -out /etc/ssl/certs/proftpd.crt -subj "/C=RU/ST=SPb/L=SPb/O=Global Security/OU=IT Department/CN=ftp.dmosk.local/CN=ftp"

* _где **ftp.dmosk.local** — имя сервера в формате FQDN (не принципиально)_.

Перезапускаем ProFTPd:

    systemctl restart proftpd

## Использование виртуальных пользователей

Для безопасности рекомендуется использовать не реальных пользователей системы, а виртуальных. Мы рассмотрим процесс их хранения в файле или базе данных.

### Хранение в файле

Создаем виртуального пользователя командой:

    ftpasswd --passwd --file=/etc/proftpd/ftpd.passwd --name=ftpvirt --uid=33 --gid=33 --home=/var/tmp --shell=/usr/sbin/ nologin

* где: 

- _**/etc/proftpd/ftpd.passwd** — путь до файла, в котором хранятся пользователи;_
- _**ftpvirt** — имя пользователя (логин);_
- _**uid** и **gid** — идентификаторы пользователя и группы системной учетной записи (например, www-data);_
- _**/var/tmp** — домашний каталог пользователя;_
- _**/usr/sbin/nologin** — оболочка, запрещающая локальный вход пользователя в систему._

---

> Это информация из другой статьи (<https://ixnfo.com/nastroyka-proftpd-s-virtualnyimi-polzovatelyami-v-fayle.html>)

После этой команды будет создан файл /etc/proftpd/ftpd.passwd схожей структуры с /etc/passwd.
UID и GID можно указывать любые, желательно кроме 0 (это root) и тех что указаны в /etc/passwd.
Можно также указать UID и GID аналогичные как у пользователя в /etc/passwd, например 33 как у пользователя www-data, чтобы предоставить похожие права к веб файлам и указать домашней директорией /var/www.
Можно создавать пользователей с одинаковыми UID и GID, разными домашними директориями и с учетом что им запрещено выходить выше уровня своей директории (параметр DefaultRoot ~ в конфигурации сервера).

Модуль mod_auth_file требует чтобы доступ к чтению и записи на файл /etc/proftpd/ftpd.passwd был запрещен для всех пользователей, по этому укажем права:

    chmod 640 /etc/proftpd/ftpd.passwd
    chown proftpd:root /etc/proftpd/ftpd.passwd

Иначе будет ошибка при запуске proftpd:

    mod_auth_file/1.0: unable to use world-readable AuthUserFile ‘/etc/proftpd/ftpd.passwd’: Операция не позволена

Создадим файл ftpd.group:

    sudo ftpasswd --group --name=nogroup --file=/etc/proftpd/ftpd.group --gid=60 --member test

Проверим правильность конфигурации:

    sudo proftpd -t

Перезапустим ProFTPd чтобы применить изменения:

    sudo /etc/init.d/proftpd restart

Так как пароли в файле хранятся в шифрованном виде, то менять пароль пользователю можно так:

    sudo ftpasswd --passwd --file=/etc/proftpd/ftpd.passwd --name=test --change-password

Можно заблокировать/разблокировать пользователя (добавляется/убирается символ ! в файле ftpd.passwd перед хешем пароля, тем самым делая невозможным подключение пользователя):

    sudo ftpasswd --passwd --file=/etc/proftpd/ftpd.passwd --name=test2 --lock
    sudo ftpasswd --passwd --file=/etc/proftpd/ftpd.passwd --name=test --unlock

Удалить пользователя можно так:

    sudo ftpasswd --passwd --file=/etc/proftpd/ftpd.passwd --name=test --delete-user

ftpasswd является скриптом написанным на Perl, обычно находится в /usr/sbin/ftpasswd.

---


Открываем конфигурационный файл proftpd:

    nano /etc/proftpd/proftpd.conf

Снимаем комментарий или редактируем опцию (если не сделали это раньше):

    DefaultRoot                     ~

* данная опция говорит о том, что корневой директорией для пользователя будет домашняя директория. Это нужно, чтобы FTP-пользователи не могли выйти за пределы дозволенного и видеть на сервере сайты друг друга.

Создаем дополнительный конфигурационный файл для proftpd:

nano /etc/proftpd/conf.d/virtual_file.conf

```
RequireValidShell off
AuthUserFile /etc/proftpd/ftpd.passwd
AuthPAM off
# LoadModule mod_auth_file.c  # ! у меня эти строки выдавали ошибку, мол alredy loaded
# AuthOrder mod_auth_file.c   # ! и AuthOrder has already be...
```

Перезапускаем сервис FTP-сервера:

systemctl restart proftpd

### Хранение в MariaDB (MySQL)

Настройку разделим на два этапа:

- Установку и настройку СУБД.
- конфигурирование FTP-сервера.

В качестве СУБД будем использовать MariaDB / MySQL.

СУБД

Устанавливаем на Ubuntu СУБД и модуль mysql для ProFTPd:

apt-get install mariadb-server proftpd-mod-mysql

Разрешаем автозапуск сервиса mariadb:

systemctl enable mariadb

Задаем пароль для пользователя root в mysql:

mysqladmin -u root password

Подключаемся к базе данных:

mysql -uroot -p

Создаем базу данных для хранения пользователей:

> CREATE DATABASE proftpd DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;

* в данном примере мы создали базу данных proftpd.

Создаем таблицу в созданной базе:

> CREATE TABLE `proftpd`.`users` (
`userid` VARCHAR( 32 ) NOT NULL ,
`passwd` CHAR( 41 ) NOT NULL ,
`uid` INT NOT NULL ,
`gid` INT NOT NULL ,
`homedir` VARCHAR( 255 ) NOT NULL ,
`shell` VARCHAR( 255 ) NOT NULL DEFAULT '/usr/sbin/nologin',
UNIQUE (`userid`)           
) ENGINE = MYISAM CHARACTER SET utf8 COLLATE utf8_general_ci;

* данной командой мы создаем таблицу users в базе данных proftpd.

Создаем пользователя mariadb для доступа к таблицам базы proftpd:

> GRANT SELECT ON proftpd.* TO proftpd_user@localhost IDENTIFIED BY 'proftpd_password';

* мы создали пользователя proftpd_user с паролем proftpd_password, которому дали право подключаться только с локального сервера.

Добавляем FTP-пользователя в таблицу:

> INSERT INTO `proftpd`.`users` VALUES ('sqluser', ENCRYPT('sqlpassword'), '33', '33', '/var/tmp', '/usr/sbin/nologin');

* в данном примере мы создаем пользователя sqluser с паролем sqlpassword.

... и отключаемся от базы:

> \q
Настройка FTP-сервера

Открываем конфигурационный файл для proftpd:

nano /etc/proftpd/proftpd.conf

Снимаем комментарий для подключения файла sql.conf:

Include /etc/proftpd/sql.conf

Открываем на редактирование файл sql.conf:

nano /etc/proftpd/sql.conf

Приводим его к виду:

<IfModule mod_sql.c>
...
SQLBackend      mysql
...
SQLEngine on
SQLAuthenticate users
...
SQLAuthTypes Crypt
...
SQLConnectInfo proftpd@localhost proftpd_user proftpd_password
...
SQLUserInfo users userid passwd uid gid homedir shell
...
SqlLogFile /var/log/proftpd/sql.log
...
</IfModule>

* где нужно обратить внимание на следующие параметры:

    SQLAuthenticate — указываем, что модуль должен выполнять аутентификацию по пользователю.
    SQLAuthTypes — способ хранения пароля в базе. Можно перечислить несколько вариантов. Для наибольшей безопасности мы разрешили хранить пароли только в зашифрованном виде.
    SQLConnectInfo — параметры для подключения к базе. Здесь мы задаем имя и сервер базы данных, а также данные пользователя для подключения.
    SQLUserInfo — информация о таблице, где хранится пользователь. Мы указываем на название таблицы и перечисляем название полей, в которых хранятся нужные сведения.

Создаем дополнительный конфигурационный файл для proftpd:

nano /etc/proftpd/conf.d/virtual_mysql.conf

RequireValidShell               off
AuthOrder                       mod_sql.c

Открываем файл modules.conf:

nano /etc/proftpd/modules.conf

Снимаем комментарии для следующих строк:

LoadModule mod_sql.c
...
LoadModule mod_sql_mysql.c

Перезапускаем сервис FTP-сервера:

systemctl restart proftpd

Можно пробовать подключаться к базе под пользователем sqluser с паролем sqlpassword. 
Настройка прав доступа

Разберем пример, когда нам нужно будет к одной и той же папке дать разные права — одному пользователю только на чтение, другому на чтение и запись.

nano /etc/proftpd/conf.d/rights.conf

Добавляем:

<Directory /var/tmp>
        <Limit WRITE>
                Order deny,allow
                AllowUser ftpvirt
        </Limit>
        <Limit ALL>
                AllowAll
        </Limit>
</Directory>

* в данном примере мы задаем права для директории /var/tmp. Мы разрешаем запись в директорию только для пользователя ftpvirt, остальные права разрешены для всех.
Устранение проблем

Для решения проблем в работе FTP-сервера можно просмотреть файл журнала. Файлов может быть несколько и они находятся в каталоге /var/log/proftpd. Основной — proftpd.log.

Для просмотра вводим команду:

tail -f /var/log/proftpd/proftpd.log

По умолчанию, настройка лога в конфигурационном файле proftpd выглядит так:

TransferLog /var/log/proftpd/xferlog
SystemLog   /var/log/proftpd/proftpd.log

При необходимости, можно настроить дополнительный файл журнала:

ExtendedLog                     /var/log/proftpd/access.log WRITE,READ write
ExtendedLog                     /var/log/proftpd/auth.log AUTH auth

* в данном примере в файле /var/log/proftpd/access.log будут храниться логи обращения к файлам; /var/log/proftpd/auth.log — аутентификации.

Не забываем перезагрузить сервис:

systemctl restart proftpd
