# mkdir

Создать директорию _'newdir'_:

{% include cl.htm cmd="mkdir newdir" %}

Создать цепочку директорий

```
dir1
  |___ dir2
         |___ dir3`
```

{% include cl.htm cmd="mkdir -p ./dir1/dir2/dir3" %}



Удаляем созданные директории и добавляем к опцию `-v`: получаем подтверждение о каждом созданном каталоге

{% include cl.htm cmd="rm -rf ./dir1" %}

{% include cl.htm cmd="mkdir -pv ./dir1/dir2/dir3"
small="
mkdir: created directory './dir1'
mkdir: created directory './dir1/dir2'
mkdir: created directory './dir1/dir2/dir3'
" %}


Создаем директорию _'public'_ с правами _777_:

{% include cl.htm cmd="mkdir -m777 public" %}

{% include cl.htm cmd="ls -lah"
small="
total 16K
drwxrwxr-x  4 olex olex 4,0K 20-02-23 ./
drwxr-xr-x 38 olex olex 4,0K 20-02-22 ../
drwxrwxr-x  3 olex olex 4,0K 20-02-23 dir1/
drwxrwxrwx  2 olex olex 4,0K 20-02-23 public/
" %}

А сейчас, дискотека!

{% include cl.htm cmd="mkdir -pv ./one/{two1,two2,two3}/three"
small="
mkdir: created directory './one'
mkdir: created directory './one/two1'
mkdir: created directory './one/two1/three'
mkdir: created directory './one/two2'
mkdir: created directory './one/two2/three'
mkdir: created directory './one/two3'
mkdir: created directory './one/two3/three'
" %}


Удаляем все и делаем еще круче:

{% include cl.htm cmd="rm -rf ~/temp/*" %}

{% include cl.htm cmd="mkdir -pv ./one/{two1,two2,two3}/{th1,th2,th3}"
small="
mkdir: created directory './one'
mkdir: created directory './one/two1'
mkdir: created directory './one/two1/th1'
mkdir: created directory './one/two1/th2'
mkdir: created directory './one/two1/th3'
mkdir: created directory './one/two2'
mkdir: created directory './one/two2/th1'
mkdir: created directory './one/two2/th2'
mkdir: created directory './one/two2/th3'
mkdir: created directory './one/two3'
mkdir: created directory './one/two3/th1'
mkdir: created directory './one/two3/th2'
mkdir: created directory './one/two3/th3'
" %}


Такой фокус работает не только с командой mkdir, например:

{% include cl.htm cmd="rm -rfv one/{two1,two2,two3}"
small="
removed directory 'one/two1/th2'
removed directory 'one/two1/th1'
removed directory 'one/two1/th3'
removed directory 'one/two1'
removed directory 'one/two2/th2'
removed directory 'one/two2/th1'
removed directory 'one/two2/th3'
removed directory 'one/two2'
removed directory 'one/two3/th2'
removed directory 'one/two3/th1'
removed directory 'one/two3/th3'
removed directory 'one/two3'
" %}


{% include cl.htm cmd="ls -lah"
small="
total 12
drwxrwxr-x  3 olex olex 4096 20-02-23 ./
drwxr-xr-x 38 olex olex 4096 20-02-22 ../
drwxrwxr-x  2 olex olex 4096 20-02-23 one/
" %}

