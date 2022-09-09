# tar

[tar --help на RU](rus_help)

## Несколько примеров

### Создать

tar-архив с именем primer.tar содержащий файл /home/ans/primer.txt

    tar -cf primer.tar /home/ans/primer.txt


tar.gz-архив с сжатием Gzip с именем arch.tgz содержащий все файлы и каталоги текущего каталога

    tar -czf arch.tgz ./.

`./` - текущий каталог, `.` - всё

:arrow_right: такие архивы могут иметь как двойное **.tar.gz**, так и традиционное **.tgz** расширение.

Создать tar.gz-архив с именем pages.tgz содержащий каталог pages со всеми вложенными файлами и каталогами

    tar -czf pages.tgz ./pages

Создать архив **update.tgz** из списка файлов, перечисленных в файле **update.lst**:

    tar -czf update.tgz -T update.lst

Cоздать tar-архив с сжатием Bzip2 по имени primer.tar.bz

    tar -cjf primer.tar.bz2 /home/primer.txt

Создать архив директории **temp**, исключая файлы/директории с начальной тильдой в расширении

    tar -c -f archive.tar --exclude '*.~*' temp

Создать архив директории **temp**, исключая файлы/директории **.gitignore**

    tar -c -f archive.tar --exclude-from=./.gitignore temp

Создать архив директории **site.org.ua**, исключая файлы/директории из **site.org.ua/.tarignore**

    tar -czf swimorgua.tgz --exclude-from=./site.org.ua/.tarignore site.org.ua

файл может быть таким:

```
*.~*
*.del
*.tgz
__ee/
__logs/
_data/appl/*.xls
site.org.ua/download/
file.lst
```

еще: http://wiki.enchtex.info/tools/console/tar

### Распаковка

Распаковать архива primer.tar в текущую папку

    tar -xf primer.tar

Распаковать tar-архив с Bzip2

    tar -xjf primer.tar.bz


Пример sh-ника, с "длинными" опциями:

```sh
echo "tar bin..."
tar --create --gzip --exclude-vcs --file bin.tgz bin
echo "tar etc..."
tar --create --gzip --exclude-vcs --file etc.tgz etc
echo "tar lib..."
tar --create --gzip --exclude-vcs --file lib.tgz lib
#echo "tar src..."
#tar --create --gzip --exclude-vcs --file src.tgz src
#echo "tar storage..."
#tar --create --gzip --exclude-vcs --file storage.tgz storage
echo "tar t..."
tar --create --gzip --exclude-vcs --file t.tgz t
echo "tar template..."
tar --create --gzip --exclude-vcs --file template.tgz template
echo "tar www..."
tar --create --gzip --exclude-vcs --file www.tgz www
echo "end of tar mailua"﻿
```

<span class="warn">TODO!</span> Создание многотомного архива

linux/commands/split#razrezanie_arxivov_tar_na_letu

