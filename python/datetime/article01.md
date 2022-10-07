# Как использовать модуль datetime в Python

Datetime — важный элемент любой программы, написанной на Python. Этот модуль позволяет управлять датами и временем, представляя их в таком виде, в котором пользователи смогут их понимать.

datetime включает различные компоненты. Так, он состоит из объектов следующих типов:

    date — хранит дату
    time — хранит время
    datetime — хранит дату и время

## Как получить текущие дату и время?

С помощью модуля Python это сделать очень просто. Сначала нужно импортировать класс datetime из модуля datetime, после чего создать объект datetime. Модуль предоставляет метод now(), который возвращает текущие дату и время с учетом локальных настроек.

```python
import datetime

dt_now = datetime.datetime.now()
print(dt_now)
```

    2020-11-14 15:43:32.249588

## Получить текущую дату в Python

Класс date можно использовать для получения или изменения объектов даты. Например, для получения текущей с учетом настроек подойдет следующее:

```python
from datetime import date

current_date = date.today()
print(current_date)
```
    2020-11-14

Текущая дата — 2020-11-14 в формате год-месяц-день соответственно.

## Получить текущее время

Для получения текущего локального времени сперва нужно получить текущие дату и время, а затем достать из этого объекта только время с помощью метода time():

```python
import datetime

current_date_time = datetime.datetime.now()
current_time = current_date_time.time()
print(current_time)
```
    15:51:05.627643

## Компоненты datetime в Python

Модуль datetime в Python может использоваться для получения разных версий времени. Для этого нужно ознакомиться с атрибутами модуля. Используем для этого функцию dir().

```python
import datetime

attr = dir(datetime)
print(attr)
# ['MAXYEAR', 'MINYEAR', '__doc__', '__name__', '__package__', 'date', 'datetime',
# 'datetime_CAPI', 'time', 'timedelta', 'tzinfo']
```

В этом руководстве речь пойдет о следующих элементах:

    date — объекты даты
    datetime — объекты даты и времени
    time — объекты времени
    timedelta — этот атрибут покрывает интервалы и используется для определения прошлых или будущих событий
    Tzinfo — этот атрибут отвечает за часовые пояса

## Как создавать объекты даты и времени

Для создания объекта времени используется класс time из модуля datetime в Python. Синтаксис следующий: datetime.time(hour, minutes, seconds).

В этом примере создается объект времени представленный следующим образом (8, 48, 45).

```python
import datetime

timeobj= datetime.time(8,48,45)
print(timeobj)
```
    08:48:45

Сначала импортируется модуль datetime. После этого создается экземпляр класса (объект time). Затем ему присваивается значение datetime.time(8, 48, 45), где параметры 8, 48 и 45 представляют собой часы, минуты и секунды соответственно.

Для создания объекта даты нужно передать дату с использованием следующего синтаксиса:

```datetime.datetime(year,month,day))```

Такой пример:

```python
import datetime

date_obj = datetime.datetime(2020,10,17)
print(date_obj)
```
Вернет вот такой результат:

    2020-10-17 00:00:00

## Timedelta

timedelta представляет длительность (даты или времени). Модуль datetime включает атрибут timedelta(), который используется для управления датой в Python. Объект timedelta выглядит следующим образом:

```python
td_object =timedelta(days=0, seconds=0, microseconds=0, milliseconds=0, minutes=0, hours=0, weeks=0)
td_object
datetime.timedelta(0)
```
Все аргументы опциональные и их значения по умолчанию равно 0. Они могут быть целыми или числами с плавающей точкой, как положительными, так и отрицательными. Благодаря этому можно выполнять математические операции, такие как сложение, вычитание и умножение.
Как вычислить разницу для двух дат

Посмотрим на несколько примеров вычисления разницы во времени. Предположим, есть два объекта datetime:

```python
first_date = date(2020, 10, 2)
second_date = date(2020, 10, 30)
```
Для получения разницы нужно лишь вычесть значение одного объекта из второго:

```python
from datetime import date

first_date = date(2020, 10, 2)
second_date = date(2020, 10, 30)
delta = second_date - first_date
print(delta)
```
    28 days,0:00:00

Таким образом между 2 и 30 октября 2020 года 28 дней.
Как вычислить разницу двух объектов datetime.time

С помощью timedelta нельзя выполнять манипуляции над объектами time. Например:

```python
from datetime import datetime, timedelta

current_datetime = datetime.now()
current_time = current_datetime.time()
print("Текущее время:", current_time)
tm_after_1_hr = current_time + timedelta(hours=1)
print(tm_after_1_hr)
```
Такой код вернет следующую ошибку:
```
Traceback (most recent call last):
  File "C:\Users\alex\AppData\Local\Programs\Python\Python38\sg_verify.py", line 6, in <module>
    tm_after_1_hr = current_time + timedelta(hours=1)
TypeError: unsupported operand type(s) for +: 'datetime.time' and 'datetime.timedelta'
```

