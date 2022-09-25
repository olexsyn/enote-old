# Читання xlrd та запис xlwt Excel-файлів старого типу `.xls`

<https://xlrd.readthedocs.io/>  
<https://xlwt.readthedocs.io/>  
див. також <https://github.com/python-excel>

    pip install xlrd
    pip install xlwt

## xlrd

<https://github.com/python-excel/tutorial/raw/master/python-excel.pdf>

- Reading Excel Files - Page 7

```python
from xlrd import cellname, cellnameabs, colname

print(cellname(0,0),cellname(10,10),cellname(100,100))
print(cellnameabs(3,1),cellnameabs(41,59),cellnameabs(265,358))
print(colname(0),colname(10),colname(100))
```
```
A1 K11 CW101
$B$4 $BH$42 $MU$266
A K CW
```


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

    col = ord(col) - 65  # 65 - це код латинської літери 'A', в модулі xlrd стовпчик 'A' == 0
    row = int(row) - 1   # в модулі xlrd рядки починаються з нуля 0

    val = shit.cell_value(rowx=row, colx=col)

    return val

book = xlrd.open_workbook("1234.xls")
sh = book.sheet_by_index(0)

print(cval(sh,'A15'))
print(cval(sh,'C20'))
```

## xlwt


https://github.com/python-excel/xlwt/tree/master/examples

### Types of Cell

All types of cell supported by the Excel file format can be written:

#### Text

When passed a unicode or string, the write methods will write a Text cell.
The set_cell_text method of the Row class can also be used to write Text cells.
When passed a string, these methods will first decode the string using the Workbook's
encoding.

#### Number

When passed a float, int, long, or decimal.Decimal, the write methods will write a
Number cell.
The set_cell_number method of the Row class can also be used to write Number cells.

#### Date

When passed a datetime.datetime, datetime.date or datetime.time, the write
methods will write a Date cell.
The set_cell_date method of the Row class can also be used to write Date cells.
Note: As mentioned earlier, a date is not really a separate type in Excel; if you don't apply a
date format, it will be treated as a number.

#### Boolean

When passed a bool, the write methods will write a Boolean cell.
The set_cell_boolean method of the Row class can also be used to write Text cells

The following example brings all of the above cell types together and shows examples use
both the generic write method and the specialist methods:

```python
from datetime import date,time,datetime
from decimal import Decimal
from xlwt import Workbook,Style
wb = Workbook()
ws = wb.add_sheet('Type examples')
ws.row(0).write(0,u'\xa3')
ws.row(0).write(1,'Text')
ws.row(1).write(0,3.1415)
ws.row(1).write(1,15)
ws.row(1).write(2,265L)
ws.row(1).write(3,Decimal('3.65'))
ws.row(2).set_cell_number(0,3.1415)
ws.row(2).set_cell_number(1,15)
ws.row(2).set_cell_number(2,265L)
ws.row(2).set_cell_number(3,Decimal('3.65'))
ws.row(3).write(0,date(2009,3,18))
ws.row(3).write(1,datetime(2009,3,18,17,0,1))
ws.row(3).write(2,time(17,1))
ws.row(4).set_cell_date(0,date(2009,3,18))
ws.row(4).set_cell_date(1,datetime(2009,3,18,17,0,1))
ws.row(4).set_cell_date(2,time(17,1))
ws.row(5).write(0,False)
ws.row(5).write(1,True)
ws.row(6).set_cell_boolean(0,False)
ws.row(6).set_cell_boolean(1,True)
ws.row(7).set_cell_error(0,0x17)
ws.row(7).set_cell_error(1,'#NULL!')
ws.row(8).write(0,'',Style.easyxf('pattern: pattern solid, fore_colour green;'))
ws.row(8).write(1,None,Style.easyxf('pattern: pattern solid, fore_colourblue;'))
ws.row(9).set_cell_blank(0,Style.easyxf('pattern: pattern solid, fore_colour yellow;'))
ws.row(10).set_cell_mulblanks(5,10,Style.easyxf('pattern: pattern solid, fore_colour red;'))
wb.save('types.xls')
```
