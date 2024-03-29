# Работаем в терминале Linux как профи: подборка полезных команд

https://tproger.ru/articles/useful-linux-commands/


## Использование табов для автодополнения

Когда вы начинаете что-то вводить в терминале, вы можете нажать Tab и вам будут предложены возможные варианты продолжения, которые начинаются с введённой вами строки.

Например, если вы хотите скопировать файл с именем `file1.txt`, вы можете ввести только `cp f`, нажать Tab и увидеть возможные варианты.

```
$ cp f
file1.txt  file2.txt  file3.txt  file4.txt
$ cp f
```
Также Tab можно использовать для автодополнения команд.


## Возвращение в последнюю рабочую директорию

Представьте ситуацию, когда вы спустились глубоко по иерархии папок, затем перешли в папку, которая находится в совершенно другом месте, а потом поняли, что вам нужно вернуться обратно. В таком случае вам всего лишь нужно ввести следующую команду:

`cd -`

Она вернёт вас в последнюю рабочую директорию и вам не придётся вручную вводить длинный путь.

> **Примечание** Последняя рабочая директория хранится в переменной окружения `OLDPWD`; вы можете использовать эту переменную для своих целей (попробуйте `echo $OLDPWD`) или даже подложить команде `cd -` другой путь (`OLDPWD=/usr/bin cd -`).


## Возвращение в домашнюю директорию

Это слишком очевидно. Чтобы вернуться в домашнюю директорию из любого места, вы можете использовать следующую команду:

`cd ~`

А вообще, можно ограничиться командой `cd` и получить тот же результат. В большинстве современных дистрибутивов Linux эта команда должна сработать.


## Вывести содержимое каталога

Вы, наверное, догадываетесь, какая команда нужна для отображения содержимого каталога. Всем известно, что для этого можно использовать `ls -l`.

Однако не все знают, что можно обойтись командой `ll`.

Конечно, всё зависит от дистрибутива, но в большинстве случаев вы сможете воспользоваться этой командой.

```
$ ll
total 44
-rw-r--r--.  1 root root  720 May 31  2016 bootchart.conf
-rw-r--r--.  1 root root  615 Jun 22 14:11 coredump.conf
-rw-r--r--.  1 root root    0 Apr 20 16:56 dont-synthesize-nobody
-rw-r--r--.  1 root root 1027 Jun 22 14:11 journald.conf
-rw-r--r--.  1 root root 1042 Jul 18 19:03 logind.conf
drwxr-xr-x.  2 root root 4096 Jul 18 19:05 network
-rw-r--r--.  1 root root  688 Jul 18 19:03 resolved.conf
drwxr-xr-x. 16 root root 4096 Sep 15 13:29 system
-rw-r--r--.  1 root root 1682 Jul 18 19:03 system.conf
-rw-r--r--.  1 root root  677 Jul 18 19:03 timesyncd.conf
drwxr-xr-x.  2 root root 4096 Jul 18 19:05 user
-rw-r--r--.  1 root root 1130 Jun 22 14:11 user.conf
```
> **Примечание**  На самом деле, `ll` является не отдельной командой, а псевдонимом для `ls -l`.


## Запуск нескольких команд за раз

Допустим, вам нужно запустить несколько команд одну за другой. Что вы будете делать? Подождёте завершения первой команды, а затем запустите следующую?

Вместо этого вы можете использовать разделитель `;`. Таким образом можно запустить несколько команд на одной строке. Вам не нужно ждать, пока какая-то из команд завершит свою работу, чтобы запустить следующую.

`command_1; command_2; command_3`

> **Примечание**  При запуске команд таким образом, они выполняются не параллельно, а последовательно. Если вам нужен именно первый вариант, то используйте конструкцию `(command_1 &); (command_2 &)`.


## Запуск нескольких команд за раз при условии, что предыдущая команда была выполнена успешно