## Как получать прошлые и будущие даты с помощью timedelta

Поскольку timedelta — это длительность, то для получения прошлой или будущей даты нужно добавить объект timedelta к существующему или вычесть из него же. Вот пример нескольких уравнений, где n — это целое число, представляющее количество дней:

```python
import datetime

current_date = datetime.datetime.today()
past_date = datetime.datetime.today() – datetime.timedelta(days=n)
future_date = datetime.datetime.today() – datetime.timedelta(days=n)
```
Если нужно, например, получить дату за прошлые две недели, то достаточно вычесть 14 дней из текущей даты:

```python
import datetime

past_date = datetime.datetime.today() - datetime.timedelta(days=14)
print(past_date)
```
    2020-10-31 16:12:09.142258

Предположим, вы задумали практиковать определенный навык в течение 21 дня. Для получения будущей даты нужно добавить 21 день к текущей дате:


```python
import datetime

future_date = datetime.datetime.today() + datetime.timedelta(days=21)
print(future_date)
```
    2020-12-05 16:14:09.718325

## Другие арифметические операции с timedelta

Значения даты и времени могут сравниваться для определения того, какая из них была раньше или позже. Например:

```python
import datetime

now = datetime.time(9, 31, 0)
next_hour = datetime.time(10, 31, 0)
print('now < next_hour:', now < next_hour)
today = datetime.date.today()
next_week = datetime.date.today() + datetime.timedelta(days=7)
print('today > next_week:', today > next_week)
```
    now < next_hour: True
today > next_week: False

## Часовые пояса

Пока что мы работали с datetime без учета часовых поясов и летнего времени. Но прежде чем переходить к следующим пунктам, нужно разобраться с разницей в абсолютных (naive) и относительных (aware) датах.

Абсолютные даты не содержат информацию, которая бы могла определить часовой пояс или летнее время. Однако с такими намного проще работать.

Относительные же содержат достаточно информации для определения часового пояса или отслеживания изменений из-за летнего времени.
Разница между DST, GMT и UTC

### GMT

Официальный часовой пояс, используемый в некоторых странах Европы и Африки. Он может быть представлен как в 24, так и в 12-часовом форматах. GMT используется для того, чтобы задавать местное время. Например, местное время для Берлина 2020–10–17 09:40:33.614581+02:00 GMT. Для Найроби же это — 2020–10–17 10:40:33.592608+03:00 GMT.

### DST (летнее время)

Страны, которые переходят на летнее время, делают это для того, чтобы дневное время длилось как можно дольше. Во время летнего времени они переводят стрелки своих часов на час вперед и возвращаются обратно осенью.

### UTC (всемирное координированное время)
Временной стандарт для часовых поясов во всем мире. Он позволяет синхронизировать время во всем мире и служит отправной точкой для остальных.

### Как работать с часовыми поясами

Рассмотрим, как создать простой относительный объект datetime:

```python
import datetime

dt_now = datetime.datetime.utcnow()
print(dt_now)
```

Эта программа возвращает объект с абсолютным значением `datetime`. Если же нужно сделать его абсолютным, то нужно явно указать часовой пояс. Как это сделать? В библиотеке datetime в Python нет модуля для работы с часовыми поясами. Для этого нужно использовать другие библиотеки. Одна из таких — `pytz`.

Предположим, нужно получить текущее время для Найроби. Для этого нужно использовать конкретный часовой пояс. Для начала можно с помощью pytz получить все существующие часовые пояса.

```python
import pytz

pytz.all_timezones
```

Вот некоторые из них:

`['Africa/Abidjan', 'Africa/Accra', 'Africa/Addis_Ababa', 'Africa/Nairobi']`

Для получения времени в Найроби:

```python
import pytz
import datetime

tz_nairobi = pytz.timezone("Africa/Nairobi")
dt_nairobi =datetime.datetime.now(tz_nairobi)
print(dt_nairobi)
```
    2020-11-14 17:27:31.141255+03:00

А вот так можно получить время Берлина:

```python
import pytz
import datetime

tz_berlin = pytz.timezone("Europe/Berlin")
dt_berlin =datetime.datetime.now(tz_berlin)
print(dt_berlin)
```
    2020-11-14 15:28:20.977529+01:00

Здесь можно увидеть разницу в часовых поясах разных городов, хотя сама дата одна и та же.
Конвертация часовых поясов

При конвертации часовых поясов в первую очередь нужно помнить о том, что все атрибуты представлены в UTC. Допустим, нужно конвертировать это значение в America/New_York:

