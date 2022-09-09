# Geany

## Установка на Linux Lite 4

Версія з Settings / Lite Software - на 3 роки застаріла, тому скачувати з сайту `tar.gz` https://www.geany.org/download/releases/ .

Інструкція по встановленню: https://www.geany.org/manual/current/index.html#installation

Стисло:

- розпаковуємо (напр. в soft)
- `./configure` - зразу не пройшов, прийшлося встановити:
  - GTK: `sudo apt install libgtk-3-dev`
  - intltool: `sudo apt search intltool`
- `./configure` знову (пройшов)
- `make`
- `sudo make install`
