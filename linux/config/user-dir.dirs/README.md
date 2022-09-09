# config/user-dir.dirs

В цьому файлі можна вручну змінити каталоги користувача на більш прості для спрощення друку в терміналі. Наприклад, так:

```
# This file is written by xdg-user-dirs-update
# If you want to change or add directories, just edit the line you're
# interested in. All local changes will be retained on the next run.
# Format is XDG_xxx_DIR="$HOME/yyy", where yyy is a shell-escaped
# homedir-relative path, or XDG_xxx_DIR="/yyy", where /yyy is an
# absolute path. No other format is supported.
# 
XDG_DESKTOP_DIR="$HOME/desktop"
XDG_DOWNLOAD_DIR="$HOME/down"
XDG_TEMPLATES_DIR="$HOME/temp"
XDG_PUBLICSHARE_DIR="$HOME/dev"
XDG_DOCUMENTS_DIR="$HOME/docs"
XDG_MUSIC_DIR="$HOME/music"
XDG_PICTURES_DIR="$HOME/img"
XDG_VIDEOS_DIR="$HOME/video"
```

(Не використовую каталог `Public` за призначенням, це в мене - каталог для розробки `dev`) 

Вказані каталоги необхідно створити, потім:

    sudo xdg-user-dirs-update

Ярлики з `Desktop` скопіювати або перенести в `desktop`.
