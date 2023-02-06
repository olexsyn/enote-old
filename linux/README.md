# Linux

скинути і знову увімкнути своп:
```
sudo swapoff -a
sudo swapon -a
```
встановити дозволи на всі каталоги чи файли:
```
find ./catalog -type d -exec chmod 755 {} \;
find ./catalog -type f -exec chmod 644 {} \;
```
Створити вміст каталогу / розархівувати tgz-архів:
```
tar -czf pages.tgz ./pages
tar -xzf pages.tgz
```
скинути сторінковий кеш:
```
su -
sync; echo 1 > /proc/sys/vm/drop_caches
```

<https://www.stationx.net/linux-command-line-cheat-sheet/>

- [apt](apt)         - менеджер пакетів
- [cat](cat)         - показати вміст файлу
- [cd](cd)           - перейти в каталог
- [chmod](http://ans.kiev.ua/wiki/linux/commands/chmod_chown_r)
- [chown](http://ans.kiev.ua/wiki/linux/commands/chmod_chown)
- [cp](cp)           - копіювати файл(и) або каталог(и)
- [dig](dig)         - подивитися запис домену
- [du](du)           - розмір каталогу або файлу
- [echo](echo)       - виводить передані аргументи
- [fdisk](fdisk)     - керування розділами диска
- [ffmpeg](ffmpeg)   - конвертор видео и аудео
- [gedit](gedit)     - редагування файла
- [grep](grep)       - пошук рядків у файлі
- [history](history) - останні команди в консолі
- [id](id)           - ідентифікатор користувача
- [ln](ln)           - створення посилань на файли та каталоги
- [locate](locate)   - пошук файлів
- [ls](ls)           - список файлів та каталогів
- [mkdir](mkdir)     - створення директорії
- [more](more)       - вивести файл частинами
- [mv](mv)           - перейменування каталогу
- [nano](nano)       - редагування файлу
- [proftpd](proftpd) - сервіс FTP
- [pwd](pwd)         - поточний шлях
- [rm](rm)           - видалення файлів і каталогів з файлами
- [rmdir](rmdir)     - видалення каталогів
- [rsync](rsync)     -
- [ssh](ssh)         -
- [tail](tail)       - подивитись кінець файлу
- [tar](tar)         - архіватор TAR
- [tee](tee)         - запис в декілька файлів одночасно
- [terminal](terminal) - термінал
- [touch](touch)     - створити порожній файл
- [unlink](unlink)   - видалення файлу або символічного посилання на файл

- [Як...](how_to)
  - [встановити шрифти](how_to/install_fonts)
  - [восстановить работоспособность USB диска/флешки после записи ISO или установки ОС](recovery_usbflash)
  - [mount -bind](https://access.redhat.com/documentation/ru-ru/red_hat_enterprise_linux/6/html/global_file_system_2/s1-manage-pathnames)

- [В терминале, как профи](terminal_pro)
- [Команди](command)
- [Програми](soft)
- [Конфигурації](config)
- [Проблемы](trouble)
- [Разное](other)
