### Директории и файлы

команда | комментарий
--- | ---
`pwd` | Выводит текущий путь
`ls` | Выводит список файлов и каталогов по порядку
`ls -laX` | Выводит форматированный список всех файлов и директорий, включая скрытые
`cd` | Переход в домашнюю директорию
`cd /home` | Переход в директорию /home
`touch /home/filename2` | Создание пустого файла /home/filename2
`cat /home/filename2` | Показать содержимое файла /home/filename2
`tail /var/log/messages` [more...](tail) | Выводит конец файла. Удобно при работе с логами и большими файлами
`tail -f error.log` [more...](tail) | Выводит конец файла и ожидает следующие строки
`nano /home/filename2` | Редактирование файла /home/filename2
`gedit /home/filename2` | Вторая команда Linux для редактирования файла
`echo "Последняя строчка" \| sudo tee -a /home/filename2` | Добавление к концу файла "Последняя строчка" в файл /home/filename2
`cp /home/user/filename.txt /home/filename.txt` | Копирует /home/user/filename.tx в home/filename.txt
`ln -s /home/user/filename.txt /home/filename` | Cоздает символическую ссылку /home/filename к файлу /home/user/filename.txt
`mkdir /home/user/dirname` [more...](mkdir) | Создание директории с именем dirname
`rmdir /home/user/dirname` | Удаление директории с именем dirname
`rm -rf /home/user/shaman` | Удаление директории с вложенными фалами
`cp -la /dir1 /dir2` | Копирование директорий
`mv /dir1 /dir2` | Переименование директории
`du -sh /home/user/` | Выводит на экран размер заданной директории. Можно использовать для определения размера файлов
`locate filename` | Поиск всех файлов с именем filename

{% include f.htm f="dirs_n_files.md" %}
