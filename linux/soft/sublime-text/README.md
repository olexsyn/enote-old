# Sublime Text

[Как можно подправить package](edit_package) (на примере темы Afterglow)

[Sublime-Text Shortcuts](https://shortcutworld.com/Sublime-Text/linux/Sublime-Text_Shortcuts)

## Плагины

Сначала необходимо установить Package Control: `Tools` -> `Command Palette` -> `Install Package Control` 

После установки, либо аналогичным способом, либо через <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> вводим и находим `Package Control: Install Package`

Из списка команд нам доступно установка пакетов, соответственно их удаление, добавление репозитория пакета, поиск пакетов, обновление и т.д.

- ![v][v] **AutoBackups** <https://packagecontrol.io/packages/AutoBackups> - сохраняет версии редактируемых файлов
- ![v][v] **ColorHighlight** https://github.com/Monnoroch/ColorHighlight - подсвечивает кодировку цвета (вместо  GutterColor и ColorHighlighter)
- ![x][c] **ColorHighlighter** https://github.com/Monnoroch/ColorHighlighter
- ![?][q] **Emmet** <https://docs.emmet.io/abbreviations/syntax/>
- ![x][c] **ColorPicker** <https://github.com/weslly/ColorPicker> (<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>C</kbd>) Глючный, как сапожник!
- ![v][v] **Trimmer** <https://github.com/jonlabelle/Trimmer> - удаляет предваряющие/заключающие/и_прочие пробелы и пробельные символы (<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>S</kbd>)
- ![v][v] Тема **Afterglow** <https://github.com/YabataDesign/afterglow-theme/blob/master/README.md>
- ![v][v] **SidebarSeparator** <https://packagecontrol.io/packages/SidebarSeparator> - возможность вставлять разделитель в списке открытых файлов 
- ![v][v] **Sidebar Tools** <https://packagecontrol.io/packages/SideBarTools> - Some useful tools to add to your sidebar context menu
- ![x][c] **Sidebar Enhancements** https://github.com/titoBouzout/SideBarEnhancements - типа Sidebar Tools, но много дохрена и мне практически не нужное
- ![?][q] **Table Cleaner** for Sublime Text 3 <https://packagecontrol.io/packages/Table%20Cleaner> (<kbd>Alt</kbd>+<kbd>;</kbd>, <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>;</kbd>)
- ![?][q] **BracketHighlighter**
- ![v][v] **rainbow_csv** <https://packagecontrol.io/packages/rainbow_csv> / <https://habr.com/post/429548/>

- ![x][c] https://github.com/ggordan/GutterColor - (потребовалось установить http://www.imagemagick.org/ а для него - **_GNU C compiler_** (пакет `gcc`)
настройках.
- ![?][q] **ZenTabs** - не помню, не использую  
- ![?][q] **RegReplace** <https://facelessuser.github.io/RegReplace/usage/> - Позволяет сохранять последовательности рег.выражений для обработки текстовых файлов. <span style="r">Пока не разобрался</span>  

[v]: /i/pl.png
[q]: /i/qu.png
[c]: /i/rm.png

## My settings

```json
{
    "bold_folder_labels": true,
    "default_line_ending": "unix",
    "detect_indentation": true,
    // "font_face": "Droid Sans Mono Regular",
    "font_face": "JetBrains Mono",
    "font_size": 13,
    "theme": "Default Dark.sublime-theme",
    "color_scheme": "Mariana.sublime-color-scheme",
    "ignored_packages": ["Vintage",],

    // Стовпці для відображення вертикальних лінійок
    "rulers": [80,],

    // Установіть значення true, щоб вставляти пробіли під час натискання табуляції
    "translate_tabs_to_spaces": false,

    // Вимикає горизонтальне прокручування, якщо ввімкнено.
    // Може бути встановлено на true, false або "auto", для яких його буде вимкнено
    // вихідний код, і в іншому випадку включено.
    "word_wrap": false,

    // Встановіть значення, відмінне від 0, щоб примусово обтікати цей
    // стовпець, а не ширину вікна. Перегляньте "wrap_width_style" для
    // додаткових параметрів.
    "wrap_width": 0,

    "show_definitions": false,
    "sidebar_size_13": true,
    "tabs_small": true,
    "margin": 0,
    "move_to_limit_on_up_down": true,
    "predawn_findreplace_small": true,
    "predawn_tabs_small": true,


    // Додає пробіли до першої відкритої дужки під час відступу. Потрібно ввімкнути auto_indent.
    "indent_to_bracket": true,

    "draw_white_space": ["all_tabs", "selection"],

    // Керує способом малювання пробілу, що не є ASCII.
    // - "none": дослівно намалювати пробіл Юнікод, наприклад. приховування пробілів нульової ширини.
    // - "punctuation": намалюйте кодові точки пробілу Unicode, визначеного як пунктуація. Це включає NBSP, але виключає ідеографічний простір CJK.
    // - "all": намалювати кодові точки всіх символів пробілу, що не є ASCII.
    "draw_unicode_white_space": "all",

    // Вирізайте пробіли під час збереження лише для тих частин файлу, які ви змінили. Якщо в інших частинах файлу є пробіли в кінці, вони залишаються окремо.
    "trim_only_modified_white_space": true,

    // Установіть значення true, щоб останній рядок файлу закінчувався символом нового рядка під час збереження
    "ensure_newline_at_eof_on_save": true,

    // Керує видаленням пробілу в кінці під час збереження.
    // - "none": не видаляти кінцеві пробіли під час збереження.
    // - "all": Видалити всі пробіли в кінці під час збереження.
    // - "not_on_caret": видаляйте лише пробіли, які не впливатимуть
    //                   на каретку.
    //                   Якщо використовується разом із "save_on_focus_lost" і певними
    // середовищами робочого столу, через які програма часто втрачає
    // фокус, це дозволяє уникнути стрибків курсору.
    "trim_trailing_white_space_on_save": "all",

    // Установіть значення true, щоб автоматично зберігати файли під час переходу до іншого файлу чи програми
    "save_on_focus_lost": false,

    // Обрізає пробіли, додані auto_indent під час переміщення каретки з рядка.
    "trim_automatic_white_space": true,

    // Установіть значення false, щоб вимкнути напрямні відступів.
    // Колір і ширину напрямних відступів можна налаштувати шляхом редагування
    // відповідний файл .tmTheme і вказуючи кольори "guide",
    // "activeGuide" і "stackGuide"
    "draw_indent_guides": true,
    /*"trim_trailing_white_space_on_save": "none",*/
}
```


**Key Bindings:**

```json
[
	{ "keys": ["f8"], "command": "toggle_setting", "args": {"setting": "word_wrap"}},

	{ "keys": ["ctrl+d"], "command": "duplicate_line" },
	{ "keys": ["ctrl+shift+d"], "command": "run_macro_file", "args": {"file": "res://Packages/Default/Delete Line.sublime-macro"} },

	{ "keys": ["shift+f9"], "command": "sort_lines", "args": {"remove_duplicates": true} },
	{ "keys": ["ctrl+alt+shift+f9"], "command": "sort_lines", "args": {"reverse": true} },

	{ "keys": ["ctrl+2"], "command": "show_overlay", "args": {"overlay": "goto", "text": "@"} },
	{ "keys": ["ctrl+;"], "command": "show_overlay", "args": {"overlay": "goto", "text": ":"} },
	{ "keys": ["ctrl+3"], "command": "show_overlay", "args": {"overlay": "goto", "text": "#"} },

	{ "keys": ["ctrl+alt+w"], "command": "swap_case" },

	{ "keys": ["ctrl+r"], "command": "show_panel", "args": {"panel": "replace", "reverse": false} },
	{ "keys": ["ctrl+alt+a"], "command": "trim_leading_whitespace" },

	{ "keys": ["ctrl+alt+w"], "command": "next_bookmark" },
	{ "keys": ["ctrl+alt+u"], "command": "prev_bookmark" },
	{ "keys": ["ctrl+alt+o"], "command": "set_mark" },

	{ "keys": ["alt+shift+up"], "command": "select_lines", "args": {"forward": false} },
	{ "keys": ["alt+shift+down"], "command": "select_lines", "args": {"forward": true} },

	{ "keys": ["ctrl+b"], "command": "toggle_bookmark" },

]
```
