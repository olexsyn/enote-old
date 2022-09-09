# Додати провідний нуль

Просто додавайте провідний нуль у любому випадку, а потім використовуйте slice(-2), щоб отримати останні два символи, наприклад:

```javascript
('0' + currentDate.getHours()).slice(-2)
```
[Докладніше про slice...](https://learn.javascript.ru/string#poluchenie-podstroki)


### Вставляємо дату у поле введення

html:

```html
<div>
    <label>Дата реєстрації</label>
    <input type="text" id="tRegDt" value="{{ REGDT }}" />
</div>

<div>
    <input type="button" id="bToday" value="Сьогодні" />
</div>
```

javascript:

```javascript
    $("#bToday").click(function(e)
    {
        e.preventDefault();
        let today = new Date();
        let date_str =  today.getFullYear() + '-' +
                ('0' + (today.getMonth() + 1)).slice(-2) + '-' +
                ('0' +  today.getDate()      ).slice(-2);
        $("#tRegDt").val(date_str);
    });
```
