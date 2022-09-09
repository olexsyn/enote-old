# fdisk

В дистрибутивах Linux на KVM и <a href="https://vps.ua/openvz-hosting/" target="_blank" rel="noopener noreferrer">OpenVZ VPS</a>, <b>fdisk</b> является лучшим инструментом для управления разделами диска. Fdisk является текстовой утилитой, довольно проста в работе и зачастую находится в пакете вместе с самим <a href="https://vps.ua/blog/best-linux-distros-for-developers/">дистрибутивом</a>. Используя fdisk, вы можете создать новый раздел, удалить или изменить существующий раздел.

При помощи этой утилиты вы можете создать максимум четыре первичных раздела, и любое количество логических разделов, в зависимости от размера диска.

Имейте в виду, что любое изменение раздела может привести к потере всей информации на нем.

## Использование утилиты

Для начала работы с fdisk используется команда формата <i>fdisk &lt;drive&gt;</i>, где <i>&lt;drive&gt;</i> &#8212; имя устройства, которому необходимо выделить раздел. Например, команда <i>fdisk /dev/sda</i> по умолчанию выберет первый диск на SATA-контроллере. При необходимости создать разделы Linux на нескольких устройствах, придётся выполнять fdisk для каждого из них.


Для проверки количества устройств подключённых к SATA-контроллеру можно применить команду


```ls /dev | grep sd```


Например:

```
[root] # ls /dev | grep sd
sda
sdb
```

Начинаем работу: выбираем нужный диск

```[root] # fdisk /dev/sda```

Утилита поприветствует вас и предложит ввести команду:

```Command (m for help):```

Для примера вызовем список команд:

```
Command (m for help): m
Command action
      a   toggle a bootable flag  
      b   edit bsd disklabel
      c   toggle the dos compatibility flag
      d   delete a partition
      l   list known partition types
      m   print this menu
      n   add a new partition
      o   create a new empty DOS partition table
      p   print the partition table
      q   quit without saving changes
      s   create a new empty Sun disklabel
      t   change a partition's system id
      u   change display/entry units
      v   verify the partition table
      w   write table to disk and exit
      x   extra functionality (experts only)
                                   
Command (m for help):
```

Ниже перевод значений команд на русский:

```
      a   установить/снять флаг загрузочного раздела (утилит запросит номер раздела)
      b   редактировать bsd метку диска
      c   переключить флаг совместимости с dos
      d   удалить раздел
      l    список известных типов разделов
      m   показать это меню
      n   добавить новый раздел
      o   создать новую пустую таблицу разделов в стиле DOS
      p   показать существующую таблицу разделов
      q   выйти без сохранения изменений
      s   создать новый раздел с меткой Sun
      t   изменить метку типа раздела
      u   изменить отображение/запись блоков
      v   проверить таблицу разделов
      w   сохранить изменения и выйти
      x   дополнительные возможности (только для экспертов)
```

Команда <i>fdisk –l</i> выведет список существующих разделов, если таковые существуют.


Для просмотра разделов одного выбранного диска используйте такой вариант этой же команды:


<i>fdisk -l /dev/sda</i>


Приступаем к созданию разделов:


Для начала создадим boot

``` 
Command (m for help): n  
Partition type:
     p     primary (0 primary, 0 extended, 4 free)
     e     extended
```

Программа спрашивает тип раздела. Первичный или логический соответственно. Выбираем первичный и его номер:

```
Command (m for help): n
Partition type:
     p     primary (0 primary, 0 extended, 4 free)
     e     extended
Select (default p): p
Partition number (1-4, default 1): 1
```

Далее, программа спросит о размещении начала раздела(специалисты рекомендуют создавать загрузочный раздел ближе к началу диска):

```
Command (m for help): n
Partition type:
     p     primary (0 primary, 0 extended, 4 free)
     e     extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (4096-784932712): 4096
```

Утилита спросит размер будущего раздела: номер начального и номер конечного цилиндра или размер раздела

```
Command (m for help): n
Partition type:
     p     primary (0 primary, 0 extended, 4 free)
     e     extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (4096-784932712): 4096
Last sector, +sectors or +size{K,M,G} (4096-784932712, default 784932712): +100M
```

Раздел готов, о чем нам сообщит программа:

```
Command (m for help): n
Partition type:
     p     primary (0 primary, 0 extended, 4 free)
     e     extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (4096-784932712): 4096
Last sector, +sectors or +size{K,M,G} (4096-784932712, default 784932712): +100M
Partition 1 of type Linux and of size 100 MiB is set
```

Таким же образом создаём своп-раздел и раздел под программы и библиотеки:

```
Command (m for help): n
Partition type:
     p     primary (1 primary, 0 extended, 3 free)
     e     extended
Select (default p): p
Partition number (1-4, default 2): 2
First sector (196876-784932712): 196876
Last sector, +sectors or +size{K,M,G} (196876-784932712, default 784932712): +8G
Partition 2 of type Linux and of size 8 GiB is set
```

Раздел для свопа создаём из расчёта ОЗУх2 если размер ОЗУ меньше 6 гигабайт и ОЗУх1 если больше.

```
Command (m for help): n
Partition type:
     p     primary (2 primary, 0 extended, 2 free)
     e     extended
Select (default p): p
Partition number (1-4, default 3): 3
First sector (2882342-784932712): 2882342
Last sector, +sectors or +size{K,M,G} (2882342-784932712, default 784932712): +40G
Partition 3 of type Linux and of size 40 GiB is set
```

Создаем расширеный раздел из которого будем создавать логические:

```
Command (m for help): n
Partition type:
     p     primary (2 primary, 0 extended, 2 free)
     e     extended
Select (default p): p
Partition number (1-4, default 3): 3
First sector (1684378-784932712): 1684378
Last sector, +sectors or +size{K,M,G} (1684378-784932712, default 784932712): 784932712
Partition 4 of type Linux and of size 204 GiB is set
```

Создаем 2 логических раздела :

```
Command (m for help): n
All primary partitions are in use
Adding logical partition 5
First sector (1684378-784932712): 1684378
Last sector, +sectors or +size{K,M,G} (1684378-784932712, default 784932712): +100G
Partition 5 of type Linux and of size 100 GiB is set

Command (m for help): n
All primary partitions are in use
Adding logical partition 5
First sector (392466356-784932712): 392466356
Last sector, +sectors or +size{K,M,G} (392466356-784932712, default 784932712): +104G
Partition 5 of type Linux and of size 104 GiB is set
```

Также мы дожны обязательно установить флаг загрузочного раздела и изменить метку своп-раздела:

```
Command (m for help): a
Partition number (1-6): 1
```

Меняем метку свопа (для того чтобы узнать нужный HEX-код, в поле «<i>Hex code (type L to list codes):</i>» введите большую <i>L</i>).

```
Command (m for help): t
Partition number (1-4): 2
Hex code (type L to list codes): 82
Changed system type of partition 2 to 82 (Linux swap)      
Command (m for help): p
```

Сохраняем изменения и выходим.

```
Command (m for help): w
The partition table has been altered!
Calling ioctl() to re-read partition table.
Syncing disks.
```

<https://vps.ua/wiki/fdisk-linux/>
