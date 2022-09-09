# HTML-Form + AJAX

{% raw %}
`/_tpl/adm/ap.htm`

```html
<!DOCTYPE html>
<html lang="uk">

<head>
	{% include 'adm/_head.htm' %}
</head>

<body>
	{% include 'adm/ap_form.htm' %}
</body>

</html>
```

`/_tpl/adm/ap_form.htm`

```html
	<div class="container my-4">
		<h3><!--#echo encoding="none" var="PAGE_TITLE"--> <small> <!--#echo encoding="none" var="SMALL_TITLE"--></small></h3>
		<p class="head mt-3">ADDR_ID: [<b>{{ ADDR_ID }}</b>]<br/>____________________</p>
		<p class="my-3" >Обов'язкові поля позначені зірочкою <span class="text-danger">*</span></p>

		<form id="addressForm" class="needs-validation" novalidate>
			<!-- action="/cgi-bin/adm_ap.py" method="post" -->
			<div class="form-row">

				<div class="col-md-3 mb-3">
					<label for="sAddrHouse">Корпус <span class="text-danger">*</span></label>
					<select class="custom-select" id="sAddrHouse" name="s_addr_house" required>
						<option selected disabled value="">корпус #...</option>
{%- for i in range(1,10) %}
	{%- if i==SEL_HOUSE -%}
	<option selected>{{ i }}</option>
	{%- else -%}
	<option>{{ i }}</option>
	{%- endif -%}
{% endfor -%}
					</select>
					<div class="invalid-feedback">
						Вкажіть номер корпусу.
					</div>
				</div>

				<div class="col-md-5 mb-3">
					<label for="tAddrFlat">Квартира <span class="text-danger">*</span></label>
					<input type="text" class="form-control" id="tAddrFlat" name="t_addr_flat" placeholder="123" minlength="1" maxlength="3" pattern="\d{1,3}" value="{{ FLAT }}" required>
					<div class="invalid-feedback">
						Від 1 до 3 цифр.
					</div>
				</div>

				<div class="col-md-4 form-group">
					<label for="cOffice">Якщо це офіс</label>
					<div class="form-check">
						<input class="form-check-input" type="checkbox" id="cOffice" name="c_office" {{ 'checked' if OFFICE == 'Y'}}>
						<label class="form-check-label" for="cOffice">
							Офіс
						</label>
					</div>
				</div>
			</div>


			<div class="my-4 text-center">

				<input type="submit" value="Показати" class="btn btn-primary mt-5" id="bShow" />
			</div>
		</form>

	</div>
	<div class="container my-4" id="out">{{ TABLE_OF_RESIDENTS }}</div>
```
```javascript
	<script src="/js/jquery.min.js"></script>
	<script src="/js/spin.min.js"></script>
	<script>
		var spinner = new Spinner({left:'15%'}).spin();

		function lz(strn, size)  // leading zeros
		{
			var strn = strn + '';

			while (strn.length < size)
				strn = '0' + strn;

			return strn;
		}


		// $("#addUser").submit(function(e)
		// {
		// 	e.preventDefault();
		// 	$('#out').html('add user');
		// });

		$("#addressForm").submit(function(e)
		{
			e.preventDefault();

			$('#out').html('');

			var inpHouse = $("#sAddrHouse").val();
			var inpFlat = $("#tAddrFlat").val();
			var err = 0;

			var house_patt = /^\d$/;
			if (inpHouse + 0 == 0 || !house_patt.test(inpHouse)) {
				$('#sAddrHouse').removeClass('is-valid').addClass('is-invalid');
				$("#sAddrHouse.invalid-feedback").show();
				err = 1;
			} else {
				$('#sAddrHouse').removeClass('is-invalid').addClass('is-valid');
				$("#sAddrHouse.invalid-feedback").hide();
			}

			var flat_patt = /^\d{1,3}$/;
			if (inpFlat + 0 == 0 || !flat_patt.test(inpFlat)) {
				$('#tAddrFlat').removeClass('is-valid').addClass('is-invalid');
				$("#tAddrFlat.invalid-feedback").show();
				err = 1;
			} else {
				$('#tAddrFlat').removeClass('is-invalid').addClass('is-valid');
				$("#tAddrFlat.invalid-feedback").hide();
			}

			if (err == 1) return false;

			var inp = inpHouse + lz(inpFlat,3);
			var inp_patt = /^\d{4}$/;
			if (inp_patt.test(inp))
			{
				$(".invalid-feedback").hide();
				$('#sAddrHouse').removeClass('is-invalid');
				$('#tAddrFlat').removeClass('is-invalid');
				$('#out').append(spinner.el);

				$.get('/cgi-bin/adm_ows_show.py', { aid:inp })
				.done(function(result){
					$('#out').html(result);
				})
				.fail(function(){
					$('#out').html('Вибачте, виникла помилка!');
				});
			}
		});
	</script>
```

