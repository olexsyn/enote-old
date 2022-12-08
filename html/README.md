# HTML

- [Некоторые `&xxx;` спецсимволы](symbols)
- [favicon для браузеров и устройств](favicon)
- [Огромная Таблица символов Юникода](http://unicode-table.com/ru/)

- [Списки](list)
- [Формы](forms)
  - [Перехід за посиланням за допомогою кнопки](forms/button_as_link)
  - [`<input type=number>`](input_type_number)

[Исходящие ссылки. rel=nofollow,sponsored и пр.](https://support.google.com/webmasters/answer/96569?hl=ru)

##datalist

:boom: TODO

https://www.jotform.com/blog/html5-datalists-what-you-need-to-know-78024/

```html
<label for="exampleDataList" class="form-label">Datalist example</label>
<input class="form-control" list="datalistOptions" id="exampleDataList" placeholder="Type to search...">
<datalist id="datalistOptions">
  <option value="1" label="San Francisco" />
  <option value="2" label="New York" />
  <option value="3" label="Seattle" />
  <option value="4" label="Los Angeles" />
  <option value="5" label="Chicago" />
</datalist>

<label for="exampleDataList" class="form-label">Datalist example</label>
<input class="form-control" list="datalistOptions" id="exampleDataList" placeholder="Type to search...">
<datalist id="datalistOptions">
  <option value="San Francisco" label="1" />
  <option value="New York" label="2" />
  <option value="Seattle" label="3" />
  <option value="Los Angeles" label="4" />
  <option value="Chicago" label="5" />
</datalist>
```
