# Sublime Text

[Как можно подправить package](edit_package) (на примере темы Afterglow)

[Sublime-Text Shortcuts](https://shortcutworld.com/Sublime-Text/linux/Sublime-Text_Shortcuts)

## Плагины

Сначала необходимо установить Package Control: `Tools` -> `Command Palette` -> `Install Package Control` 

После установки, либо аналогичным способом, либо через <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> вводим и находим `Package Control: Install Package`

Из списка команд нам доступно установка пакетов, соответственно их удаление, добавление репозитория пакета, поиск пакетов, обновление и т.д.

- ![v][v] **Emmet** <https://docs.emmet.io/abbreviations/syntax/>
- ![v][v] **ColorPicker** <https://github.com/weslly/ColorPicker> (<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>C</kbd>)
- ![v][v] **AutoBackups** <https://packagecontrol.io/packages/AutoBackups> - сохраняет версии редактируемых файлов
- ![v][v] **Trimmer** <https://github.com/jonlabelle/Trimmer> - удаляет предваряющие/заключающие/и_прочие пробелы и пробельные символы (<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>S</kbd>)
- ![v][v] Тема **Afterglow** <https://github.com/YabataDesign/afterglow-theme/blob/master/README.md>
- ![v][v] **SidebarSeparator** <https://packagecontrol.io/packages/SidebarSeparator> - возможность вставлять разделитель в списке открытых файлов 
- ![v][v] **Sidebar Tools** <https://packagecontrol.io/packages/SideBarTools> - Some useful tools to add to your sidebar context menu
- ![x][c] **Sidebar Enhancements** https://github.com/titoBouzout/SideBarEnhancements - типа Sidebar Tools, но много дохрена и мне практически не нужное
- ![?][q] **Table Cleaner** for Sublime Text 3 <https://packagecontrol.io/packages/Table%20Cleaner> (<kbd>Alt</kbd>+<kbd>;</kbd>, <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>;</kbd>)
- ![?][q] **BracketHighlighter**
- ![v][v] **rainbow_csv** <https://packagecontrol.io/packages/rainbow_csv> / <https://habr.com/post/429548/>

- ![x][c] https://github.com/ggordan/GutterColor - (потребовалось установить http://www.imagemagick.org/ а для него - **_GNU C compiler_** (пакет `gcc`)
- ![x][c] https://github.com/Monnoroch/ColorHighlighter - вместо GutterColor - подсвечивает кодировку цвета (#337ab7, red и др.) в файлах, указанных в его настройках.
- ![?][q] **ZenTabs** - не помню, не использую  
- ![?][q] **RegReplace** <https://facelessuser.github.io/RegReplace/usage/> - Позволяет сохранять последовательности рег.выражений для обработки текстовых файлов. <span style="r">Пока не разобрался</span>  

[v]: /i/pl.png
[q]: /i/qu.png
[c]: /i/rm.png

## My settings

```json
{
	"bold_folder_labels": true,
	"color_scheme": "Packages/User/Color Highlighter/themes/ans-white.tmTheme",
	"default_line_ending": "unix",
	"detect_indentation": false,
	"draw_white_space": "all",
	"font_face": "JetBrains Mono",
	// "font_face": "Droid Sans Mono Regular",
	"font_size": 14,
	"ignored_packages":
	[
		"Vintage",
	],
	"margin": 0,
	"move_to_limit_on_up_down": true,
	"predawn_findreplace_small": true,
	"predawn_tabs_small": true,
	"rulers":
	[
		79
	],
	"scroll_past_end": false,
	"show_definitions": false,
	"sidebar_size_13": true,
	"tabs_small": true,
	"theme": "Default Dark.sublime-theme",
	"translate_tabs_to_spaces": false,
	"trim_automatic_white_space": false,
	"trim_trailing_white_space_on_save": true,
}
```

**Sublime keymap:**

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
