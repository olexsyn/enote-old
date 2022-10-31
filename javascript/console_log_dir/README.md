# console.dir(elem) и console.log(elem)

Большинство браузеров поддерживают в инструментах разработчика две команды: `console.log` и `console.dir`. Они выводят свои аргументы в консоль. Для JavaScript-объектов эти команды обычно выводят одно и то же.

Но для DOM-элементов они работают по-разному:

- `console.log(elem)` выводит элемент в виде DOM-дерева.
- `console.dir(elem)` выводит элемент в виде DOM-объекта, что удобно для анализа его свойств.

Попробуйте сами на `document.body`.

<https://learn.javascript.ru/basic-dom-node-properties>
