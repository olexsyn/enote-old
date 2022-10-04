# SourcesList

[Apt](../../soft/apt/) downloads packages from one or more software repositories (sources) and installs them onto your computer.

{% include a.htm url="https://debian-handbook.info/browse/ru-RU/stable/apt.html#sect.apt-sources.list" text="См. подробнее" %}


```
cd /etc/apt/sources.list.d
```



```
ls -la
total 48
drwxr-xr-x 2 root root 4096 бер 31 23:38 .
drwxr-xr-x 7 root root 4096 бер 31 23:39 ..
-rw-r--r-- 1 root root   66 бер 25  2020 dropbox.list
-rw-r--r-- 1 root root  189 лип  3  2020 google-chrome.list
-rw-r--r-- 1 root root   54 бер 22  2020 linuxlite.list
-rw-r--r-- 1 root root   56 бер 31  2018 linuxlite.list.save
-rw-r--r-- 1 root root   72 бер 31  2018 otto-kesselgulasch-ubuntu-gimp-xenial.list
-rw-r--r-- 1 root root   72 бер 31  2018 otto-kesselgulasch-ubuntu-gimp-xenial.list.save
-rw-r--r-- 1 root root   56 бер 31 23:38 skype-stable.list
-rw-r--r-- 1 root root   50 бер 22  2020 sublime-text.list
-rw-r--r-- 1 root root 1201 гру 14 16:30 teamviewer.list
-rw-r--r-- 1 root root  132 бер 31  2018 teejee2008-ubuntu-ppa-bionic.list
```


```
cat sublime-text.list
deb https://download.sublimetext.com/ apt/stable/
```