Как запускать несколько команд за раз вы уже знаете. А как убедиться, что команды не завершились с ошибкой?

Допустим, вы хотите собрать код и запустить его в случае успешной сборки.

В этом случае вы можете использовать разделитель `&&`, который запускает следующую команду только при условии, что предыдущая успешно завершилась.

`command_1 && command_2`

Как пример использования `&&` можно привести команду `sudo apt update && sudo apt upgrade` для обновления системы через терминал на системах, основанных на Debian.


## Время убивать

Есть несколько способов «убить» программу. Команда `killall` сделает это по имени, а `kill` требуется номер процесса. Например, `killall chrome` убьёт все процессы chrome. Также можно послать любому процессу сигнал прерывания (как Ctrl+C) с помощью `kill -INT <номер процесса>`.


## Пора остановиться

Чтобы поставить работающую команду на паузу нажмите комбинацию Ctrl+Z, а чтобы продолжить — `%`.


## Простой поиск и использование предыдущих команд

Представим ситуацию, когда вы воспользовались какой-то командой пару часов назад и снова хотите её использовать, но не можете вспомнить название.

Здесь поможет обратный поиск. С его помощью можно по заданному условию найти команду в истории.

Просто нажмите комбинацию Ctrl+R и введите часть команды. Затем вам будут показаны команды из истории, которые удовлетворяют заданному условию.

`Ctrl+R <условие>`

По умолчанию показывается только один результат. Чтобы увидеть больше результатов, нужно повторно нажать Ctrl+R. Чтобы выйти из поиска, нажмите Ctrl+C.

Учтите, что в некоторых оболочках Bash можно использовать Page Up и Page Down с условием поиска для автодополнения команды.


## Выводим консоль из зависания после Ctrl+S

Многие привыкли использовать комбинацию Ctrl+S для сохранения. Однако после её использования в терминале, он часто зависает. Чтобы вернуть его в нормальное состояние, нажмите комбинацию Ctrl+Q.


## Переход к началу или концу строки

Допустим, вы вводите длинную команду и вдруг понимаете, что вам нужно что-то изменить в её начале. Чтобы попасть в начало или конец строки вы можете несколько раз нажать клавишу стрелки влево/вправо или Home/End. А можете нажать Ctrl+A или Ctrl+E.


## Чтение лог-файла в реальном времени

В ситуациях, когда вам нужно анализировать логи при запущенном приложении, можно использовать команду `tail` с флагом `-f`.

`tail -f <путь к лог-файлу>`

Также можно использовать регулярные выражения в `grep`, чтобы выводить только нужные строки:

`tail -f <путь к лог-файлу> | grep <регулярное выражение>`

Кроме того, вы можете использовать флаг `-F`, чтобы `tail` продолжал работу даже в случае удаления лог-файла. Таким образом, когда лог-файл снова будет создан, `tail` продолжит логирование.

Если вы хотите просматривать системный лог в реальном времени, воспользуйтесь аналогичной опцией `-f` команды `journalctl`:

`journalctl -f`


## Чтение сжатых логов без извлечения

Серверные логи обычно сжимаются gzip'ом для сохранения дискового пространства. Это становится проблемой для разработчика или сисадмина, который анализирует эти логи. Возможно, вам придётся скопировать архив в другое место, а затем извлечь его, так как не всегда есть права на извлечение логов.

К счастью, в таких ситуациях всегда спасут z-команды. Они являются альтернативами обычных команд, которые используются для работы с логами вроде `less`, `cat`, `grep`.

Поэтому вы можете воспользоваться `zless`, `zcat`, `zgrep` и т.д., даже не извлекая логи.


## Использование less для чтения файлов

Команда `cat` не всегда лучший выбор для отображения содержимого файла, особенно если он большой — `cat` выведет сразу весь файл.

Вы можете использовать Vi, Vim или другой терминальный текстовый редактор, но если вам просто нужно прочитать файл, то команда `less` подойдёт гораздо лучше.

