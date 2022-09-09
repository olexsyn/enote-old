## Ссылки

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
{% include a.htm text="Link Description" url="https://link.to" %}
{% include a.htm text="" url="" %}  # для копіювання
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

### Проблема з моїми посиланнями у списках

- {% include a.htm text="Посилання 1" url="https://olexsyn.github.io/" %}
  - {% include a.htm text="Посилання 2" url="https://olexsyn.github.io/e-note/" %}
- {% include a.htm text="Посилання 3" url="https://olexsyn.github.io/" -%}
  - {% include a.htm text="Посилання 4" url="https://olexsyn.github.io/e-note/" %}

Чомусь, темплейт вставляє `<p>` параграфи в код і список роз’їзжається. Поки що таке рішення:

- {% include a.htm text="Посилання 1" url="https://olexsyn.github.io/" -%}.
  - {% include a.htm text="Посилання 2" url="https://olexsyn.github.io/e-note/" -%}.
- {% include a.htm text="Посилання 3" url="https://olexsyn.github.io/" -%}.
  - {% include a.htm text="Посилання 4" url="https://olexsyn.github.io/e-note/" -%}.

- {% include a.htm text="Посилання 1" url="https://olexsyn.github.io/" -%}&nbsp;
  - {% include a.htm text="Посилання 2" url="https://olexsyn.github.io/e-note/" -%}&nbsp;
- {% include a.htm text="Посилання 3" url="https://olexsyn.github.io/" -%}&nbsp;
  - {% include a.htm text="Посилання 4" url="https://olexsyn.github.io/e-note/" -%}&nbsp;


{% include f.htm f="links.md" %}
