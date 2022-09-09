# директива Directory

Определяя настройки доступа к каталогам сайта с помощью директивы <Directory> в одном конфигурационном файле всего сайта, мы получим следующие преимущества:

- можно быть уверенным, что ничего не пропустим, если вдруг нужно изменить уровень доступа к какому-нибудь ресурсу;
- повышаем скорость реакции сервера на запросы, т.к. все настройки загружаются при старте Apache.

Ну а мириться придется с тем, что для каждого каталога необходимо описывать права отдельно (помним, что для подкаталогов права наследуются), даже если они одинаковые. Правда, есть поддержка масок, например:


```apache
<Directory ~ "^/www/.*/[0-9]{3}">
```

будет соответствовать именам каталогов в `/www/`` состоящим из трех цифр, но это не всегда может облегчить ситуацию.


Пример
Описываем те же права в главном конфигурационном файле Apache _**httpd.conf**_ или в файле настройки виртуального хоста:

```apache
<VirtualHost logos.mynetwork.ru>
  DocumentRoot /var/www/html/logos
  ServerName logos.mynetwork.ru
  ErrorLog /var/log/httpd/logos/error_log
  CustomLog /var/log/httpd/logos/access_log combined
  <Directory /var/www/html/logos/info1>
    Options +Indexes
    Order deny,allow
    Deny from all
    Allow from 192.168.100.11
    Allow from 192.168.100.17
  </Directory>
  <Directory /var/www/html/logos/info2>
    AuthType Basic
    AuthName "Boss"
    AuthUserFile "/var/www/main_users"
    Require valid-user
  </Directory>
</VirtualHost>
```