`_tpl/adm/ows_show_table.htm`

```html
	<table class="table table-striped">
		<thead>
			<tr>
				<th scope="col">owid</th>
				<th scope="col">name</th>
				<th scope="col">home<br/>flat<br/>door</th>
				<th scope="col">cars</th>
				<th scope="col">tel1<br/>tel2<br/>tel3</th>
				<th scope="col">email</th>
				<th scope="col">st</th>
				<!-- <th scope="col">cons</th> -->
				<th scope="col">edit</th>
			</tr>
		</thead>
		<tbody>
			{{ TABLE_BODY }}
		</tbody>
	</table>
```

`_tpl/adm/ows_show_table_row.htm`

```html
<tr>
	<td>{{ OWID }}</td>
	<td>{{ LNAME }}<br/>
	  {{ FNAME }}<br/>
	  {{ SNAME }}</td>
	<td>{{ HOUSE }}<br/>{{ FLAT }}<br/>{{ DOOR }}</td>
{% if CAR and not NOCAR %}
	<td  class="alert-success text-center">{{ CAR }}</td>
{% elif CAR and NOCAR %}
	<td  class="alert-danger text-center">~~ NO CAR ~~<br>{{ CAR }}</td>
{% elif not CAR and NOCAR %}
	<td  class="alert-danger text-center">NO CAR</td>
{% else %}
	<td  class="text-center">NO</td>
{% endif %}
	<td>{{ TEL1 }}<br/>{{ TEL2 }}<br/>{{ TEL3 }}</td>
	<td>{{ EMAIL }}<br/><small>not confirmed!</small></td>
	<td>{{ STATE }}</td>
	<!-- <td class="{% if CONSENT=='N' %}alert-danger{% endif %} text-center">{{ CONSENT }}</td> -->
	<td>
		<form action="/adm/ow/{{ OWID }}/" method="POST">
			<button type="submit" class="btn btn-outline-success btn-sm w-100">Edit Owner</button>
		</form>
		<form action="/adm/ow/add/{{ OWID }}/" method="POST" class="mt-2">
			<button type="submit" class="btn btn-outline-info btn-sm w-100">Add Owner</button>
		</form>
	</td>
</tr>
```

```python
#!/usr/local/bin/python3.7

import cgi
import re

from lib import aInit
from lib import aCom
from lib import aJ2 as j2
from lib.aDB import get_owners_by_flat, get_owner_cars_brands


SCRIPT_NAME = 'adm_ow_show.py'


form = cgi.FieldStorage()
aid  = form.getfirst('aid','none')

s = re.search('^\d\d\d\d$', aid)

if not s:
	j2.alert('danger', 'ERR_INCORRECT_ADDRESS_ID', f"id: {aid}")

else:
	house, flat = aCom.addr_split(aid)

	if house == 0 or flat == 0:
		j2.alert('danger', 'ERR_INCORRECT_ADDRESS_ID', f"к.{house} / кв.{flat}")

	else:
		ows_list = get_owners_by_flat(house, flat)

		if not len(ows_list):
			j2.alert('warning', 'NOBODY_LIVES_HERE', f"к.{house} / кв.{flat} &nbsp; | &nbsp; <a href='/adm/ow/add/{aid}/'>Зареєструвати</a>")

		else:
			table_rows_rendered = ''

			for item in ows_list:    # item = Row(cid=129, num='AA0000KT', brand='VAZ', model='2109', color='BLU')
				tpl_vars = dict(
					OWID   = item.owid,
					LNAME  = item.lname,
					FNAME  = item.fname,
					SNAME  = item.sname,
					HOUSE  = item.house,
					DOOR   = item.door,
					FLAT   = item.flat,
					EMAIL  = item.email,
					NOCAR  = 1 if item.nocar == 'NO CAR' else 0,
					CAR    = '<br>'.join(get_owner_cars_brands(item.owid)),
					STATE  = item.owstate,
					TEL1   = aCom.tel_template(item.tel1),
					TEL2   = aCom.tel_template(item.tel2),
					TEL3   = aCom.tel_template(item.tel3),
					APID   = aCom.addr_join(item.house, item.flat),
				)
				table_rows_rendered += j2.render('adm/ows_show_table_row.htm', tpl_vars)
			# for

			tpl_vars = dict(
				TABLE_BODY = table_rows_rendered,
			)
			print(j2.render('adm/ows_show_table.htm', tpl_vars))
```
{% endraw %}
