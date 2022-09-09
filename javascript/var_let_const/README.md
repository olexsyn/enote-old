# var, let и const

**var**

- ограничена областью видимости функции
- ее значение будет undefined если вы попытаетесь обратиться к ней до ее объявления

**let**

- ограничена областью видимости блока
- вы получите ReferenceError если попытаетесь обратиться к ней до ее объявления

**const**

- ограничена областью видимости блока
- вы получите ReferenceError если попытаетесь обратиться к ней до ее объявления
- не может быть перезаписана

Подробнее:

- {% include a.htm url="https://learn.javascript.ru/let-const" text="learn.javascript.ru" %}
- {% include a.htm url="https://habr.com/ru/post/438880/" text="Когда использовать var, let и const в Javascript" %}


**Keys**: <kbd>var</kbd> <kbd>let</kbd> <kbd>const</kbd>
