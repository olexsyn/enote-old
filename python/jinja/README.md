# Jinja2

- [Простий приклад](simple_example) а також див. нижче

## Install

{% include cl.htm cmd="pip3 install Jinja2"
out="...
Successfully installed Jinja2-2.11.2 MarkupSafe-1.1.1" %}

На сервере, где установлено окружение (напр. python3.7), необходимо добавить опцию `--user`:

{% include cl.htm cmd="which pip3.7"
out="/usr/local/bin/pip3.7" %}

{% include cl.htm cmd="pip3.7 install Jinja2"
out="...
Could not install packages due to an EnvironmentError: [Errno 13] Permission denied...
Consider using the `--user` option or check the permissions." %}

{% include cl.htm cmd="pip3.7 install --user Jinja2"
out="...
Installing collected packages: MarkupSafe, Jinja2
Successfully installed Jinja2-2.11.2 MarkupSafe-1.1.1" %}


> :warning: **Экспериментальная поддержка Python 3** :nbsp: Jinja 2.7 обеспечивает экспериментальную поддержку Python >= 3.3. Это означает, что все unittests передают новую версию, но там могут быть небольшие ошибки, и поведение может быть непоследовательным. Если вы заметили какие-либо ошибки, сообщите об этом в трекер Jinja.

## Почему Jinja2?

http://python2or3.blogspot.com/2015/08/python.html

Если по вопросу "с какого фреймворка начинать в Питоне" еще есть плюрализм (от "Flask - он легковесный, наращиваешь сам и понимаешь как все работает" до "Django - в нем все есть, а чего нет, быстро доустанавливаешь"), то с шаблонизаторами все упростилось.

До недавнего времени шаблонизаторов было 3-4: Jinja, Mako, Genshi и, конечно, Django Templates.

Собственно, они никуда не делись, Genshi и сейчас используется по умолчанию в Turbogears 2, а Mako - в Pylons/Pyramid.

Но и Turbogears, и Django и Pyramid с недавнего времени поддерживают шаблонизатор, ставший популярным благодаря Flask - Jinja 2.

Ну и, наконец, посмтрим на подборку генераторов статических сайтов (http:_www.staticgen.com/): 11 из 17, в том числе самый популярный Pelican (http:_docs.getpelican.com/) опираются на Jinja2.

Итого - вопрос с выбором шаблонизатора Python  на сегодня не стоит.


## Пример использования Jinja2

https://lectureswww.readthedocs.io/6.www.sync/2.codding/3.templates/jinja2.html

### Hello  name!

```python
# -*- coding: utf-8 -*-
from jinja2 import Template

template = Template('Hello ![pic]( name )!')
print(template.render(name=u'Вася'))
```

  Hello Вася!

### Комментарии

```python
{# Это кусок кода, который стал временно не нужен, но удалять жалко
    {% for user in users %}
        ...
    {% endfor %}
#}
```


### Операторы

См.также https://ru.wikipedia.org/wiki/Оператор_(программирование)

```python
# -*- coding: utf-8 -*-
from jinja2 import Template
text = '{% for item in range(5) %}Hello ![pic]( name )! {% endfor %}'
template = Template(text)
print(template.render(name=u'Вася'))
```

  Hello Вася! Hello Вася! Hello Вася! Hello Вася! Hello Вася!

### Модули

```python
# -*- coding: utf-8 -*-
from jinja2 import Template
template = Template("{% set a, b, c = 'foo', 'фуу', 'föö' %}")
m = template.module
print(m.a)
print(m.b)
print(m.c)
```

  foo
  фуу
  föö

### Макросы

```python
# -*- coding: utf-8 -*-
from jinja2 import Template

template = Template('{% macro foo() %}42{% endmacro %}23')
m = template.module
print(m)
print(m.foo())
```

  23
  42

### Чтение из файла

```python
<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
  </head>
  <body>
    {% for item in range(5) %}
      Hello ![pic]( name )!
    {% endfor %}
  </body>
</html>
```

`jinja2/3.loader/0.file.py` — чтение шаблона из файла

```python
# -*- coding: utf-8 -*-

from jinja2 import Template

html = open('foopkg/templates/0.hello.html').read()
template = Template(html)
print(template.render(name=u'Петя'))
```

Результат рендеринга шаблона `jinja2/3.loader/foopkg/templates/0.hello.html`

```python
<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
  </head>
  <body>

      Hello Петя!

      Hello Петя!

      Hello Петя!

      Hello Петя!

      Hello Петя!

  </body>
</html>
```

### Окружение (Environment)

См.также

http://jinja.pocoo.org/docs/dev/api/#loaders

http://jinja.pocoo.org/docs/dev/api/#jinja2.Environment

### Настройки

#### Загрузчики шаблонов (Loaders)

**FileSystemLoader**

```python
# -*- coding: utf-8 -*-
from jinja2 import Environment, FileSystemLoader

env = Environment(loader=FileSystemLoader('foopkg/templates'))
template = env.get_template('0.hello.html')
print(template.render(name=u'Петя'))
```

Результат рендеринга шаблона jinja2/3.loader/foopkg/templates/0.hello.html

**PackageLoader**

```python
# -*- coding: utf-8 -*-
from jinja2 import Environment, PackageLoader

env = Environment(loader=PackageLoader('foopkg', 'templates'))

template = env.get_template('0.hello.html')
print(template.render(name=u'Петя'))
```

Результат рендеринга шаблона jinja2/3.loader/foopkg/templates/0.hello.html

**DictLoader**

```python
# -*- coding: utf-8 -*-
from jinja2 import Environment, DictLoader

html = '''<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
  </head>
  <body>
    {% for item in range(5) %}
      Hello ![pic]( name )!
    {% endfor %}
  </body>
</html>
'''

env = Environment(loader=DictLoader({'index.html': html}))
template = env.get_template('index.html')
print(template.render(name=u'Петя'))
```

Результат рендеринга шаблона jinja2/3.loader/foopkg/templates/0.hello.html

**FunctionLoader**

```python
# -*- coding: utf-8 -*-
from jinja2 import Environment, FunctionLoader

html = '''<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
  </head>
  <body>
    {% for item in range(5) %}
      Hello ![pic]( name )!
    {% endfor %}
  </body>
</html>
'''


def myloader(name):
    if name ##### 'index.html':
        return html

env = Environment(loader=FunctionLoader(myloader))
template = env.get_template('index.html')
print(template.render(name=u'Петя'))
```

Результат рендеринга шаблона jinja2/3.loader/foopkg/templates/0.hello.html

**PrefixLoader**

```python
# -*- coding: utf-8 -*-
from jinja2 import Environment, FunctionLoader, PackageLoader, PrefixLoader

html = '''<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
  </head>
  <body>
    {% for item in range(5) %}
      Hello ![pic]( name )!
    {% endfor %}
  </body>
</html>
'''


def myloader(name):
    if name ##### 'index.html':
        return html

env = Environment(loader=PrefixLoader({
    'foo': FunctionLoader(myloader),
    'bar': PackageLoader('foopkg', 'templates')
}))
template1 = env.get_template('foo/index.html')
template2 = env.get_template('bar/0.hello.html')
print(template1.render(name=u'Петя'))
print(template2.render(name=u'Петя'))
```

Результат рендеринга шаблона jinja2/3.loader/foopkg/templates/0.hello.html


**ChoiceLoader**

```python
# -*- coding: utf-8 -*-
from jinja2 import Environment, FunctionLoader, PackageLoader, ChoiceLoader

html = '''<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
  </head>
  <body>
    {% for item in range(5) %}
      Hello ![pic]( name )!
    {% endfor %}
  </body>
</html>
'''


def myloader(name):
    if name ##### 'index.html':
        return html

env = Environment(loader=ChoiceLoader({
    FunctionLoader(myloader),
    PackageLoader('foopkg', 'templates')
}))
template1 = env.get_template('index.html')
template2 = env.get_template('0.hello.html')
print(template1.render(name=u'Петя'))
print(template2.render(name=u'Петя'))
```

Результат рендеринга шаблона jinja2/3.loader/foopkg/templates/0.hello.html

**ModuleLoader**

```python
# -*- coding: utf-8 -*-
from jinja2 import Environment, FileSystemLoader, ModuleLoader

# Compile template
Environment(loader=FileSystemLoader('foopkg/templates'))\
    .compile_templates("foopkg/compiled/foopkg.zip",
                       py_compile=True)  # pyc generate, only for python2

# Environment
env = Environment(loader=ModuleLoader("foopkg/compiled/foopkg.zip"))
template = env.get_template('0.hello.html')
print(template.render(name=u'Петя'))
```

Результат рендеринга шаблона jinja2/3.loader/foopkg/templates/0.hello.html

**BaseLoader**

```python
# -*- coding: utf-8 -*-
from os.path import exists, getmtime, join

from jinja2 import BaseLoader, Environment, TemplateNotFound


class FoopkgLoader(BaseLoader):

    def __init__(self, path="foopkg/templates"):
        self.path = path

    def get_source(self, environment, template):
        path = join(self.path, template)
        if not exists(path):
            raise TemplateNotFound(template)
        mtime = getmtime(path)
        with open(path) as f:
            source = f.read()
        return source, path, lambda: mtime ##### getmtime(path)

# Environment
env = Environment(loader=FoopkgLoader())
template = env.get_template('0.hello.html')
print(template.render(name=u'Петя'))
```

Результат рендеринга шаблона jinja2/3.loader/foopkg/templates/0.hello.html

### Шаблон конфига Nginx

```python
server {
         listen ![pic]( SRC_SERVER_PUB_IP ):80;
         servern_name ![pic]( FQDN }} www.{{ FQDN )

          location / {
              proxy_pass         http://![pic]( SRC_SERVER_LOCAL_IP ):80/;
              proxy_redirect     off;

              proxy_set_header   Host             $host;
              proxy_set_header   X-Real-IP        $remote_addr;
              proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
         }
}
```

```python
#!/usr/bin/env python
from jinja2 import Environment, FileSystemLoader

env = Environment(loader=FileSystemLoader('.'))

template = env.get_template('nginx_proxy_conf.tpl')

data = {
    "SRC_SERVER_PUB_IP": "192.168.0.100",
    "SRC_SERVER_LOCAL_IP": "10.0.3.100",
    "FQDN": "example.com"
}

conf = template.render(**data)
print(conf)

open("proxy.nginx.conf", "w").write(conf)
```

```python
server {
         listen 192.168.0.100:80;
         servern_name example.com www.example.com

          location / {
              proxy_pass         http://10.0.3.100:80/;
              proxy_redirect     off;

              proxy_set_header   Host             $host;
              proxy_set_header   X-Real-IP        $remote_addr;
              proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
         }
}
```

### {% extends «Наследование» %}

```html
<!DOCTYPE html>
<html lang="en">
<head>
    {% block head %}
      <link rel="stylesheet" href="style.css" />
      <title>{% block title %}{% endblock %} - My Webpage</title>
      <meta charset='utf-8'>
    {% endblock %}
</head>
<body>
    <div id="content">{% block content %}{% endblock %}</div>
    <div id="footer">
        {% block footer %}
          &copy; Copyright 2008 by <a href="http://domain.invalid/">you</a>.
        {% endblock %}
    </div>
</body>
</html>
```

```python
{% extends "base.html" %}
{% block title %}Index{% endblock %}
{% block head %}
    ![pic]( super() )
    <style type="text/css">
        .important { color: #336699; }
    </style>
{% endblock %}
{% block content %}
    <h1>Index</h1>
    <p class="important">
      Welcome ![pic]( name ) to my awesome homepage.
    </p>
{% endblock %}
```

```python
# -*- coding: utf-8 -*-
from jinja2 import Environment, FileSystemLoader

env = Environment(loader=FileSystemLoader('.'))
template = env.get_template('index.html')
print(template.render(name=u'Петя'))
<!DOCTYPE html>
<html lang="en">
<head>


    <link rel="stylesheet" href="style.css" />
    <title>Index — My Webpage</title>
    <meta charset='utf-8'>

    <style type="text/css">
        .important { color: #336699; }
    </style>

</head>
<body>
    <div id="content">
    <h1>Index</h1>
    <p class="important">
      Welcome Петя to my awesome homepage.
    </p>
</div>
    <div id="footer">

        &copy; Copyright 2008 by <a href="http://domain.invalid/">you</a>.

    </div>
</body>
</html>
```

### Блог

`templates/base.html` — базовый шаблон.

```python
<!DOCTYPE html>
<html lang="en">
<head>
    {% block head %}
      <link rel="stylesheet" href="style.css" />
      <title>{% block title %}{% endblock %} - My Blog</title>
      <meta charset='utf-8'>
    {% endblock %}
</head>
<body>
    <div id="content">{% block content %}{% endblock %}</div>
    <br />
    <br />
    <br />
    <div id="footer">
        {% block footer %}
          &copy; Copyright 2015 by <a href="http://domain.invalid/">you</a>.
        {% endblock %}
    </div>
</body>
</html>
```

Главная страница `templates/index.html` наследуется от `templates/base.html`

```python
{% extends "base.html" %}

{% block title %}Index{% endblock %}
{% block content %}
    <h1>Simple Blog</h1>
    <a href="/article/add">Add article</a>
    <br />
    <br />
    {% for article in articles %}
      ![pic]( article.id }} - (<a href="/article/{{ article.id )/delete">delete</a> |
      <a href="/article/![pic]( article.id )/edit">edit</a>)
      <a href="/article/![pic]( article.id }}">{{ article.title )</a><br />
    {% endfor %}
{% endblock %}
```

`templates/create.html` наследуется от базового шаблона.

```python
{% extends "base.html" %}

{% block title %}Create{% endblock %}
{% block content %}
    <h1>Simple Blog -> EDIT</h1>
    <form action="" method="POST">
        Title:<br>
        <input type="text" name="title" value="![pic]( article.title )"><br>
        Content:<br>
        <textarea name="content">![pic]( article.content )</textarea><br><br>
        <input type="submit" value="Submit">
    </form>
{% endblock %}
```

`templates/read.html` наследуется от базового шаблона.

```python
{% extends "base.html" %}

{% block title %}Index{% endblock %}
{% block content %}
    <h1><a href="/">Simple Blog</a> -> READ</h1>
    <h2>![pic]( article.title )</h2>
    ![pic](  article.content )
{% endblock %}
```

`views.py` — окружение Jinja2.

```python
from models import ARTICLES

from jinja2 import Environment, FileSystemLoader

env = Environment(loader=FileSystemLoader('templates'))


class BaseBlog(object):

    def __init__(self, environ, start_response):
        self.environ = environ
        self.start = start_response


class BaseArticle(BaseBlog):

    def __init__(self, *args):
        super(BaseArticle, self).__init__(*args)
        article_id = self.environ['wsgiorg.routing_args'][1]['id']
        (self.index,
         self.article) = next(((i, art) for i, art in enumerate(ARTICLES)
                               if art['id'] ##### int(article_id)),
                              (None, None))


class BlogIndex(BaseBlog):

    def __iter__(self):
        self.start('200 OK', [('Content-Type', 'text/html')])
        yield str.encode(
            env.get_template('index.html').render(articles=ARTICLES)
        )


class BlogCreate(BaseBlog):

    def __iter__(self):
        if self.environ['REQUEST_METHOD'].upper() ##### 'POST':
            from urllib.parse import parse_qs
            values = parse_qs(self.environ['wsgi.input'].read())
            max_id = max([art['id'] for art in ARTICLES])
            ARTICLES.append(
                {'id': max_id+1,
                 'title': values[b'title'].pop().decode(),
                 'content': values[b'content'].pop().decode()
                 }
            )
            self.start('302 Found',
                       [('Content-Type', 'text/html'),
                        ('Location', '/')])
            return

        self.start('200 OK', [('Content-Type', 'text/html')])
        yield str.encode(
            env.get_template('create.html').render(article=None)
        )


class BlogRead(BaseArticle):

    def __iter__(self):
        if not self.article:
            self.start('404 Not Found', [('content-type', 'text/plain')])
            yield b'not found'
            return

        self.start('200 OK', [('Content-Type', 'text/html')])
        yield str.encode(
            env.get_template('read.html').render(article=self.article)
        )


class BlogUpdate(BaseArticle):

    def __iter__(self):
        if self.environ['REQUEST_METHOD'].upper() ##### 'POST':
            from urllib.parse import parse_qs
            values = parse_qs(self.environ['wsgi.input'].read())
            self.article['title'] = values[b'title'].pop().decode()
            self.article['content'] = values[b'content'].pop().decode()
            self.start('302 Found',
                       [('Content-Type', 'text/html'),
                        ('Location', '/')])
            return
        self.start('200 OK', [('Content-Type', 'text/html')])
        yield str.encode(
            env.get_template('create.html').render(article=self.article)
        )


class BlogDelete(BaseArticle):

    def __iter__(self):
        self.start('302 Found',  # '301 Moved Permanently',
                   [('Content-Type', 'text/html'),
                    ('Location', '/')])
        ARTICLES.pop(self.index)
        yield b''
```

## Links

* [https://eax.me/python-jinja/Работа с HTML-шаблонами в Python при помощи Jinja](https://eax.me/python-jinja/Работа с HTML-шаблонами в Python при помощи Jinja)
* [Templating With Jinja2 in Flask: Essentials](https://code.tutsplus.com/tutorials/templating-with-jinja2-in-flask-essentials--cms-25571) :gb:
* [Templating With Jinja2 in Flask: Date and Time Formatting With moment.js](https://code.tutsplus.com/tutorials/templating-with-jinja2-in-flask-date-and-time-formatting-with-momentjs--cms-25813?_ga=2.240665924.696840753.1545733828-1731101557.1545733828) :gb:


## Links

- <https://lectureswww.readthedocs.io/6.www.sync/2.codding/3.templates/jinja2.html> (есть в wiki)
- [Jinja + Flask](https://pythonru.com/uroki/6-shablony-vo-flask)
- [Jinja2 Templating Engine Tutorial](https://medium.com/@jasonrigden/jinja2-templating-engine-tutorial-4bd31fb4aea3)
