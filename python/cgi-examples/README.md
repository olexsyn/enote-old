# Примеры CGI

## Сгенерировать простую HTML-страничку

```python
#!/usr/bin/python3

# ---------------------------
def html_head(lang='en',title='test'):
	print("Content-Type: text/html\n")  # print переводит строку, поэтому - один \n
	print(f'''<!DOCTYPE html>
<html lang="{lang}">
<head><title>{title}</title></head>
<body>''')

# ---------------------------
def html_foot():
	print('</body></html>')

# ===========================

html_head()
print('<h1>Hello World!<h1>')
html_foot()
```
