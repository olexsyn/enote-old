# JSON

JavaScript Object Notation — це вбудований пакет Python. Використання JSON може працювати з даними JSON JSON використовується для обміну та зберігання даних. Це текст. Просто імпортуйте пакет JSON, тоді ми зможемо використовувати JSON 

    імпорт json

Об’єкти JSON включають аналіз, серіалізацію, десеріалізацію та багато іншого. Це пакет JSON, який надає необхідні інструменти.

- <https://docs.python.org/3/library/json.html>
- <https://pyneng.readthedocs.io/ru/latest/book/17_serialization/json.html>

Кодування рідного типу даних у формат JSON називається процесом серіалізації. Наприклад, розглянемо словник python, який використовує python JSON, який може перетворюватися на об’єкт JSON. Подібним чином, int і float, перетворені як числа, списки та кортежі JSON, можна перетворити на масив JSON; JSON null результати з None converted.

Як серіалізувати дані Python у формат JSON? Давайте розглянемо ці методи:

- json.dump()
- json.dumps() 

Ми можемо використовувати dumps() за допомогою функції json.dumps(), яка перетворює об’єкт Python у рядок json.

Синтаксис:

    json.dumps(obj)  # де obj – це словник
    json.dumps({'id': order_id.id})

    json.dump(dict, 'filename.json')  # використовується для запису у файл json

## Методи десеріалізації

Десеріалізація є прямою протилежністю серіалізації. Якщо ви вже закодували об’єкт, скористайтеся методом десеріалізації, щоб знову декодувати цей об’єкт.

- json.loads()
- json.load()


Синтаксис

    json.loads(s), аргументи `s` можуть бути рядком, масивом, байтом

```pyton
task= {
'parent_id': task_obj.id,
'name': rec.product_id.name
}
json.loads(task)
```

Зауважте, що нам потрібно повернути об’єкт JSON, щоб у той час ми могли використовувати json.load() 

```pyton
res = json.load(urlopen(f'https://api.github.com))
```

### Кодування комплексних чисел

<https://www.cybrosys.com/blog/analysis-of-python-java-script-object-notation>

