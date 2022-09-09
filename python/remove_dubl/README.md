# Удаление дубликатов в списке

Среди регулярно используемых трюков в Python – преобразование списка во множество и обратно в список для удаления повторяющихся элементов списка:

```python
items = [2, 2, 3, 3, 1]
print(list(set(items)))
```
{% include cl.htm cmd="[1, 2, 3]" %}

Но множества – это неупорядоченные последовательности. Часто стоит задача сохранить порядок следования элементов. Для этого удобно воспользоваться типом данных OrderedDict из модуля collections:

```python
items = [2, 2, 3, 3, 1]
from collections import OrderedDict
print(list(OrderedDict.fromkeys(items).keys()))
```
{% include cl.htm cmd="[2, 3, 1]" %}


{% include a.htm url="https://proglib.io/p/python-tricks/" text="Источник" %}
