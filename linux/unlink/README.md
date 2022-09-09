# unlink

видалення окремого файлу

---

Синтаксис:

    unlink FILE
    unlink OPTION

Де filename - ім'я файлу, який потрібно видалити. У разі успіху команда не видає жодного результату і повертає нуль.

Команда **unlink** приймає лише два параметри: `--help`, що показує довідку команди та `--version` - інформацію про версію.

Будьте особливо обережні, видаляючи файли за допомогою команди **unlink**, оскільки після видалення файл не може бути повністю відновлений.

На відміну від більш потужної **[rm](../rm)** команди, **unlink** може приймати лише один аргумент, що означає, що ви можете видалити лише один файл. Якщо ви спробуєте видалити більше одного файлу, ви отримаєте помилку «unlink: extra operand».

При **видаленні символічних посилань** за допомогою **unlink**, файл, на який вказує символічне посилання, не видаляється.

Щоб видалити певний файл, вам потрібно мати права на запис у каталозі, що містить цей файл. В іншому випадку ви отримаєте помилку «Permission denied».

У системах GNU/Linux за допомогою **unlink** не можна видалити каталог.


## unlink --help

{% include cl.htm cmd="<b>unlink</b> --help"
out="Usage: unlink FILE
  or:  unlink OPTION
Call the unlink function to remove the specified FILE.

      --help     display this help and exit
      --version  output version information and exit

GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
Full documentation at: <http://www.gnu.org/software/coreutils/unlink>
or available locally via: info '(coreutils) unlink invocation'
" %}


## Див. також:

- [rm](../rm)
- [rmdir](../rmdir)
- <http://www.gnu.org/software/coreutils/unlink>

