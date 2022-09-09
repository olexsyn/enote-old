## Блоки кода {#code}

Отформатированные блоки кода используются в случае необходимости процитировать исходный код программ или разметки.
Для создания блока кода в языке Markdown необходимо каждую строку параграфа начинать  с отступа, состоящего из четырех пробелов или  одного символа табуляции. Блок кода продолжается до тех пор, пока не встретится строка без отступа (или конец текста).  Внутри блока кода амперсанды («&») и угловые скобки («<» и «>») автоматически преобразуются в элементы HTML разметки. Кроме того, следует отметить, что внутри блоков кода обычный синтаксис Markdown не обрабатывается.
Блок кода в Markdown выглядит следующим образом:

Это обычный параграф:

    Это блок кода

### Строки кода

Чтобы отметить фрагмент строки, содержащий код, необходимо окружить его обратными апострофами «\`».  При использовании кодовых фрагментов строк текст будет отображаться в виде моноширинного шрифта.
В отличие от блоков кода, кодовый фрагмент позволяет поместить код внутрь обычного абзаца текста.
Кодовый фрагмент строки в языке Markdown выглядит следующим образом:

~~~
це теж код
~~~

### Escaping Pipe Characters in Tables

You can display a pipe (|) character in a table by using its HTML character code (&#124;).

### Fenced Code Blocks

The basic Markdown syntax allows you to create code blocks by indenting lines by four spaces or one tab. If you find that inconvenient, try using fenced code blocks. Depending on your Markdown processor or editor, you’ll use three backticks (```) or three tildes (~~~) on the lines before and after the code block. The best part? You don’t have to indent any lines!

```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```
The rendered output looks like this:

{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}

### Syntax Highlighting

Many Markdown processors support syntax highlighting for fenced code blocks. This feature allows you to add color highlighting for whatever language your code was written in. To add syntax highlighting, specify a language next to the backticks before the fenced code block.

```json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

The rendered output looks like this:

{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}

{% include f.htm f="code.md" %}
