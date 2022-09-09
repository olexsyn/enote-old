# Favicon для сайта на GitHub Pages

Просто бросить иконку в "корень" репозитория не получится, т.к. в действительности, это не корень сайта и браузер не подхватит ее. 

Например: `https://github.com/olexsyn/e-note/`, где корень - `github.com/`.

Поэтому, лучше указать ее расположение на страницах или в шаблоне:

```html
<link href="{{ site.baseurl }}/favicon.ico" rel="shortcut icon" type="image/png">
```
<small>тут у меня `favicon.ico` в реальности - файл `.png`, поэтому - `image/png`</small>

см. больше на [/html/favicon/]({{ site.baseurl }}/html/favicon/)
