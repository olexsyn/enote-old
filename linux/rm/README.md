# rm

видалення файлів і каталогів

---

**Загальний синтаксис**

    rm [OPTIONS]... FILE...

За замовчуванням, коли виконується без будь-яких параметрів, **rm** не видаляє каталоги та не запитує користувача, чи продовжувати видалення даних файлів.

**видалити один файл**:

{% include cl.htm cmd="<b>rm</b> filename" %}

Якщо файл не захищений від запису, його буде видалено без попередження. У разі успіху команда не видає жодного результату і повертає нуль.

Якщо у вас немає дозволів на запис у батьківському каталозі, ви отримаєте помилку «Операція не дозволена».

Під час видалення файлів, захищених від запису, команда запропонує вам підтвердження, як показано нижче:

{% include cl.htm cmd="<b>rm</b> filename"
out="rm: remove write-protected regular empty file 'filename'?" %}

Введіть <kbd>Y</kbd> і натисніть <kbd>Enter</kbd>, щоб видалити файл.

Опція `-f` вказує **rm** ніколи не запитувати користувача та ігнорувати неіснуючі файли та аргументи.

{% include cl.htm cmd="<b>rm</b> -f filename" %}

Якщо ви хочете отримати інформацію про те, що видаляється, скористайтеся параметром -v (verbose - багатослівний):

{% include cl.htm cmd="<b>rm</b> -v filename"
out="removed 'filename'" %}


**Видалити кілька файлів одночасно**. Для цього передайте імена файлів як аргументи, розділені пробілом:

{% include cl.htm cmd="<b>rm</b> file1 file2 file3" %}

Можна використовувати **регулярні вирази** для відповідності кільком файлам. Наприклад, щоб видалити всі _.png_ файли в поточному каталозі:

{% include cl.htm cmd="<b>rm</b> *.png" %}

Перед використанням команди **rm** з регулярним виразом бажано перевірити його роботу з командою **[ls](../ls)**, щоби бачити, які файли будуть видалені.

**Видалити один або кілька порожніх каталогів**, скористайтеся опцією `-d`:

{% include cl.htm cmd="<b>rm</b> -d dirname" %}

`rm -d` функціонально ідентичний команді `rmdir`.

**Рекурсивно видалити непусті каталоги та всі файли в них**, використовуйте параметр `-r` (recursive - рекурсивний):

{% include cl.htm cmd="<b>rm</b> -r dirname" %}

**Підказка перед видаленням**

Параметр `-i` вказує **rm** запитувати користувача перед видаленням кожного файлу. Введіть <kbd>Y</kbd>, <kbd>Enter</kbd> щоб видалити файл.

{% include cl.htm cmd="<b>rm</b> -i file1 file2"
out="rm: remove regular empty file 'file1'? y 
rm: remove regular empty file 'file2'?" %}
 
При видаленні більше трьох файлів або **рекурсивному видаленні каталогу**, щоб отримати **єдиний запит для всієї операції**, скористайтеся параметром `-I`. Вам буде запропоновано підтвердити видалення всіх даних файлів і каталогів:

{% include cl.htm cmd="<b>rm</b> -I file1 file2 file3 file4"
out="rm: remove 4 arguments?" %}

Якщо даний каталог або файл у каталозі захищені від запису, команда **rm** запропонує вам підтвердити операцію. Щоб **видалити каталог без запиту**, скористайтеся опцією `-f`:

{% include cl.htm cmd="<b>rm</b> -rf dirname" %}

Команда `rm -rf` дуже небезпечна, і її слід використовувати з особливою обережністю!

## rmdir --help

{% include cl.htm cmd="<b>rm</b> --help"
out="Usage: rm [OPTION]... [FILE]...
Remove (unlink) the FILE(s).

  -f, --force           ignore nonexistent files and arguments, never prompt
  -i                    prompt before every removal
  -I                    prompt once before removing more than three files, or
                          when removing recursively; less intrusive than -i,
                          while still giving protection against most mistakes
      --interactive[=WHEN]  prompt according to WHEN: never, once (-I), or
                          always (-i); without WHEN, prompt always
      --one-file-system  when removing a hierarchy recursively, skip any
                          directory that is on a file system different from
                          that of the corresponding command line argument
      --no-preserve-root  do not treat '/' specially
      --preserve-root   do not remove '/' (default)
  -r, -R, --recursive   remove directories and their contents recursively
  -d, --dir             remove empty directories
  -v, --verbose         explain what is being done
      --help     display this help and exit
      --version  output version information and exit

By default, rm does not remove directories.  Use the --recursive (-r or -R)
option to remove each listed directory, too, along with all of its contents.

To remove a file whose name starts with a '-', for example '-foo',
use one of these commands:
  rm -- -foo

  rm ./-foo

Note that if you use rm to remove a file, it might be possible to recover
some of its contents, given sufficient expertise and/or time.  For greater
assurance that the contents are truly unrecoverable, consider using shred.

GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
Full documentation at: <http://www.gnu.org/software/coreutils/rm>
or available locally via: info '(coreutils) rm invocation'
" %}


## Див. також:

- [rmdir](../rmdir)
- [unlink](../unlink)
- <http://www.gnu.org/software/coreutils/rm>

