# datetime

- <https://docs.python.org/3/library/datetime.html>
- <https://www.w3schools.com/python/python_datetime.asp>
- [Как использовать модуль datetime](article01.md)


```python
import datetime

x = datetime.datetime(2020, 5, 17)

print(x)  # 2020-05-17 00:00:00
```


```python
import datetime

x = datetime.datetime(2020, 5, 17)

print(f"{x=}")  # x=datetime.datetime(2020, 5, 17, 0, 0)
```


```python
import datetime

x = str(datetime.datetime(2020, 5, 17))

print(f"{x=}")  # x='2020-05-17 00:00:00'
```

```python
import datetime

x = datetime.datetime.now()

print(x.strftime("%x"))  # 10/05/22
```

```python
import datetime

x = datetime.datetime.now()

print(x.strftime("%d.%m.%Y"))  # 05.10.2022
```

## isoformat(), fromisoformat()

```python
from datetime import date

dt = date.fromisoformat('2019-12-04')

print(dt)        # 2019-12-04
print(f"{dt=}")  # dt=datetime.date(2019, 12, 4)
```


```python
from datetime import datetime, date

today = date.today()      # date!
print(today)              # 2022-10-05
print(today.isoformat())  # 2022-10-05

dt = datetime.now()       # datetime!
print(dt.isoformat())     # 2022-10-05T15:12:31.038965

dt = date.fromisoformat('2022-10-05 15:12:31')             # ValueError: Invalid isoformat string
dt = datetime.fromisoformat('2022-10-05 15:12:31.03')      # 2022-10-05 15:12:31.03
dt = datetime.fromisoformat('2022-10-05T15:12:31.03')      # 2022-10-05 15:12:31.03
dt = datetime.fromisoformat('2022-10-05T15:12:31.038965')  # 2022-10-05 15:12:31.038965

print(f"{dt=}")           # dt=datetime.datetime(2022, 10, 5, 15, 12, 31, 38965)
```

## strftime()

див. тут: https://www.w3schools.com/python/python_datetime.asp

```python
from datetime import date

dt = date.fromisoformat('2019-12-04')

print(dt.strftime("%B"))           # December
print(dt.strftime("%Y-%m-%d"))     # 2019-12-04

dt_str = dt.strftime("%d.%m.%Y")
print(f"{dt_str=}")                # dt_str='04.12.2019'
```
