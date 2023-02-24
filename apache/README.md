# Apache

- [Установка и настройка Apache](install)
- [файл .htaccess](htaccess)
- [директива Directory](directory)
- [SSI](ssi)
- [ModRewrite](mod_rewrite)
- [SSL](ssl)
- [Коды ошибок](error_code)
- [Проблема корректного отображения UTF8 в CGI-скриптах](cgi-utf-fix)
- [Apache і Мирохост](mirohost)

### Версія

```
/usr/sbin/apache2 -v

Server version: Apache/2.4.29 (Ubuntu)
Server built:   2020-03-13T12:26:16"
```

### Стан

```
service apache2 stаtus
```

### Стоп, старт, рестарт

```
sudo service apache2 stop|start|restart
```

а також, в інших дистрибутивах Linux:

```
systemctl status httpd
sudo systemctl stop|start|restart httpd.service
```

```
/etc/init.d/apache2 status
/etc/init.d/apache2 stop|start|restart|reload|force-reload
```

Перевірка конфігурації

```
sudo apache2ctl configtest
```

Допомагає знайти помилку у файлах конфігурації


> <span class="warn">!</span> В случае появления сообщения  
> `AH00558: httpd: Could not reliably determine the server's fully qualified`  
> необходимо прописать `ServerName localhost`  
> в файле **/etc/apache2/apache2.conf** (или **/etc/httpd/conf/httpd.conf**)


## restart и reload - разница?

- **restart**: останавливает (**stop**), а затем запускает (**start**) службу Apache.
- **reload:** изящно перезапускает службу Apache. При reload основной процесс Apache завершает работу дочерних процессов, загружает новую конфигурацию и запускает новые дочерние процессы.

## Подключить виртуальный хост

- [Подключить виртуальный хост - a2ensite](a2ensite)

<span class="warn">TODO!</span>

- [Configuring Apache2 to run Python Scripts](https://www.linux.com/training-tutorials/configuring-apache2-run-python-scripts/)
