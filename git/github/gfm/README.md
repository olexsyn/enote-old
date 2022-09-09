# Мова розмітки GitHub Flavored Markdown

**[Markdown](https://ru.wikipedia.org/wiki/Markdown)** – візуально зрозуміла та зручна при редагуванні мова розмітки для оформлення текстових документів. Зазвичай перетворюється на код [HTML](https://ru.wikipedia.org/wiki/HTML) для відображення інформації в Інтернет. [GitHub](https://github.com) розширив стандартний Markdown, додавши можливість оформлення таблиць (<span class="ques">?</span> лише?). Крім власної розмітки Markdown-текст може містити у собі вставки звичайного HTML-коду.

## Зміст

- [Типографія](#typography)
- [Заголовки](#headers)
- [Параграфи та розриви рядків](#paragraphs)
- [Лінії (розділювачі)](#lines)
- [Виділення тексту](#Emphasis)
- [Списки](#lists)
  + [unordered](unordered)
  + [ordered](ordered)
  + [definition](definition)
  + [task](task)
- [Цитати](#quotes)
- [Виноски](#footnotes)
- [Посилання](#links)
- [Зображення](#images)
- [Спеціальні HTML-символи](#symbols)
- [Код](#code)

Переделать это:

1. Блочные элементы
 + [Блоки кода](#CodeBlocks);
2. Строчные элементы
 + ;
 + [Строки кода](#Code);
 + [Изображения](#Images).


[GitHub Flavored Markdown Spec](https://github.github.com/gfm/)

{% include_relative typography.md %}

{% include_relative headers.md %}

{% include_relative paragraphs.md %}

{% include_relative lines.md %}

{% include_relative lists.md %}

{% include_relative quotes.md %}

{% include_relative footnotes.md %}

{% include_relative links.md %}

{% include_relative images.md %}

{% include_relative code.md %}


It's very easy to make some words **bold** and other words *italic* with Markdown. You can even [link to Google!](http://google.com)




Используйте оператор `if` ???


Дополнительные элементы
-----------------------

### <a name="BackslashEscapes"></a>	Обратный слеш

Может употребляться в Markdown перед специальными символами для того, чтобы они воспринимались в их буквальном (а не служебном) значении. Полный список данных символов приводится ниже:

- `\`  - обратный слеш
- `|`  - символ "pipe", который является разделителем ячеек в таблицах (также можно заменить кодом `&#124;`)
- <kbd>`</kbd> - обратный апостроф
- `*`  - звездочка
- `_`  - символ подчеркивания
- `{}` - фигурные скобки
- `[]` - квадратные скобки
- `()` - круглые скобки
- `#`  - символ решетки
- `+`  - плюс
- `-`  - минус (дефис)
- `.`  - точка
- `!`  - восклицательный знак


<a name="symbols"></a>
{% include_relative symbols.md %}


См. также
---------

- [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
- [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
- <https://paulradzkov.com/2014/markdown_cheatsheet/>
- <https://help.github.com/en/github/writing-on-github/working-with-advanced-formatting>
- <https://github.com/github/linguist/blob/master/lib/linguist/languages.yml>
- [emoji](https://help.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax#using-emoji) / [emoji-cheat-sheet](https://github.com/ikatyang/emoji-cheat-sheet)


[q]: /i/q.png "Вопрос"
