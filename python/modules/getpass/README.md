# getpass

```python
import getpass

while 1:
	passw1 = getpass.getpass()
	passw2 = getpass.getpass('Please, enter your password again: ')

	if passw1 == passw2:
		print(f'Password "{passw1}" saved. Thank you!')
		break
	else:
		print(f'Sorry, your passwords are incorrect: "{passw1}" vs "{passw2}".')
		yn = input('Try again? (y/n): ')
		if yn == 'y':
			print()
			continue
		else:
			break

print('Good bye!')
```
