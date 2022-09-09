# CSS, подключаемый в дефолтной теме GitHub Pages

Найти его можно, просмотрев код html-страниц:

```html
<link rel="stylesheet" href="/YOUR_REPOSITORY/assets/css/style.css?v=...">
```
Используя некоторые классы мы можем добавлять цвет на GitHub Pages:

```html
Test color of <span class="text-blue">text-blue</span> style.
Test color of <span class="text-red ">text-red </span> style.
Test color of <span class="text-gray-light">text-gray-light</span> style.
Test color of <span class="text-gray">text-gray</span> style.
Test color of <span class="text-gray-dark">text-gray-dark</span> style.
Test color of <span class="text-green">text-green</span> style.
Test color of <span class="text-orange">text-orange</span> style.
Test color of <span class="text-orange-light">text-orange-light</span> style.
Test color of <span class="text-purple">text-purple</span> style.
Test color of <span class="text-white bg-gray-dark">text-white</span> style.
Test color of <span class="text-inherit">text-inherit</span> style.
Test color of <span class="text-pending">text-pending</span> style.
Test color of <span class="bg-pending">bg-pending</span> style.
```

Test color of <span class="text-blue">text-blue</span> style.
Test color of <span class="text-red ">text-red </span> style.
Test color of <span class="text-gray-light">text-gray-light</span> style.
Test color of <span class="text-gray">text-gray</span> style.
Test color of <span class="text-gray-dark">text-gray-dark</span> style.
Test color of <span class="text-green">text-green</span> style.
Test color of <span class="text-orange">text-orange</span> style.
Test color of <span class="text-orange-light">text-orange-light</span> style.
Test color of <span class="text-purple">text-purple</span> style.
Test color of <span class="text-white bg-gray-dark">text-white</span> style.
Test color of <span class="text-inherit">text-inherit</span> style.
Test color of <span class="text-pending">text-pending</span> style.
Test color of <span class="bg-pending">bg-pending</span> style.

Кроме этого, мы можем использовать атрибут style для HTML-тегов:

```html
<p><span style="color: red; font-size: 2em">U</span>t wisis enim ad minim veniam...</p>
```

<p><span style="color: red; font-size: 2em">U</span>t wisis enim ad minim veniam...</p>

<span class="warn">!</span> Однако, надо уточнить, что выбор цветов невелик и цвет начинает "работать" только на _**USERNAME.github.io**_, на **github.com/USERNAME/** он невидим! Т.е. _Preview_ не покажет его, что неудобно. Но, все же...

Пример куска css-кода, подключаемого к дефолтной теме GitHub Pages:

```css

.text-blue {
	color: #0366d6 !important
}
.text-red {
	color: #cb2431 !important
}
.text-gray-light {
	color: #6a737d !important
}
.text-gray {
	color: #586069 !important
}
.text-gray-dark {
	color: #24292e !important
}
.text-green {
	color: #28a745 !important
}
.text-orange {
	color: #a04100 !important
}
.text-orange-light {
	color: #e36209 !important
}
.text-purple {
	color: #6f42c1 !important
}
.text-white {
	color: #fff !important
}
.text-inherit {
	color: inherit !important
}
.text-pending {
	color: #b08800 !important
}
.bg-pending {
	color: #dbab09 !important
}


.bg-white {
	background-color: #fff !important
}
.bg-blue {
	background-color: #0366d6 !important
}
.bg-blue-light {
	background-color: #f1f8ff !important
}
.bg-gray-dark {
	background-color: #24292e !important
}
.bg-gray {
	background-color: #f6f8fa !important
}
.bg-gray-light {
	background-color: #fafbfc !important
}
.bg-green {
	background-color: #28a745 !important
}
.bg-green-light {
	background-color: #dcffe4 !important
}
.bg-red {
	background-color: #d73a49 !important
}
.bg-red-light {
	background-color: #ffdce0 !important
}
.bg-yellow {
	background-color: #ffd33d !important
}
.bg-yellow-light {
	background-color: #fff5b1 !important
}
.bg-purple {
	background-color: #6f42c1 !important
}
.bg-purple-light {
	background-color: #f5f0ff !important
}
.bg-shade-gradient {
	background-image: linear-gradient(180deg, rgba(27, 31, 35, 0.065), rgba(27, 31, 35, 0)) !important;
	background-repeat: no-repeat !important;
	background-size: 100% 200px !important
}
```

[полная версия css-файла]({{ site.baseurl }}/github.css)