`less <путь к файлу>`

В `less` можно искать нужную подстроку, листать по страницам, отображать номера строк и не только. А ещё `less` может читать не только текстовые документы, но ещё и архивы и другие типы файлов.


## Использование аргумента предыдущей команды с помощью !$

Использование аргумента предыдущей команды может пригодиться во многих ситуациях. Например, вы создали директорию и вам нужно сразу в неё перейти.

```
$ ls /
bin  boot  cdrom  dev  etc  home  sys  tmp  usr  var  vmlinuz  vmlinuz.old
$ cd !$
cd /
```
Ещё лучше использовать `alt+.` . Множественное нажатие точки позволяет выбрать аргумент одной из нескольких предыдущих команд.


## Использование предыдущей команды в текущей с помощью !!

С помощью `!!` можно вызвать даже всю предыдущую команду. Это особенно полезно в тех случаях, когда оказывается, что для запуска команды нужны рут-привилегии.

Быстрое `sudo !!` позволяет сэкономить немного времени.


## Использование alias для исправления опечаток

Вероятно, вы уже знаете, зачем нужна команда `alias`. Её можно приспособить для исправления опечаток.

Представим, что вместо `grep` вы часто пишете `gerp`. Если вы установите псевдоним следующим образом, то вам не придётся больше перепечатывать команду:

`alias gerp=grep`

К слову, для исправления опечаток не обязательно использовать псевдонимы — утилита <a href="https://github.com/nvbn/thefuck" data-wpel-link="external" target="_blank" rel="nofollow noopener noreferrer">The Fuck</a> сама исправит предыдущую команду.


## Перезагружаемся

Чтобы выключить компьютер из терминала, введите `poweroff`, а для перезагрузки — `reboot`.


## Вставка скопированного текста в терминал

Здесь не всё однозначно, так как между дистрибутивами Linux и терминалами есть определённая разница. Но в общем случае вставить текст можно одним из следующих способов:


- Скопируйте текст и кликните правую кнопку мыши для вставки (работает в Putty и других Windows-клиентах SSH);
- Скопируйте текст и нажмите среднюю кнопку мыши (колёсико) для вставки;
- Ctrl+Shift+C для копирования и Ctrl+Shift+V для вставки;
- В некоторых эмуляторах терминала работает привычная комбинация Ctrl+V.


## Завершить работающий процесс/команду

Возможно, это слишком очевидно. Если у вас запущена команда, работу которой вы хотите завершить, просто нажмите Ctrl+C и команде будет отправлен сигнал прерывания (SIGINT). А если вы хотите быстро покинуть терминал, нажмите комбинацию Ctrl+D, которая для баша и других интерактивных программ означает окончание ввода.


## Команда для скриптов или команд, которым нужен интерактивный ответ

Команда `yes` может пригодиться, если какой-то скрипт/команда требует взаимодействия с пользователем, которое заключается только в нажатии Y каждый раз.

`yes | <команда или скрипт>`


## Очистить файл, не удаляя его

Если вам нужно только очистить содержимое файла, а не удалить его, вы можете сделать это следующим образом:

`> имя_файла`


## Узнать, есть ли файл с определённым текстом

В терминале Linux можно искать разными способами. Если вам нужно узнать, есть ли файл(ы) с определённым текстом, можете воспользоваться этой командой:

`grep -Pri <текст_для_поиск> <путь_к_директории>`


## Получаем справку для каждой команды

Почти все команды/инструменты командной строки содержат справку с указаниями по работе. Чтобы получить справку, воспользуйтесь этой командой:

`<команда> --help`

Кроме того, порой можно получить более подробную справку с помощью команды `man <команда>`.


## Получаем историю команд

Если вы хотите взглянуть на все команды, которые вы когда-либо запускали, введите `history`. Если вам нужен не полный список, а только несколько последних, воспользуйтесь командой `fc -l`.


