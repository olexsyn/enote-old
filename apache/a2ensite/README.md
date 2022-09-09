## Подключить сайт

Конфігураційні файли для віртуальних хостів зберігаються в `/etc/apache2/sites-available/`

Для Apache, починаючи з версії 2.4, у файла має бути розширення `.conf`

Приклад файлу конфігурації хоста **mysite.com** (файл `/etc/apache2/sites-available/mysite_com.conf**`):

```apache
<VirtualHost 127.0.1.2:80>
	ServerName site.com.loc
	DocumentRoot /home/olex/www/site/site.com
	<Directory /home/olex/www/site/site.com/>
		Options +Includes
		AddType text/html .htm
		AddOutputFilter INCLUDES .htm
		AllowOverride All
		Require all granted
		# see https://olexsyn.github.io/e-note/apache/cgi-utf-fix/
		PassEnv LANG en_US.UTF-8
	</Directory>

	ScriptAlias /cgi-bin/ /home/olex/www/site/cgi-bin/
	<Directory "/home/olex/www/site/cgi-bin">
		AllowOverride None
		Options +ExecCGI -MultiViews
		Require all granted
		# see https://olexsyn.github.io/e-note/apache/cgi-utf-fix/
		PassEnv LANG en_US.UTF-8
	</Directory>

	ErrorLog /home/olex/www/__logs/site/error.log
	CustomLog /home/olex/www/__logs/site/access.log combined
</VirtualHost>
```

Для того, щоб Apache прочитав конфігурацію, потрібно додати символічне посилання на файл конфігурації в каталозі `/etc/apache2/sites-enabled/`.

Зробити це можна командою **a2ensite**:

{% include cl.htm cmd="sudo a2ensite site_com" %}

> яка, насправді, просто створює символічне посилання:  
> `sudo ln -s /etc/apache2/sites-available/site_com.conf /etc/apache2/sites-enabled/site_com.conf`  
> ([дивись код](a2ensite), якщо цікаво)

перевірити наявність помилок у синтаксисі:

{% include cl.htm cmd="sudo apache2ctl configtest"
out="Syntax OK" %}

та перезапустити http-сервер:

{% include cl.htm cmd="sudo systemctl reload apache2" %}

**Команда для відключення конфігурації** віртуального хоста:

{% include cl.htm cmd="sudo a2dissite site_com" %}

> ([дивись код](a2dissite), якщо цікаво)

> У процесі запуску сервера можемо отримати повідомлення:  
> `Could not reliably determine the server's fully qualified domain name, ...`  
> Це можна [виправити так]({{ site.baseurl }}/apache/err_not_reliably_determine).
