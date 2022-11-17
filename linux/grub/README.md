# Linux. Programs. GRUB

## Редактирование некоторых параметров GRUB

В файле **/etc/default/grub**

    sudo nano /etc/default/grub

### Уменьшение времени ожидания при загрузке

Исправляем на нужное значение (в секундах) параметр `GRUB_TIMEOUT`. Например:

```apache
  GRUB_TIMEOUT=2
```

### Включение информации о загрузке системы

Чтобы заменить графическую заставку во время загрузки на информацию о загрузке компонентов системы (это позволит проследить за процессом загрузки и выявить неполадки).

```apache
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```

Manjaro: `GRUB_CMDLINE_LINUX_DEFAULT="quiet resume=UUID=f1fcafae-b6b2-42a7-8e39-50cd7a159913"`

заменить на:

```apache
GRUB_CMDLINE_LINUX_DEFAULT=""
```

Manjaro: оставил только `resume`

```apache
GRUB_CMDLINE_LINUX_DEFAULT="resume=UUID=f1fcafae-b6b2-42a7-8e39-50cd7a159913"
```

Если нужно отключить splash только для одной загрузки, то при старте системы нажмите Escape чтобы перейти в меню grub. Далее нажимаем кнопку "e" для перехода к редактированию опций загрузки. Находим параметры ядра (строка начинается со слова linux) и просто удаляем слово splash и нажимаем Ctrl+X чтобы начать загрузку.

### Отключение меню GRUB

:sos:

В случае, если на компьютере установлена только одна ОС, можно отключить меню загрузки чтобы **grub** загружал систему напрямую.

Однако же, иногда может возникнуть необходимость загрузиться с другим ядром или же запустить проверку памяти. для этого предусмотрено "скрытое меню".

