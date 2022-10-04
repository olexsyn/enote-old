# collections

**namedtuple** - не итерируемый. Т.е. его нельзя перебрать в цикле, используя ключи и/или значения. У namedtuple нет таких методов как items(), keys(), values(). Но есть метод _asdict(), который позволяет перебрать его, как словарь...

{% include a.htm url="https://docs.python.org/3/library/collections.html#collections.namedtuple" %}

```python
from collections import namedtuple

Restaurant = namedtuple('Restaurant', 'name cuisine phone dish price')
RC = [
	Restaurant("Thai Dishes", "Thai",     "334-4433", "Mee Krob",    12.50),
	Restaurant("Nobu",        "Japanese", "335-4433", "Natto Temaki", 5.50)
]

one, two = RC[0], RC[1]

print(f'name = {one.name}')
print(f'cuisine = {one.cuisine}')
print(f'phone = {one.phone}')
print(f'dish = {one.dish}')
print(f'price = {one.price}')

print()

print(f'name = {two.name}')
print(f'cuisine = {two.cuisine}')
print(f'phtwo = {two.phone}')
print(f'dish = {two.dish}')
print(f'price = {two.price}')

print('\n','-'*50,'\n')

# используем '_asdict()':

for item in RC:
	for key, val in item._asdict().items():
		print(f'{key} = {val}')
	print()
```