## Быстро запускаем команды из истории

При получении команд одним из вышеуказанных способов рядом с каждой командой находится её номер в истории. Чтобы быстро запустить команду из этого списка просто введите `!<номер команды>`.


## Выполняем команду в обход истории

Если вы хотите выполнить команду так, чтобы она не сохранилась в истории, просто введите пробел перед командой.


## Поднимаем простой HTTP-сервер

Чтобы поднять сервер и сделать доступной текущую директорию по адресу http://localhost:8000/ введите `python3 -m http.server`.


## Пишем длинные команды с удобством

Если зажать Ctrl, а затем нажать по очереди X и E, то откроется текстовый редактор, в котором можно будет спокойно записать длинную команду, а после выхода из него — выполнить её.


## Восстанавливаем терминал

Если вы вывели в терминал сырые бинарные данные или ещё что-то, что выводить не стоило, то убрать увиденную абракадабру позволит команда `reset`.


## Информация о файловых системах

Чтобы получить информацию о текущих смонтированных файловых системах с удобным оформлением по столбцам, введите команду `mount | column -t`.

Также вы можете воспользоваться командой `findmnt`, которая отображает информацию в виде красивого дерева и сама форматирует столбцы, а также может найти нужную файловую систему:

```
$ findmnt
TARGET                                SOURCE      FSTYPE  OPTIONS
/                                     /dev/sda4   ext4    rw,relatime,seclabel
├─/sys                                sysfs       sysfs   rw,nosuid,nodev,noexec,rela
│ ├─/sys/kernel/security              securityfs  securit rw,nosuid,nodev,noexec,rela
│ ├─/sys/fs/cgroup                    tmpfs       tmpfs   ro,nosuid,nodev,noexec,secl
│ │ ├─/sys/fs/cgroup/unified          cgroup2     cgroup2 rw,nosuid,nodev,noexec,rela
│ │ ├─/sys/fs/cgroup/pids             cgroup      cgroup  rw,nosuid,nodev,noexec,rela
│ │ └─/sys/fs/cgroup/devices          cgroup      cgroup  rw,nosuid,nodev,noexec,rela
│ ├─/sys/fs/pstore                    pstore      pstore  rw,nosuid,nodev,noexec,rela
│ ├─/sys/firmware/efi/efivars         efivarfs    efivarf rw,nosuid,nodev,noexec,rela
│ ├─/sys/kernel/config                configfs    configf rw,relatime
│ └─/sys/fs/fuse/connections          fusectl     fusectl rw,relatime
├─/proc                               proc        proc    rw,nosuid,nodev,noexec,rela
│ └─/proc/sys/fs/binfmt_misc          systemd-1   autofs  rw,relatime,fd=30,pgrp=1,ti
│   └─/proc/sys/fs/binfmt_misc        binfmt_misc binfmt_ rw,relatime
├─/home                               /dev/sda6   ext4    rw,relatime,seclabel
└─/var/lib/nfs/rpc_pipefs             sunrpc      rpc_pip rw,relatime

```

## Деревья процессов

Есть инструмент `pstree`, который умеет рисовать красивые деревья процессов. Например:

```
$ pstree 1721
gnome-shell─┬─Xwayland───5*[{Xwayland}]
            ├─gnome-system-mo───3*[{gnome-system-mo}]
            ├─ibus-daemon─┬─ibus-dconf───3*[{ibus-dconf}]
            │             ├─ibus-engine-sim───2*[{ibus-engine-sim}]
            │             ├─ibus-extension-───3*[{ibus-extension-}]
            │             └─2*[{ibus-daemon}]
            ├─telegram-deskto───14*[{telegram-deskto}]
            └─13*[{gnome-shell}]
```

## Экран блокировки

Чтобы заблокировать экран, используйте команду `$ loginctl lock-session`.