За него отвечает параметр `GRUB_HIDDEN_TIMEOUT`. в случае, когда установлены другие ОС, этот параметр закомментирован (# в начале строки). в случае с единственной ОС он будет активен.

Значение его задает задержку в секундах. **grub** приостановит загрузку на заданное количество секунд, давая пользователю возможность вызвать меню загрузки, нажав `[Esc]`.

Если значение установлено в 0, то задержки не будет. Однако, пользователь все равно сможет вызвать отображение меню, удерживая при загрузке `[Shift]`.

Параметр "GRUB_HIDDEN_TIMEOUT_QUIET" отвечает за отображение таймера во время паузы. при значении `true` таймер показан не будет. `false` - будет отображаться.

```
# If you change this file, run 'update-grub' afterwards to update
# /boot/grub/grub.cfg.
# For full documentation of the options in this file, see:
#   info -f grub -n 'Simple configuration'

# применить изменения:
# sudo update-grub

# пункт загрузки по умолчанию
GRUB_DEFAULT=0
# время ожидания (в сек.) выбора пункта меню GRUB
GRUB_TIMEOUT=2
# чтобы меню GRUB не отображалось раскомментировать следующую строчку
# GRUB_HIDDEN_TIMEOUT=0
GRUB_HIDDEN_TIMEOUT_QUIET=true
GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
GRUB_CMDLINE_LINUX_DEFAULT=""
GRUB_CMDLINE_LINUX=""

# Uncomment to enable BadRAM filtering, modify to suit your needs
# This works with Linux (no patch required) and with any kernel that obtains
# the memory map information from GRUB (GNU Mach, kernel of FreeBSD ...)
#GRUB_BADRAM="0x01234567,0xfefefefe,0x89abcdef,0xefefefef"

# Uncomment to disable graphical terminal (grub-pc only) ! текстовый режим (синее меню)
# GRUB_TERMINAL=console

# The resolution used on graphical terminal
# note that you can use only modes which your graphic card supports via VBE
# you can see them in real GRUB with the command `vbeinfo'
#GRUB_GFXMODE=640x480

# Uncomment if you don't want GRUB to pass "root=UUID=xxx" parameter to Linux
#GRUB_DISABLE_LINUX_UUID=true

# Uncomment to disable generation of recovery mode menu entries
#GRUB_DISABLE_RECOVERY="true"

# Uncomment to get a beep at grub start
#GRUB_INIT_TUNE="480 440 1"
```
### Пример файла grub для VM, где только одна ОС

(показать все строки, кроме закомментированных):

  cat /etc/default/grub | grep -v '#'

```apache
GRUB_DEFAULT=0
GRUB_TIMEOUT=0
GRUB_HIDDEN_TIMEOUT=0
GRUB_HIDDEN_TIMEOUT_QUIET=true
GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
GRUB_CMDLINE_LINUX_DEFAULT=""
GRUB_CMDLINE_LINUX=""
```

## Сохранение внесенных изменений:

  sudo update-grub


## Links

* http://ubuntologia.ru (+ описание различных опций, русс)
* https://ru.wikibooks.org (вообще все про GRUB2, русс)
* [восстановление grub](http://help.ubuntu.ru/wiki/восстановление_grub)
* [Восстановление grub и MBR,  различные ситуации](http://blog.amet13.name/2013/02/grub-mbr.html)
* [Мстительный Linux или no such partition grub rescue](.grub:problem)
* [В случае нештатного отключения компьютера](.grub:problem2)
* [Как удалить GRUB и восстановить загрузчик Windows 7](.grub:remove_grub)

* http://help.ubuntu.ru/wiki/grub
* http://ubuntologia.ru/blog/system/117.html
* http://ubuntologia.ru/blog/system/116.html
* http://ru.wikibooks.org/wiki/Grub_2
* [Начальный загрузчик GRUB 2 - полное руководство](http://rus-linux.net/MyLDP/boot/GRUB2-full-tutorial.html)
* www.ibm.com/developerworks/ru/library/l-lpic1-v3-102-2/
* habr.com/post/104536/ - GRUB: Получаем полный доступ к системе
* [BURG, или как сделать ваш загрузчик красивым](http://kubuntu.ru/node/6866)
* [Мультизагрузка с GRUB Mini-HOWTO](http://www.vnc.org.ua/grub/Multiboot-with-GRUB.html) (Кажется, это древний grub, но все же занимательно)
* [Мультизагрузка Windows, Linux и Mac OS X](http://ru.d-ws.biz/articles/multibootWinLinMac.shtml) (Тут посвежее)

:question: Что за команда? восстановление MBR?

  sudo apt-get install mbr
  sudo install-mbr /dev/sda


## Linux: изменить порядок загрузки в GRUB

Было решено заменить загрузку с Ubuntu на Windows, что бы не выбирать систему во время запуска.

Настройки порядка загрузки хранятся в файле /boot/grub/grub.cfg, в первых же строках которого большими буквами сказано:

  # DO NOT EDIT THIS FILE

Потому что этот файл создается самой системой во время выполнения команды update-grub на основе файлов:

  # ls -1 /etc/grub.d/
  00_header
  05_debian_theme
  10_linux
  20_linux_xen
  20_memtest86+
  30_os-prober
  30_uefi-firmware
  40_custom
  41_custom
  README

И файла `/etc/default/grub`, в котором мы и будем менять значение порядка загрузки.

Перед изменениями – делаем резервную копию:

  # cp /etc/default/grub /etc/default/grub.bkp

Для root-доступа не забыть:

  sudo -s

Выглядит файл `/etc/default/grub` по-умолчанию так:

  # cat /etc/default/grub | grep -v '#'

  GRUB_DEFAULT=0
  GRUB_HIDDEN_TIMEOUT_QUIET=true
  GRUB_TIMEOUT=10
  GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
  GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
  GRUB_CMDLINE_LINUX=""

Строка `GRUB_DEFAULT` может иметь значение либо числовое (0, 1 и т.д.), либо буквенное – `saved`.

`GRUB_DEFAULT=0` будет загружать первую систему, описанную в файле `/boot/grub/grub.cfg`, в блоках `menuentry`.

Обратите внимание, что строки входящие в `submenu` не учитываем, но сам раздел `submenu` учитываем – `+1`.

Проще всего во время загрузки GRUB просто посчитать порядковый номер системы, либо – просмотреть файл /boot/grub/grub.cfg в текстовом редакторе, в котором будет четко видно разделение на «главные» пункты меню, и его «подменю».


Вариант – изменить строку `GRUB_DEFAULT=` вручную, прямо в файле, и указать номер системы для загрузки.

Либо, вместо номера, указать полное имя:

  GRUB_DEFAULT="'Windows 7 (loader) (на /dev/sda1)"

Другой вариант – изменить `GRUB_DEFAULT` на `GRUB_DEFAULT=saved`, после чего выполнить:

  # grub-set-default 4

Этим мы указываем две вещи:

а) GRUB_DEFAULT=saved – GRUB будет загружать ту систему, которая была загружена последней;

б) такой системой мы устанавливаем запись №4, т.е. – Windows 7 (loader).

Причем второй пункт выполнять необязательно – достаточно будет 1 раз выбрать систему во время загрузки – и она будет сохранена как «система по-умолчанию».

Так же, вместо указания «индекса» системы – можно указать полное ее полное «имя»:

  # grub-set-default "'Windows 7 (loader) (на /dev/sda1)"

После чего выполнить:

  # update-grub

//Generating grub configuration file ...
Найден образ linux: /boot/vmlinuz-3.13.0-24-generic
Найден образ initrd: /boot/initrd.img-3.13.0-24-generic
Найден образ linux: /boot/vmlinuz-3.5.0-46-generic
Найден образ initrd: /boot/initrd.img-3.5.0-46-generic
Найден образ linux: /boot/vmlinuz-3.5.0-37-generic
Найден образ initrd: /boot/initrd.img-3.5.0-37-generic
Найден образ linux: /boot/vmlinuz-3.5.0-26-generic
Найден образ initrd: /boot/initrd.img-3.5.0-26-generic
Найден образ linux: /boot/vmlinuz-3.5.0-17-generic
Найден образ initrd: /boot/initrd.img-3.5.0-17-generic
Found memtest86+ image: /boot/memtest86+.elf
Found memtest86+ image: /boot/memtest86+.bin
Найден Windows 7 (loader) на /dev/sda1
завершено//



## Исправление заставки

Чиним сплэш в Ubuntu 10.04

После установки проприетарных драйверов видео (по крайней мере от nVidia, насчет ATI не знаю) в Ubuntu 10.04 сплэш при загрузке по какой-то причине показывается в маленьком разрешении экрана и поэтому выглядит увеличенным. Исправить это очень просто.

Открываем файл конфигурирования загрузчика системы GRUB 2:

  sudo nano /etc/default/grub

Добавляем в него такую строку:

```apache
  GRUB_GFXPAYLOAD_LINUX=1024x768
```

Вместо `1024x768` пишите своё разрешение. Куда добавлять — не важно, я добавил сразу после `GRUB_CMDLINE_LINUX`.

После чего нам нужно обновить конфигурацию GRUB, чтобы произведенные нами изменения записались в grub.cfg. Для этого существует следующая команда:

  sudo update-grub

Теперь загрузочная заставка должна быть нормальных размеров.

## Что-то такое случилось...

как-то поставил Минт вместо другого Минта, который был прописан с виндой на grub'е. Установщик винду не заметил, предлагал поставить Минт рядом с Минтом. Поэтому выбрал пункт __вручную__. Взял, затер области со старым Минтом, создал новые и установил туда новый Минт. Все было Ок, пока не решил запустить винду. А она взяла и исправила "ошибки" на диске. Пытался исправить по вышеприведенной инструкции - `install grub` ругался что-то про canonical, слишком маленькую загрузочную область, писал `error`. Не знаю, что именно повлияло, но Загрузил gparted, и установил boot на раздел с линуксом вместо винды - и grub успешно загрузился.

```
mint@mint ~ $ sudo mount /dev/sda6 /mnt
mint@mint ~ $ sudo grub-install --root-directory=/mnt /dev/sda

grub-probe: error: failed to get canonical path of `/cow'.
Installing for i386-pc platform.
grub-install.real: warning: your embedding area is unusually small.  core.img won't fit in it..
grub-install.real: warning: Embedding is not possible.  GRUB can only be installed in this setup by using blocklists.  However, blocklists are UNRELIABLE and their use is discouraged..
grub-install.real: error: will not proceed with blocklists.

mint@mint ~ $ sudo update-grub --output=/mnt/boot/grub/grub.cfg
/usr/sbin/grub-probe: error: failed to get canonical path of `/cow'.
```



Назад на [Linux. Programs](:linux:programs)
