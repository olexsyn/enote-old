# Security

- [Настройка SSL-сертификата LetsEncrypt](letsencrypt)
- [Tor Browser](torbro)

```apache
RewriteEngine on

# для хакерских запросов ищущих php-скрипты
RewriteCond %{REQUEST_URI} \.php$ [OR]
RewriteCond %{REQUEST_URI} admin
RewriteRule (.*) /error/404/hackers.htm [F,L]

# запросы по не защищенному протоколу и/или запросы с www
RewriteCond %{HTTPS} !on [OR]
RewriteCond %{HTTP_HOST} ^www\.
RewriteRule (.*) https://YOURDOMAIN.COM%{REQUEST_URI} [L,R=301]
```
## Хеші

| алг.   | довж. | приклад |
| ------ | ----- | ------- |
| MD5    | 32    | 139964c7385e0e8751c5c56a36687c88 |
| SHA1   | 40    | 68941fadbf551907bbec059d229949b4c111a608 |
| SHA256 | 64    | d3a64fddd1abf21d998021e3f3bc8c5461b7c9c1d644ef6ed3b5c78059a64a2b |
| SHA512 | 128   | у 2 рази довший, ніж ^^^ |
