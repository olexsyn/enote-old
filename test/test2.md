## Мой шаблон для командной строки


### Одна строка с командой

{% raw %}
```

```
rsync --port=7777 ONLY
```

```
{% endraw %}

```
rsync --port=7777 ONLY
```



### Команда и строки вывода информации

{% raw %}
```

```
"rsync --port=7777 mymachine.example.com::pickup/"


Hello! Welcome to Martin's rsync server.
drwxr-xr-x        4096 2009/08/23 08:56:19 .
-rw-r--r--           0 2009/08/23 08:56:19 article21.html
-rw-r--r--           0 2009/08/23 08:56:19 design.txt
-rw-r--r--           0 2009/08/23 08:56:19 figure1.png
```
```
{% endraw %}


```
"rsync --port=7777 mymachine.example.com::pickup/"


Hello! Welcome to Martin's rsync server.
drwxr-xr-x        4096 2009/08/23 08:56:19 .
-rw-r--r--           0 2009/08/23 08:56:19 article21.html
-rw-r--r--           0 2009/08/23 08:56:19 design.txt
-rw-r--r--           0 2009/08/23 08:56:19 figure1.png
```


### Команда и большое кол-во выводимой информации

{% raw %}
```

```
"rsync --port=7777 mymachine.example.com::pickup/"
small="Hello! small Welcome to Martin's rsync server.
drwxr-xr-x        4096 2009/08/23 08:56:19 .
-rw-r--r--           0 2009/08/23 08:56:19 article21.html
-rw-r--r--           0 2009/08/23 08:56:19 design.txt
-rw-r--r--           0 2009/08/23 08:56:19 figure1.png
```
```
{% endraw %}


```
"rsync --port=7777 mymachine.example.com::pickup/"
small="Hello! small Welcome to Martin's rsync server.
drwxr-xr-x        4096 2009/08/23 08:56:19 .
-rw-r--r--           0 2009/08/23 08:56:19 article21.html
-rw-r--r--           0 2009/08/23 08:56:19 design.txt
-rw-r--r--           0 2009/08/23 08:56:19 figure1.png
```



{% include f.htm f="test2.md" %}
