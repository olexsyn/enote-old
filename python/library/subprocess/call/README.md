# call

Вы можете легко отображать системные всплывающие уведомления из программ на Python или любом другом языке.

Вам понадобится обвязка **libnotify** для Python:

    pacman -S python-notify

<small>(pacman - установщик для Archlinux, Manjaro)</small>

Вот простой "hello world" пример:

```python
import subprocess

def notify(title, mess):
    subprocess.call(['notify-send', title, mess])

path = "/home/user/tmp"
notify('Copied to', path)
```