```python
import datetime
import pytz

timezone_berlin = '2019-06-29 17:08:00'
tz_ber_obj = datetime.datetime.strptime(timezone_berlin, '%Y-%m-%d %H:%M:%S')
timezone_newyork = pytz.timezone('America/New_York')
timezone_newyork_obj = timezone_newyork.localize(tz_ber_obj)
print(timezone_newyork_obj)
print(timezone_newyork_obj.tzinfo)
```
    2019-06-29 17:08:00-04:00
    America/New_York

### Другие практические примеры

Всегда храните даты в UTC. Вот примеры:

```python
import datetime
import pytz

time_now = datetime.datetime.now(pytz.utc)
print(time_now)
```
Результат для этого кода — 2020-11-14 14:38:46.462397+00:00, хотя локальное время может быть, например, таким 2020-11-14 16:38:46.462397+00:00. А уже при демонстрации даты пользователю стоит использовать метод localize с местными настройками:

```python
import datetime
import pytz

now = datetime.datetime.today()
now_utc = pytz.utc.localize(now)
```
Вернет текущее локальное время — 2020-11-14 16:42:38.228528+00:00.

## Как конвертировать строки в datetime

strptime() в Python — это метод из модуля datetime. Вот его синтаксис:

dateobj = datetime.strptime(date_string, format)

Аргументы формата необязательные и являются строками. Предположим, нужно извлечь текущие дату и время:

```python
import datetime

current_dt = datetime.datetime.now()
print(current_dt)
```
    2020-11-14 16:50:45.049229

Результат будет в формате ISO 8601, то есть YYYY-MM-DDTHH:MM:SS.mmmmmm — формат по умолчанию, что позволяет получать строки в едином формате.

Таблица форматов:
Символ | Описание | Пример
------ | -------- | ------
%a | День недели, короткий вариант |  Wed
%A | Будний день, полный вариант | Wednesday
%w | День недели числом 0-6, 0 — воскресенье | 3
%d | День месяца 01-31 |  31
%b | Название месяца, короткий вариант | Dec
%B | Название месяца, полное название  |  December
%m | Месяц числом 01-12 | 12
%y | Год, короткий вариант, без века | 22
%Y | Год, полный вариант | 2022
%H | Час 00-23  | 17
%I | Час 00-12  | 05
%p | AM/PM  | PM
%M | Минута 00-59  |  41
%S | Секунда 00-59 |  08
%f | Микросекунда 000000-999999 | 548513
%z | Разница UTC | +0100
%Z | Часовой пояс  |  CST
%j | День в году 001-366 | 365
%U | Неделя числом в году, Воскресенье первый день недели, 00-53 | 52
%W | Неделя числом в году, Понедельник первый день недели, 00-53 | 52
%c | Локальная версия даты и времени | Mon Dec 31 17:41:00 2018
%x | Локальная версия даты  |  12/31/18
%X | Локальная версия времени  | 17:41:00
%% | Символ “%” | %

```python
import datetime

date_string = "11/17/20"
date_obj = datetime.datetime.strptime(date_string, '%m/%d/%y')
print(date_obj)
```
    2020-11-17 00:00:00

## Примеры конвертации строки в объект datetime с помощью strptime

Предположим, что есть следующая строка с датой: «11/17/20 15:02:34», и ее нужно конвертировать в объект datetime.

```python
from datetime import datetime

datetime_string = "11/17/20 15:02:34"
datetime_obj = datetime.strptime(datetime_string, '%m/%d/%y %H:%M:%S')
print(datetime_obj)
```
    2020-11-17 15:02:34

Даты могут быть записаны в разных форматах. Например, следующие даты отличаются лишь представлением:

    Friday, November 17, 2020;
    11/17/20;
    11–17–2020.

Вот как это работает:

```python
from datetime import datetime

# создадим даты как строки
ds1 = 'Friday, November 17, 2020'
ds2 = '11/17/20'
ds3 = '11-17-2020'

# Конвертируем строки в объекты datetime и сохраним
dt1 = datetime.strptime(ds1, '%A, %B %d, %Y')
dt2 = datetime.strptime(ds2, '%m/%d/%y')
dt3 = datetime.strptime(ds3, '%m-%d-%Y')

print(dt1)
print(dt2)
print(dt3)
```
Результат будет одинаковым для всех форматов:

    2020-11-17 00:00:00
    2020-11-17 00:00:00
    2020-11-17 00:00:00

## Практические примеры

Если строка представлена в формате «Oct 17 2020 9:00PM», то ее можно конвертировать следующим образом:

