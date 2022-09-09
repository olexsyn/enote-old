# rmdir

видалення каталогів, якщо вони порожні

---

Команда **rmdir** корисна, коли треба видалити каталог, лише якщо він порожній, без необхідності перевіряти, чи є каталог порожнім чи ні.

Синтаксис:

    rmdir [OPTION]... DIRECTORY...

Якщо каталог не порожній, ви отримаєте помилку.

У цьому випадку вам потрібно буде використати команду **[rm](../rm)** або вручну видалити вміст каталогу, перш ніж використати команду **rmdir**.

Можна вказати повний шлях до каталогу, наприклад:
У наступному прикладі буде спроба видалення каталогу `dir1`, що знаходиться в каталозі `/tmp`.

{% include cl.htm cmd="<b>rmdir</b> /tmp/dir1" %}

Ви також можете видалити каталог та всі його каталоги за допомогою опції `-p`.

{% include cl.htm cmd="<b>rmdir</b> -p /tmp/dir1" %}

У цьому прикладі буде спроба видалення каталогу `dir1`, що знаходиться в каталозі `/tmp`. Якщо спроба вдасться, команда спробує видалити `/tmp`. Робота **rmdir** буде продовжуватися доти, доки не виникне помилка або не буде видалено все вказане дерево.


## rmdir --help

{% include cl.htm cmd="<b>rmdir</b> --help"
out="Usage: rmdir [OPTION]... DIRECTORY...
Remove the DIRECTORY(ies), if they are empty.

      --ignore-fail-on-non-empty
                  ignore each failure that is solely because a directory
                    is non-empty
  -p, --parents   remove DIRECTORY and its ancestors; e.g., 'rmdir -p a/b/c' is
                    similar to 'rmdir a/b/c a/b a'
  -v, --verbose   output a diagnostic for every directory processed
      --help     display this help and exit
      --version  output version information and exit

GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
Full documentation at: <http://www.gnu.org/software/coreutils/rmdir>
or available locally via: info '(coreutils) rmdir invocation'
" %}


## Див. також:
- [rm](../rm)
- <http://www.gnu.org/software/coreutils/rmdir>
