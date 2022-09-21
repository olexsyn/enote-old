# xlrd читання Excel-файлів старого типу `.xls`

<https://xlrd.readthedocs.io/>

див. також <https://github.com/python-excel>

    pip install xlrd

```python
import xlrd

book = xlrd.open_workbook("myfile.xls")
print("The number of worksheets is {0}".format(book.nsheets))
print("Worksheet name(s): {0}".format(book.sheet_names()))
sh = book.sheet_by_index(0)

print("{0} {1} {2}".format(sh.name, sh.nrows, sh.ncols))
print("Cell D30 is {0}".format(sh.cell_value(rowx=29, colx=3)))

for rx in range(sh.nrows):
    print(sh.row(rx))
```

## Зручна адресація до комірок - функція cval()

Вказувати адресу комірок як 'A15', 'C20' - значно зручніше

```python
import xlrd
import re

def cval(shit, addr):
    """
    cval <- CellValue
    Отримує значення комірки, адреса якої задається як 'літера'+'число':
    shit - лист Excel
    addr - адреса

    val = cval(sh, 'C20')
    """
    res = re.search('^([A-Z])(\d{1,2})$', addr)

    if res:
        col = res.group(1)  # letter
        row = res.group(2)  # digit
    else:
        return None

    col = ord(col) - 65
    row = int(row) - 1

    val = shit.cell_value(rowx=row, colx=col)
    # return dict( rowx=row, colx=col )
    return val

book = xlrd.open_workbook("1234.xls")
sh = book.sheet_by_index(0)

print(cval(sh,'A15'))
print(cval(sh,'C20'))
```