Для разблокировки экрана введите команду `$ loginctl unlock-session`. Конечно, вряд ли вы сможете использовать терминал при заблокированном экране, однако вы можете пойти обходными путями. Например, можно создать задачу для разблокировки через какое-то время.


## Супершелл

Чтобы запустить шелл от имени суперпользователя, можно воспользоваться командой `sudo -s`.  Во многих источниках можно встретить вариант `sudo su`, который тоже работает, но медленнее, так как запускает лишний процесс.


## Быстро открываем файлы в программе по умолчанию

Команда `xdg-open` позволяет открыть любой файл в соответствующей программе. Например, `xdg-open file.txt` откроет файл в текстовом редакторе по умолчанию.


## Статус системных сервисов

Чтобы посмотреть статус системных сервисов, введите команду `systemctl status` или `systemctl status <имя сервиса>`, если вас интересует конкретный сервис.


## Быстро ищем файлы

Если вам нужно найти файл, но вы не знаете, где конкретно он находится, можно воспользоваться командой `find`. Например:

```
$ find /usr/include -name gtk.h
/usr/include/gtk-3.0/gtk/gtk.h
```

## Используем вывод одной команды в качестве аргумента другой

Чтобы использовать вывод одной команды в качестве аргумента другой, используйте конструкцию `команда-2 $(команда-1)`. Например:

```
$ less $(find /usr/include -name gtk.h)
```

## Календарь

Команда `cal` может нарисовать календарь на текущий месяц (и даже выделить текущее число) или на другой промежуток:

```
$ cal
   September 2018   
Mo Tu We Th Fr Sa Su
                1  2
 3  4  5  6  7  8  9
10 11 12 13 14 15 16
17 18 19 20 21 22 23
24 25 26 27 28 29 30
                    
$ cal 2019
                               2019                               

       January               February                 March       
Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su
    1  2  3  4  5  6                1  2  3                1  2  3
 7  8  9 10 11 12 13    4  5  6  7  8  9 10    4  5  6  7  8  9 10
14 15 16 17 18 19 20   11 12 13 14 15 16 17   11 12 13 14 15 16 17
21 22 23 24 25 26 27   18 19 20 21 22 23 24   18 19 20 21 22 23 24
28 29 30 31            25 26 27 28            25 26 27 28 29 30 31
                                                                  
        April                   May                   June        
Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su
 1  2  3  4  5  6  7          1  2  3  4  5                   1  2
 8  9 10 11 12 13 14    6  7  8  9 10 11 12    3  4  5  6  7  8  9
15 16 17 18 19 20 21   13 14 15 16 17 18 19   10 11 12 13 14 15 16
22 23 24 25 26 27 28   20 21 22 23 24 25 26   17 18 19 20 21 22 23
29 30                  27 28 29 30 31         24 25 26 27 28 29 30
                                                                  
        July                  August                September     
Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su
 1  2  3  4  5  6  7             1  2  3  4                      1
 8  9 10 11 12 13 14    5  6  7  8  9 10 11    2  3  4  5  6  7  8
15 16 17 18 19 20 21   12 13 14 15 16 17 18    9 10 11 12 13 14 15
22 23 24 25 26 27 28   19 20 21 22 23 24 25   16 17 18 19 20 21 22
29 30 31               26 27 28 29 30 31      23 24 25 26 27 28 29
                                              30                  
       October               November               December      
Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su   Mo Tu We Th Fr Sa Su
    1  2  3  4  5  6                1  2  3                      1
 7  8  9 10 11 12 13    4  5  6  7  8  9 10    2  3  4  5  6  7  8
14 15 16 17 18 19 20   11 12 13 14 15 16 17    9 10 11 12 13 14 15
21 22 23 24 25 26 27   18 19 20 21 22 23 24   16 17 18 19 20 21 22
28 29 30 31            25 26 27 28 29 30      23 24 25 26 27 28 29
                                              30 31          
```

## Планировщик задач

