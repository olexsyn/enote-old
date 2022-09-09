# Установка и настройка Apache

{% include cl.htm cmd="sudo apt install apache2" %}

## Модули

В Дебиан есть много различных модулей для Апач, каждый пакет имеет префикс `libapache2-mod`. Уже установленые модули, могут быть включены или отключены с помощью команды **a2enmod** и **a2dismod**.

### Подключить возможность обрабатывать инструкции SSI

{% include cl.htm cmd="sudo a2enmod include" %}

### Подключить mod_rewrite

{% include cl.htm cmd="sudo a2enmod rewrite" %}

## Скрипты / Динамический контент

Апач может использовать разные внешние программы и скриптовые языки, через CGI или FastCgi (libapache2-mod-fcgid). Апач может использовать различные скриптовые языки или соединяться с сервером приложений для создания динамического контента:

PHP (libapache2-mod-php5), Perl (libapache2-mod-perl2), Python (libapache2-mod-python, libapache2-mod-wsgi), Java/Jsp, Ruby,
Lisp...

### Подключить возможность выполнять CGI-скрипты:

{% include cl.htm cmd="sudo a2enmod cgi" %}

## Подключить виртуальный хост

[a2ensite](../a2ensite)

## Якщо потрібен протокол `HTTPS`

[робимо це](../ssl)

!!TODO!!

- [Apache HTTP Server Version 2.4 Documentation](http://httpd.apache.org/docs/2.4/)
  - [Introduction to Server Side Includes](http://httpd.apache.org/docs/2.4/howto/ssi.html)
  - [nginx в связке с ssi](http://nginx.org/ru/docs/http/ngx_http_ssi_module.html) - [nginx](http://nginx.org/ru/)

- [Как подключить mod_rewrite](mod_rewrite)
