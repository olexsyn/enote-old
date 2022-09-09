## Мой шаблон для командной строки


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



{% include f.htm f="test2.md" %}
