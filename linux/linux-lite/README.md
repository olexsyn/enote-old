
## nVidia

Здається, проблеми з драйвером nouveau стосуються лише мого ноутбука з картою nVidia.

На відміну від Manjaro екран не блимав час від часу, але сотні строчок під час запуску та вимкнення ноута

```
... nouveau Error ...
... nouveau Error ...
... nouveau Error ...
```

не тільки не давали спокою, але і суттєво марнували мій час!

Але, на відміну від Manjaro, драйвер nVidia став на ноут з LinuxLite коректно.

### Встановлення драйвера NVidia

Інфу знайшов в локальній документації **file:///usr/share/doc/litemanual/hardware.html#nvidia** де радили ставити `proprietary, tested` - такий і вибрав.


`Menu` -> `Settings` -> `Install Drivers`

![](linuxlite_nvidia.png)


Перезавантажився, помилки пропали, все ок.
