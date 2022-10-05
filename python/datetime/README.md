# datetime

- <https://docs.python.org/3/library/datetime.html>
- <https://www.w3schools.com/python/python_datetime.asp>

```python
import datetime

x = datetime.datetime(2020, 5, 17)

print(x)
```
    2020-05-17 00:00:00
----


```python
import datetime

x = datetime.datetime(2020, 5, 17)

print(f"{x=}")
```
    x=datetime.datetime(2020, 5, 17, 0, 0)
----


```python
import datetime

x = str(datetime.datetime(2020, 5, 17))

print(f"{x=}")
```
    x='2020-05-17 00:00:00'
----


```python
import datetime

x = datetime.datetime.now()

print(x.strftime("%x"))
```
    10/05/22
----


```python
import datetime

x = datetime.datetime.now()

print(x.strftime("%d.%m.%Y"))
```
    05.10.2022
----


```python
from datetime import date

dt = date.fromisoformat('2019-12-04')

print(dt)
print(f"{dt=}")
```
    2019-12-04
    dt=datetime.date(2019, 12, 4)
----


```python
from datetime import date

dt = date.fromisoformat('2019-12-04')

print(dt.strftime("%B"))
print(dt.strftime("%Y-%m-%d"))

dt_str = dt.strftime("%d.%m.%Y")
print(f"{dt_str=}")
```
    December
    2019-12-04
    dt_str='04.12.2019'
----

