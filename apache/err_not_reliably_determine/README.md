# Ошибка Could not reliably determine

После перезапуска Apache мы можем столкнуться с не критическим сообщением:

`Could not reliably determine the server's fully qualified domain name, ...`

## Apache 2.2

Создаем файл **/etc/apache2/conf.d/vhosts.conf**

Куда прописываем `ServerName localhost`

Cохраняем файл и рестартуем Apache:

  sudo /etc/init.d/apache2 reload

## Apache 2.4

Відкриваємо файл **/etc/apache2/apache2.conf** і додаємо рядок `ServerName localhost`

Зберігаємо файл та перезапускаємо Apache

----

Также смотри [здесь](apache:dirs_n_files_ubuntu#warn).
<span class="warn">TODO!</span>
