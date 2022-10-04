# Загрузка файлов пользователя на сервер

См. <https://developer.mozilla.org/ru/docs/Web/HTML/Element/Input/file> - есть пример выбора нескольких графических файлов с определением размера и демонстрацией их эскизов. Здесь более родробно + "drag and drop": <https://developer.mozilla.org/ru/docs/Web/API/File/Using_files_from_web_applications>

## Простейшая форма выбора файла и кнопки "Upload"

**HTML** _some.htm_

```html
<html>
<body>
	<form enctype="multipart/form-data" action = "upl.py" method = "post">
	<p>File: <input type="file" name="uplfile" /></p>
	<p><input type="submit" value="Upload" /></p>
	</form>
</body>
</html>
```

**CGI**  _upl.py_

```python
#!/usr/bin/python

import cgi, os.path

UPLOAD_DIR = '/var/www/site/upload'

form = cgi.FieldStorage()

if "uplfile" in form:
	upl_file = form['uplfile']  # upl_file is now an object
	if upl_file.filename:

		uploaded_file_path = os.path.join(UPLOAD_DIR, os.path.basename(upl_file.filename))
		with open(uploaded_file_path, 'wb') as fout:
			while True:
				chunk = upl_file.file.read(100000)
				if not chunk:
					break
				fout.write(chunk)

		# # load the written file to display it
		# with open(uploaded_file_path, 'r') as fin:
		# 	inFileData = ""
		# 	for line in fin:
		# 		inFileData += line

	message = 'The file ' + upl_file.filename + ' was uploaded successfully'
else:
	message = 'No file was uploaded'

print('Content-Type: text/html\n')
print(f'{message}')
```

### Стилизовать форму/кнопку выбора файлов 

```html
<html>
<body>
	<form enctype="multipart/form-data" action = "test_upl.py" method = "post">
	<input type="file" id="uplfile" name="uplfile" style="display:none">
	<p><label for="uplfile">Click me to select file</label></p>
	</form>
</body>
</html>
```


## Форма без кнопки Upload - файл загружается сразу после его выбора

**HTML** _some.htm_

```html
<html>
<head>
	<script src="/js/jquery.js"></script>
</head>
<body>
	<form id="form1" enctype="multipart/form-data" action="upl.py" method="post" target="hidden_frame" >
	<p>File: <input type="file" id="uplfile" name="uplfile" /></p>
	<span id="msg"></span><br/>
	<iframe name='hidden_frame' id="hidden_frame" style='display:none'></iframe>
	</form>
<script>
	$(document).ready(function () {
	$("#uplfile").change(function() {
		$("#form1").submit();
	});
});

function callback(msg) {
	$("#msg").html(msg);
}
</script>
</body>
</html>
```

**CGI**  _upl.py_

```python
#!/usr/bin/python

import cgi, os.path

UPLOAD_DIR = '/var/www/site/upload'

form = cgi.FieldStorage()

if "uplfile" in form:
	upl_file = form['uplfile']  # upl_file is now an object
	if upl_file.filename:
		filename = upl_file.filename
		uploaded_file_path = os.path.join(UPLOAD_DIR, os.path.basename(filename))
		with open(uploaded_file_path, 'wb') as fout:
			while True:
				chunk = upl_file.file.read(100000)
				if not chunk:
					break
				fout.write(chunk)

		# # load the written file to display it
		# with open(uploaded_file_path, 'r') as fin:
		# 	inFileData = ""
		# 	for line in fin:
		# 		inFileData += line

	message = f"<script>parent.callback('The file {filename} upload file success')</script>"
else:
	message = f"<script>parent.callback('No file was uploaded')</script>"

print('Content-Type: text/html\n')
print(f'{message}')
```
