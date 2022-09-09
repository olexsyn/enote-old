# Test

[Пример большой страницы, разделенной на части для удобства редактирования](multi_part_page)

## Contents

- [Visual](#visual)
- [Code](#code)
- [Тест картинок](#тест-картинок)
- [Command Line Template](#command-line-template)
- [Links](#links)
- [Different](#different)

<https://about-me.pp.ua/>

---


## Visual

<span class="ques">?</span> question

<span class="info">i</span> info

<span class="warn">!</span> warning

{% raw %}
```
<span class="ques">?</span> question

<span class="info">i</span> info

<span class="warn">!</span> warning
```
{% endraw %}


## Code

`одиночные кавычки`

```html
<code class="language-plaintext highlighter-rouge">одиночные кавычки</code>
```

---

```тройные кавычки в строку```

```html
<code class="language-plaintext highlighter-rouge">тройные кавычки в строку</code>
```

---

```
строка окруженная тройными кавычками
```

```html
<div class="language-plaintext highlighter-rouge">
	<div class="highlight">
		<pre class="highlight"><code>
		строка окруженная тройными кавычками
		</code></pre>
	</div>
</div>
```

---

    4 пробела в начале строки

```html
<div class="highlight">
	<pre class="highlight"><code>
	4 пробела в начале строки
	</code></pre>
</div>
```

---

<code>текст в теге code...</code>

```html
<code>текст в теге code...</code>
```

---

<code>
строка окруженная тегом code.
</code>

```html
<code>
строка окруженная тегом code.
</code>
```

---

<pre>
строка окруженная тегом pre.
</pre>

```html
<pre>строка окруженная тегом pre.
</pre>
```

---

<pre><code>
строка окруженная тегами pre code.
</code></pre>

```html
<pre><code>
строка окруженная тегами pre code.
</code></pre>
```


## Тест картинок

| desc           | img              | code              |
| -------------: | :--------------: | :---------------- |
| **wa**rning    |  ![](/i/wa.png)  |  `![](/i/wa.png)` |
| **in**fo       |  ![](/i/in.png)  |  `![](/i/in.png)` |
| **qu**estion   |  ![](/i/qu.png)  |  `![](/i/qu.png)` |
| **pl**us       |  ![](/i/pl.png)  |  `![](/i/pl.png)` |
| **r**e**m**ove |  ![](/i/rm.png)  |  `![](/i/rm.png)` |
| **t**a**g**    |  ![](/i/tg.png)  |  `![](/i/tg.png)` |


## Command Line Template


### Одна строка с командой

{% raw %}
```
{% include cl.htm cmd="rsync --port=7777 ONLY" %}
```
{% endraw %}
{% include cl.htm cmd="rsync --port=7777 ONLY" %}


### Команда и строки вывода информации

{% raw %}
```
{% include cl.htm cmd="..." out="..." %}
```

```
{% include cl.htm cmd="rsync --port=7777 mymachine.example.com::pickup/"
out="
Hello! Welcome to Martin's rsync server.
drwxr-xr-x        4096 2009/08/23 08:56:19 .
-rw-r--r--           0 2009/08/23 08:56:19 article21.html
-rw-r--r--           0 2009/08/23 08:56:19 design.txt
-rw-r--r--           0 2009/08/23 08:56:19 figure1.png
" %}
```
{% endraw %}

{% include cl.htm cmd="rsync --port=7777 mymachine.example.com::pickup/"
out="
Hello! Welcome to Martin's rsync server.
drwxr-xr-x        4096 2009/08/23 08:56:19 .
-rw-r--r--           0 2009/08/23 08:56:19 article21.html
-rw-r--r--           0 2009/08/23 08:56:19 design.txt
-rw-r--r--           0 2009/08/23 08:56:19 figure1.png
" %}


### Команда и большое кол-во выводимой информации

{% raw %}
```
{% include cl.htm cmd="rsync --port=7777 mymachine.example.com::pickup/"
small="Hello! small Welcome to Martin's rsync server.
drwxr-xr-x        4096 2009/08/23 08:56:19 .
-rw-r--r--           0 2009/08/23 08:56:19 article21.html
-rw-r--r--           0 2009/08/23 08:56:19 design.txt
-rw-r--r--           0 2009/08/23 08:56:19 figure1.png
" %}
```
{% endraw %}

{% include cl.htm cmd="rsync --port=7777 mymachine.example.com::pickup/"
small="Hello! small Welcome to Martin's rsync server.
drwxr-xr-x        4096 2009/08/23 08:56:19 .
-rw-r--r--           0 2009/08/23 08:56:19 article21.html
-rw-r--r--           0 2009/08/23 08:56:19 design.txt
-rw-r--r--           0 2009/08/23 08:56:19 figure1.png
" %}


## Links

Full [`sql.RawBytes`](https://golang.org/pkg/database/sql/#RawBytes) support.

Full `[sql.RawBytes](https://golang.org/pkg/database/sql/#RawBytes)` support.

### Абсолютные и относительные

Можно указать абсолютную, "от корня", но при этом, нужно использовать переменную _site.baseurl_:

{% raw %}
```
[Apt]({{ site.baseurl }}/linux/soft/apt/)
```
{% endraw %}

или оносительную, от текущей директории:

{% raw %}
```
[Apt](../../soft/apt/)
```
{% endraw %}


### Мои ссылки

Для того, чтобы ссылки на другие сайты открывались в новом окне прописал в `e-note/_includes/a.htm` такой код

{% raw %}
```html
<a href="{{ include.url }}" target="_blank" rel="nofollow">
{%- if include.text -%}
  {{ include.text }}
{%- else -%}
  {{ include.url }}
{%- endif -%}
</a>
```
На страницах ссылка оформляется так:

```
{% include a.htm url="https://link.to" text="Link Description" %}
{% include a.htm url="" text="" %}  # for copy
```
{% endraw %}

Для отличия по цвету (зеленые - локальные, синие - внешние) в css:

```css
a {
	color: green;
	text-decoration: none
}

a[href ^= "http"] {
  color: #0366d6;
}

a[href ^= "mailto"] {
  color: #0366d6;
}
```


## Different

{% assign abs_path = '/linux/soft' -%}

`page.url` | {{ page.url }}
`page.path` | {{ page.path }}
`page.id` | {{ page.id }}
`page.dir` | {{ page.dir }}
`page.name` | {{ page.name }}
`page.categories` | {{ page.categories }}
`site.url` | {{ site.url }}
`site.baseurl` | {{ site.baseurl }}
`abs_path` | {{ abs_path }}



![tags][tg] | test | images | table

<p><span class="HF9Klc iJddsb" style="height:16px;width:16px"><svg focusable="false" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M21.11 2.89A3.02 3.02 0 0 0 18.95 2h-5.8c-.81 0-1.58.31-2.16.89L7.25 6.63 2.9 10.98a3.06 3.06 0 0 0 0 4.32l5.79 5.8a3.05 3.05 0 0 0 4.32.01l8.09-8.1c.58-.58.9-1.34.9-2.16v-5.8c0-.81-.32-1.59-.89-2.16zM20 10.85c0 .28-.12.54-.32.74l-3.73 3.74-4.36 4.36c-.41.41-1.08.41-1.49 0l-2.89-2.9-2.9-2.9a1.06 1.06 0 0 1 0-1.49l8.1-8.1c.2-.2.46-.3.74-.3l5.8-.01A1.05 1.05 0 0 1 20 5.05v5.8zM16 6c1.1 0 2 .9 2 2s-.9 2-2 2-2-.9-2-2 .9-2 2-2z"></path></svg></span> Test</p>

<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> - три кнопки нажаты одновременно

<kbd>Ctrl <kbd>K</kbd>+<kbd>U</kbd></kbd> - Ctrl - удерживается, U и K - поочередно


<https://webhamster.ru/mytetrashare/index/mtb0> - здесь много статей

## Таблиці

GitHub не відібражає цей код як таблицю, а GitHub Pages - відібражає

```one | two | three```

1 | 2 | 3
one | two | three

1 | 2 | 3
--- | --- | ---
one | two | three

1 | --- | one
2 | --- | two
3 | --- | three



Lorem ipsum dolor sit amet, <span class="ques">?</span> consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

test test test test test

```<kbd>test</kbd>, <kbd>images</kbd>, <kbd>table</kbd>```

<kbd>test</kbd>, <kbd>images</kbd>, <kbd>table</kbd>


```![tags][tg] : <var>test, images, table</var>```

![tags][tg] : <var>test, images, table</var>


```
**keys**: <i>test</i>, <i>images</i>, <i>table</i>
```

**keys**: <i>test</i>, <i>images</i>, <i>table</i>


```<small><samp>test, images, table</samp></small>```

<small><samp>test, images, table</samp></small>


[tg]: /i/tg.png "Tags"


tags: ___test___, ___images___, ___table___
