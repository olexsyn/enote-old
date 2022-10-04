# Обработка форм

```html
<form action="/cgi-bin/reg.py" method="post">

    Ім'я:
    <input type="text" name="t_fname" value="">

    Корпус:
    <select name="s_house">
        <option selected disabled value="">корпус #...</option>
        <option>1</option>
        <option>2</option>
        <option>3</option>
    </select>
    
    <input type="radio" name="r_messeng" value="email"> E-mail
    <input type="radio" name="r_messeng" value="teleg"> Telegram
    <input type="radio" name="r_messeng" value="viber"> Viber
  
    <input type="checkbox" name="c_office"> Офіс

    <input type="checkbox" name="c_consent" value="i_agree" required> Я згоден

    <button type="submit">Відправити</button>

</form>
```

```python
import cgi
form = cgi.FieldStorage()

fname   =        form.getfirst('t_fname','')
house   =        form.getfirst('s_house','')
messeng =        form.getfirst('r_messeng','')  # в зависимости от выбора messeng примет одно из значений: email / teleg / viber
office  = 'Y' if form.getfirst('c_office','')               else 'N'  # поле без value
consent = 'Y' if form.getfirst('c_consent','') == 'i_agree' else 'N'  # поле имеет value='i_agree'
```