```python
date_string = 'Oct 17 2020 9:00PM'
date_object = datetime.strptime(date_string, '%b %d %Y %I:%M%p')
print(date_object)
```
Результат — `2020-10-17 21:00:00`.

Функцию strptime() можно использовать для конвертации строки в объект даты:

```python
from datetime import datetime

date_string = '10-17-2020'
date_object = datetime.strptime(date_string, '%m-%d-%Y').date()
print(type(date_object))
print(date_object)
```
    <type 'datetime.date'>
    2020-10-17

Как конвертировать объект datetime в строку

Модуль datetime в Python содержит метод strftime(), который делает обратное (то есть, конвертирует объект datetime и time в строки). Вот его синтаксис:

```python
datetime_string = datetime_object.strftime(format_string)
time_string = datetime_object.strftime(format_string[,time_object])
```

## Примеры конвертации datetime в строку с помощью strftime()

Предположим, нужно конвертировать текущий объект datetime в строку. Сначала нужно получить представление объекта datetime и вызвать на нем метод strftime().

```python
import datetime

current_date = datetime.datetime.now()
current_date_string = current_date.strftime('%m/%d/%y %H:%M:%S')
print(current_date_string)
```

Результат — `11/14/20 17:15:03`.

### Как получить строковое представление даты и времени с помощью функции format()

Пример №1. Конвертация текущей временной метки в объекте datetime в строку в формате «DD-MMM-YYYY (HH:MM:SS:MICROS)»:

```python
import datetime

dt_obj =datetime.datetime.now()
dt_string = dt_obj.strftime("%d-%b-%Y (%H:%M:%S.%f)")
print('Текущее время : ', dt_string)
```
    Текущее время :  14-Nov-2020 (17:18:09.890960)

Пример №2. Конвертация текущей временной метки объекта datetime в строку в формате «HH:MM:SS.MICROS – MMM DD YYYY».

```python
import datetime

dt_obj =datetime.datetime.now()
dt_string = dt_obj.strftime("%H:%M:%S.%f - %b %d %Y")
print('Текущее время : ', dt_string)
```
    Текущее время :  17:20:28.841390 - Nov 14 2020

## Другие datetime-библиотеки в Python

В Python есть и другие библиотеки, которые упрощают процесс манипуляций с объектами datetime. В некоторых из них есть поддержка часовых поясов.

### Arrow

Arrow — еще один популярный модуль, который делает более простым процесс создания, управления и форматирования дат и времени. Получить его можно с помощью pip. Для установки достаточно ввести pip install arrow.

Arrow можно использовать для получения текущего времени по аналогии с модулем datetime:

```python
import arrow

current_time = arrow.now()
print(current_time)
print(current_time.to('UTC'))
```
    2020-11-14T15:52:58.921198+00:00
    2020-11-14T15:52:58.921198+00:00

### Maya

Maya упрощает процесс парсинга строк и конвертации часовых поясов. Например:

```python
import maya

dt = maya.parse('2019-10-17T17:45:25Z').datetime()
print(dt.date())
print(dt)
print(dt.time())
```
    2019-10-17
    2019-10-17 17:45:25+00:00
    17:45:25

### Dateutil

Dateutil — это мощная библиотека, которая используется для парсинга дат и времени в разных форматах. Вот некоторые примеры.

```python
from dateutil import parser

dt_obj = parser.parse('Thu Oct 17 17:10:28 2019')
print(dt_obj)
dt_obj1=parser.parse('Thursday, 17. October 2019 5:10PM')
print(dt_obj1)
dt_obj2=parser.parse('10/17/2019 17:10:28')
print(dt_obj2)
t_obj=parser.parse('10/17/2019')
print(t_obj)
```
    2019-10-17 17:10:28
    2019-10-17 17:10:00
    2019-10-17 17:10:28
    2010-10-17 00:00:00

Важно, что в этом случае не нужны регулярные выражения при определении формата. Парсер ищет узнаваемые токены и либо возвращает корректный результат, либо выдает ошибку.
Важные нюансы

Вот о чем важно помнить при работе с datetime в Python:

- Рекомендуется всегда работать с UTC. Это позволяет не думать о часовых поясах, что часто приводит к ошибкам из-за разницы во времени в разных регионах.
- Дату и время стоит конвертировать в локальную только при выводе пользователю.

## Выводы

Есть масса сценариев работы с датой и временем в реальных приложениях. Например:

- Запланировать работу скрипта на определенное время.
- Отфильтровать даты.
- Извлечь дату из определенных API каждый день, в определенное время.
- Приложения для отслеживания событий, записей, бронирования и так далее.

Скриншоты с https://pythonru.com/primery/kak-ispolzovat-modul-datetime-v-python

![](article01_01.png)
![](article01_02.png)
![](article01_03.png)