Чтобы выполнить какую-то команду в нужное вам время, воспользуйтесь `at`:

`echo команда-для-выполнения | at время_выполнения`

Учтите, что эта команда может отсутствовать на вашей системе, и вам придётся установить её самостоятельно.


## Получаем свой внешний IP

Чтобы получить свой внешний IP-адрес введите `curl ifconfig.me` или `curl ipinfo.io/ip`. Возможно, сначала вам придётся установить `curl`.


## Прогноз погоды

Введите команду `curl wttr.in/<нужный город>` и получите красивую таблицу с прогнозом погоды:

```
curl wttr.in/Kyiv
```
```
Weather report: Kyiv

       .-.      Heavy snow
      (   ).    -5(-11) °C     
     (___(__)   ↓ 17 km/h      
     * * * *    2 km           
    * * * *     0.5 mm         
                                                       ┌─────────────┐                                                       
┌──────────────────────────────┬───────────────────────┤  Mon 06 Feb ├───────────────────────┬──────────────────────────────┐
│            Morning           │             Noon      └──────┬──────┘     Evening           │             Night            │
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│      .-.      Moderate snow  │  _`/"".-.     Light snow     │  _`/"".-.     Light snow     │  _`/"".-.     Light snow     │
│     (   ).    -4(-10) °C     │   ,\_(   ).   -3(-9) °C      │   ,\_(   ).   -3(-8) °C      │   ,\_(   ).   -4(-9) °C      │
│    (___(__)   ↓ 17-24 km/h   │    /(___(__)  ↓ 18-24 km/h   │    /(___(__)  ↓ 14-18 km/h   │    /(___(__)  ↓ 14-20 km/h   │
│    * * * *    5 km           │      *  *  *  10 km          │      *  *  *  10 km          │      *  *  *  10 km          │
│   * * * *     0.1 mm | 0%    │     *  *  *   0.1 mm | 0%    │     *  *  *   0.0 mm | 0%    │     *  *  *   0.0 mm | 0%    │
└──────────────────────────────┴──────────────────────────────┴──────────────────────────────┴──────────────────────────────┘
                                                       ┌─────────────┐                                                       
┌──────────────────────────────┬───────────────────────┤  Tue 07 Feb ├───────────────────────┬──────────────────────────────┐
│            Morning           │             Noon      └──────┬──────┘     Evening           │             Night            │
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│               Cloudy         │               Overcast       │    \  /       Partly cloudy  │     \   /     Clear          │
│      .--.     -6(-10) °C     │      .--.     -3(-8) °C      │  _ /"".-.     -4(-9) °C      │      .-.      -6(-11) °C     │
│   .-(    ).   ↓ 9-14 km/h    │   .-(    ).   ↙ 13-17 km/h   │    \_(   ).   ↓ 12-18 km/h   │   ― (   ) ―   ↙ 12-20 km/h   │
│  (___.__)__)  10 km          │  (___.__)__)  10 km          │    /(___(__)  10 km          │      `-’      10 km          │
│               0.0 mm | 0%    │               0.0 mm | 0%    │               0.0 mm | 0%    │     /   \     0.0 mm | 0%    │
└──────────────────────────────┴──────────────────────────────┴──────────────────────────────┴──────────────────────────────┘
                                                       ┌─────────────┐                                                       
┌──────────────────────────────┬───────────────────────┤  Wed 08 Feb ├───────────────────────┬──────────────────────────────┐
│            Morning           │             Noon      └──────┬──────┘     Evening           │             Night            │
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│     \   /     Sunny          │     \   /     Sunny          │               Overcast       │     \   /     Clear          │
│      .-.      -7(-11) °C     │      .-.      -2(-6) °C      │      .--.     -4(-7) °C      │      .-.      -6(-10) °C     │
│   ― (   ) ―   ↓ 9-14 km/h    │   ― (   ) ―   ↓ 10-12 km/h   │   .-(    ).   ↘ 7-12 km/h    │   ― (   ) ―   ↘ 9-17 km/h    │
│      `-’      10 km          │      `-’      10 km          │  (___.__)__)  10 km          │      `-’      10 km          │
│     /   \     0.0 mm | 0%    │     /   \     0.0 mm | 0%    │               0.0 mm | 0%    │     /   \     0.0 mm | 0%    │
└──────────────────────────────┴──────────────────────────────┴──────────────────────────────┴──────────────────────────────┘
Location: Київ, Шевченківський район, Київ, 01000-06999, Україна [50.4501071,30.5240501]
```

## Получаем таблицу ASCII

Чтобы получить быстрый доступ к таблице ASCII просто введите `man ascii`.


## Простой калькулятор

Небольшие выражения можно вычислять прямо в терминале. Это можно сделать либо с помощью конструкции `echo <выражение> | bc`, либо `echo $((<выражение>))`. Например:

```
$ echo 35+42 | bc
77
$ echo $((35+42))
77
```

## Выполняем команду в другой директории и возвращаемся обратно

Если вы хотите выполнить команду в другой директории, но при это не хотите покидать текущую, то просто оберните команду скобками. Например, `(cd /tmp && ls)`. Здесь скобки запускают подшелл (subshell), внутри которого мы и выполняем `cd`.


## Узнаём, какие библиотеки нужны команде/библиотеке

Чтобы узнать, какие динамические библиотеки нужны программе или библиотеке и как они будут разрешены при запуске, используйте команду `ldd`:

```
$ ldd /usr/lib/systemd/systemd
    linux-vdso.so.1 (0x00007fff7e7c6000)
    libsystemd-shared-239.so => /usr/lib/systemd/libsystemd-shared-239.so (0x00007f265acbd000)
    librt.so.1 => /lib64/librt.so.1 (0x00007f265ac7e000)
    libseccomp.so.2 => /lib64/libseccomp.so.2 (0x00007f265ac3a000)
    libselinux.so.1 => /lib64/libselinux.so.1 (0x00007f265ac0e000)
    ...
    libunistring.so.2 => /lib64/libunistring.so.2 (0x00007f265a076000)
    libsepol.so.1 => /lib64/libsepol.so.1 (0x00007f2659fc1000)
    libudev.so.1 => /lib64/libudev.so.1 (0x00007f2659f99000)
    libm.so.6 => /lib64/libm.so.6 (0x00007f2659e15000)
```

## Узнаём, что лежит внутри файла

Чтобы определить тип содержимого, находящегося в файле, используйте команду `file`:

```
$ file Pictures/wayland-screenshot.png 
Pictures/wayland-screenshot.png: PNG image data, 1920 x 1080, 8-bit/color RGBA, non-interlaced
$ file dev/gnome-builder/src/main.c 
dev/gnome-builder/src/main.c: C source, UTF-8 Unicode text
```

## Многократный запуск команды

Чтобы запускать команду каждые несколько секунд (по умолчанию две) и смотреть на её вывод, воспользуйтесь командой `watch <команда>`.


## Время на запуск команды

Чтобы узнать, сколько времени уходит на запуск команды, используйте `time <команда>`.


## Системные вызовы команды

Чтобы узнать, какие системные вызовы совершает программа, введите `strace <команда>`.


## Запоминаем набираемую команду

Если вы набираете какую-то команду и вам по какой-то причине нужно прерваться и, например, ввести другую команду, вы можете «запомнить» то, что вы ввели комбинацией Ctrl+U, а затем вставить комбинацией Ctrl+Y.


## Выкачиваем сайты

Чтобы выкачать сайт используйте команду `wget --random-wait -r -p -e robots=off -U mozilla <адрес сайта>`.


## Проводим туннели

С помощью команды `ssh -N -L 2001:localhost:80 somemachine` можно создать туннель от 80 порта на удалённой машине до 2001 на локальной.

