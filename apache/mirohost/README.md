# Apache і Мирохост

- [Как создать SSL сертификат](https://mirohost.net/support/hosting-technical/kak-sozdat-ssl-sertifikat-v-kontrolnoj-paneli-mirohost)
- [Настройка DKIM подписи](https://mirohost.net/support/hosting-technical/nastrojka-dkim-podpisi)
- [Чому на Mirohost не працюють cgi-скрипти](#cgi-fail)
- [Проблема (?) с SSI в связке Apache и Nginx на Mirohost](#ssi-fail)

<a name="cgi-fail"></a>
### Чому на Mirohost не працюють cgi-скрипти

Увага, на Mirohost'і всі директорії (в тому числі і cgi-bin) створюются з правами 775. Тому скрипти не працюють ніде.
Поки не призначити і скриптам, і директоріям права 755.

Щоб запрацювали скрипти на python необхідно додати розширення "py" до виключеннь зі статичних файлів nginx. Інакше, браузер намагатиметься завантажувати скрипти ".py".
Також, якщо треба щоб працювало таке:

`site.com/dir/file.htm`

"htm" теж треба додати у виключення, але якщо ні, то можна викрутитися так:

`site.com/dir/file/` (index.htm)

Тобто, створити директорію `file` і в неї покласти `index.htm` з вмістом _file.htm_

Далі, у директоріях, де планується запускати скрипти треба прописати свої файли `.htaccess`. В ньому:

Якщо нема наступних інструкцій (однієї, або обох) текст скрипта буде дукуватися у вікні браузера:

```apache
AddHandler cgi-script .py
Options +ExecCGI -MultiViews
```
Якщо нема цієї опції скрипти .pl та .py на моєму локальному Apache
**не показують кирилицю**. Вперше з цим зіткнувся на Linux Lite. 
На сервері Мирохосту все працює і без цієї опції. Але вона і не заважає,
тому просто її залишив, щоб не мати розбіжностей з .htaccess на локалці:

```apache
PassEnv LANG en_US.UTF-8
```
Крім цього, для коректного відображення кирилиці, у скриптах повинна бути строка з `charset=utf-8`:

```python
print("Content-Type: text/html; charset=utf-8\n")
```

Про це ще можна прочитати тут: [Корректное отображение UTF8 в CGI-скриптах]({{ site.baseurl }}/apache/cgi-utf-fix/)

<a name="ssi-fail"></a>

## Проблема (?) с SSI в связке Apache и Nginx на Mirohost

SSI корректно работает только на ссылках типа

`example.com/test/`

а на страницах

`example.com/test/index.htm`  
`example.com/test/something.htm`

не работает

### Решение

В панели управления Mirohost, разделе "Сервер" - "Настройки Nginx" добавить в "Расширения файлов, которые не будут отдаваться как статические файлы nginx'ом" расширение `htm`.

Хостинг-пакет H-85***

## Почта

Отправляю письма через Web mail - все письма на Укр.Нет возвращаются с
ошибкой.  
Сначала думал, что пользователи дают неправильные адреса, пока не
подставил свой.  
Присылаю на почтовый ящик Мирохоста письмо с Укр.Нет - приходит. Делаю
на него ответ - ошибка "The following address(es) failed" (см. ниже).
На другие почтовые сервисы письма доставляются (GMail, ProtonMail и
даже запрещенный Mail.Ru).  
Не могли бы Вы помочь понять в чем проблема и как ее решить?

> Добавьте в настройки зоны запись ТХТ следующего вида:
>
> ```v=spf1 +a +mx include:_spf.mx1.mirohost.net -all```


#### Keys

<button>mirohost</button> <button>ssi</button> <button>apache</button> <button>nginx</button>
