# String to Integer, Integer to String

## parseInt()

Функція `parseInt()` аналізує рядковий аргумент і повертає ціле число вказаної системи числення (основа в математичних системах числення).

### Приклади

```javascript
// Усі наступні приклади повертають `15`:

parseInt("0xF", 16);
parseInt("F", 16);
parseInt("17", 8);
parseInt("015", 10);     // але `parseInt('015', 8)` will return 13
parseInt("15,123", 10);
parseInt("FXX123", 16);
parseInt("1111", 2);
parseInt("15 * 3", 10);
parseInt("15e2", 10);
parseInt("15px", 10);
parseInt("12", 13);

// Усі наступні приклади повертають `NaN`:

parseInt("Hello", 8);   // зовсім не номер
parseInt("546", 2);     // цифри, відмінні від 0 або 1, є неприпустимими для двійкової основи

// Усі наступні приклади повертають `-15`:

parseInt("-F", 16);
parseInt("-0F", 16);
parseInt("-0XF", 16);
parseInt("-17", 8);
parseInt("-15", 10);
parseInt("-1111", 2);
parseInt("-15e1", 10);
parseInt("-12", 13);
Копіювати в буфер обміну
```

<https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt>

## toString()

(**Number.prototype.toString()**)

Метод `toString()` повертає рядок, що представляє вказане числове значення.

### Приклади

```javascript
const count = 10;
count.toString();     // "10"

(17).toString();      // "17"
(17.2).toString();    // "17.2"

const x = 6;
x.toString(2);        // "110"
(254).toString(16);   // "fe"
(-10).toString(2);    // "-1010"
(-0xff).toString(2);  // "-11111111"
```

<https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toString>
