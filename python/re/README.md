# re

<https://docs.python.org/3/library/re.html>

## search

```python
import re

print('re: search')
print('-' * 30, '\n')

time_str = '1:02:34.05'

res = re.search('^(.+)[\.,](.+)$', time_str)

if res:
    print('res =',res)     
    print('res.groups() =',res.groups())     
    print('res.group(0) =',res.group(0))     
    print('res.group(1) =',res.group(1))     
    print('res.group(2) =',res.group(2))     
else:
    print('not found')
```

## findall

```python
import re

print('re: compile, findall')
print('-' * 30, '\n')

one_str = '+380 (12) 345-6789'

any_str = ('+380 (12) 345-6789'
           '+381 (98) 765-4321')

pat = re.compile('\+(\d+)\s\((\d\d)\)\s(\d{3}\-\d{4})')

res = re.findall(pat, one_str)  # ?returns list of tuples?
if res:
    print('res     =',res)     
    print('found   =',res[0])     
    print('country =',res[0][0])     
    print('city    =',res[0][1])     
    print('number  =',res[0][2])     

print('-' * 30)
#  если одни () - список
# если ()() список кортежей
res = re.findall(pat, any_str)  # ?returns list of tuples?

if res:
    print('res     =',res)     

    cnt = 0
    for item in res:
        cnt += 1
        print('#', cnt, '-----')
        print('found   =',item)     
        print('country =',item[0])     
        print('city    =',item[1])     
        print('number  =',item[2])     
        
'''
    #print('res[1] =',res[1])     
    #print('res[2] =',res[2])     
    #print('res.group(0) =',res.group(0))     
    #print('res.group(1) =',res.group(1))     
    #print('res.group(2) =',res.group(2))     
else:
    print('not found')
'''
```

## Пример валидации e-mail

```python
#!/usr/bin/python3
from re import *

def get_address():
    '''
    проверка email по шаблону    
    '''
    pattern = compile('(^|\s)[-a-z0-9_.]+@([-a-z0-9]+\.)+[a-z]{2,6}(\s|$)')
    address = input('inter you email address:')
    is_valid = pattern.match(address)
    if is_valid:
        print('правильный email:', is_valid.group())
        # объект is_valid содержит 3 метода
        print('методы: start:', is_valid.start(), 'end:',\
        is_valid.end(), 'group:', is_valid.group())
    else:
        print('неверный email! введите email...\n')


get_address()
```
