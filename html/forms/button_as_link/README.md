# При натисканні на кнопку перейти за посиланням

```html
  <form action="/dir/goto.htm" target="_blank">
    <button>Відкрити сторінку</button>
  </form>
```

## Submit та звичайні кнопки (Bootstrap)

```html
<a href="#somewhere" class="btn btn-primary">Go somewhere</a>
```

<hr>

```html
  <form id="exampleForm" action="/signup/" method="POST">
    <button type="submit" class="btn btn-primary">Реєстрація</button>
  </form>
```
```javascript
<script>
  ...
  $("#exampleForm").submit(function(e)
  {
    ...
  });
</script>
```

<hr>

```html
  <input type="button" id="bGo" value="Перейти" class="btn btn-primary" />
```
```javascript
<script>
  ...
  $("#bGo").click(function(e)
  {
    ...
  });
</script>
```

<button type="submit" class="btn btn-outline-success btn-sm w-100">Редагувати</button>
			
