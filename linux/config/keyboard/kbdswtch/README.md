# My kbdswtch

Да, автоматическое переключение раскладок - немного зло... Привыкаешь, а потом на другой машине не можешь нормально работать.

Но, иногда бывает, не сразу замечаешь, что печатаешь не на нужной раскладке. Напрягает, что надо поменять раскладку и все перепечатать...

Простое решение: выделить неправильно набранный текст и нажать кнопочку, например, Pause и текст "перевернется" в альтернативную раскладку.

```bash
#!/bin/bash

# сохраняем выделение в файл
xclip -o -selection primary > /tmp/~sel.tmp

# сохраняем буфер обмена в файл
xclip -o -selection clipboard > /tmp/~clip.tmp

# чтобы не напечатать содержимое буфера обмена, если ничего не выделено, мы его очистим
xclip -i -selection clipboard

# очищаем выделение
xdotool key Delete

# записываем обработанный выделенный текст в буфер обмена
# - ru:
# cat /tmp/~sel.tmp | sed "y/\`~\!@#$%^&qwertyuiop[]asdfghjkl;'zxcvbnm,.\/QWERTYUIOP{}ASDFGHJKL:\"|ZXCVBNM<>?ёЁ\!\"№;%:?йцукенгшщзхъфывапролджэячсмитьбю.ЙЦУКЕНГШЩЗХЪФЫВАПРОЛДЖЭ\/ЯЧСМИТЬБЮ,/ёЁ\!\"№;%:?йцукенгшщзхъфывапролджэячсмитьбю.ЙЦУКЕНГШЩЗХЪФЫВАПРОЛДЖЭ\/ЯЧСМИТЬБЮ,\`~\!@#$%^&qwertyuiop[]asdfghjkl;'zxcvbnm,.\/QWERTYUIOP{}ASDFGHJKL:\"|ZXCVBNM<>?/" | xclip -selection clipboard
# - ua: (тут - стандартно)
# cat /tmp/~sel.tmp | sed "y/\`~\!@#$%^&qwertyuiop[]asdfghjkl;'zxcvbnm,.\/QWERTYUIOP{}ASDFGHJKL:\"|ZXCVBNM<>?ёЁ\!\"№;%:?йцукенгшщзхїфівапролджєячсмитьбю.ЙЦУКЕНГШЩЗХЇФІВАПРОЛДЖЄ\/ЯЧСМИТЬБЮ,/ёЁ\!\"№;%:?йцукенгшщзхїфівапролджєячсмитьбю.ЙЦУКЕНГШЩЗХЇФІВАПРОЛДЖЄ\/ЯЧСМИТЬБЮ,\`~\!@#$%^&qwertyuiop[]asdfghjkl;'zxcvbnm,.\/QWERTYUIOP{}ASDFGHJKL:\"|ZXCVBNM<>?/" | xclip -selection clipboard
# - ua: (a тут - ще англійський ` міняю на ’ - наклонний апостроф, який не одинарна кавичка!)
cat /tmp/~sel.tmp | sed "y/\`~\!@#$%^&qwertyuiop[]asdfghjkl;'zxcvbnm,.\/QWERTYUIOP{}ASDFGHJKL:\"|ZXCVBNM<>?ёЁ\!\"№;%:?йцукенгшщзхїфівапролджєячсмитьбю.ЙЦУКЕНГШЩЗХЇФІВАПРОЛДЖЄ\/ЯЧСМИТЬБЮ,/’Ё\!\"№;%:?йцукенгшщзхїфівапролджєячсмитьбю.ЙЦУКЕНГШЩЗХЇФІВАПРОЛДЖЄ\/ЯЧСМИТЬБЮ,\`~\!@#$%^&qwertyuiop[]asdfghjkl;'zxcvbnm,.\/QWERTYUIOP{}ASDFGHJKL:\"|ZXCVBNM<>?/" | xclip -selection clipboard

# при проблемах установить задержку по вкусу:
sleep 0.1

# вставляем содержимое буфера обмена
xdotool key Shift+Insert

# восстанавливаем буфер обмена из файла
cat /tmp/~clip.tmp | xclip -in -selection clipboard

# удаляем временные файлы
rm /tmp/~clip.tmp /tmp/~sel.tmp

# опционально меняем раскладку !!! не работает у меня !!!
# xdotool key Shift_L+Capslock

# это "setxkbmap 'ua'" -  переключает раскладку, но "вешает" индикатор
#LANG1="us"
#LANG2="ua"
#CURRENT_LANG=$(setxkbmap -query | tail -n 1 | cut -f6 -d ' ')
#if [ "$CURRENT_LANG" = $LANG1 ]; then
#    setxkbmap $LANG2
#else
#    setxkbmap $LANG1
#fi

# этот вариант тоже не прокатил
#xdotool keydown Shift+Shift
#sleep 1
#xdotool keyup Shift+Shift

# shift иногда может залипать, это решает проблему
# xdotool key Shift

# notify-send "Change Layout" -t 2000
```

Нужно сохранить этот скрипт, дать права на выполнениее, в настройках клавиатуры добавить его, например, на клавишу Pause

<span class="info">i</span> Должна быть установлена маленькая утилитка `xdotool`

  sudo apt install xdotool

<span class="warn">!</span> Бывает, не работает в некоторых окошках


Было бы неплохо и сразу поменять раскладку индикатора, но не получается пока...

```
# опционально меняем раскладку !!! не работает у меня !!!
# xdotool key Shift_L+Capslock

# это "setxkbmap 'ua'" -  переключает раскладку, но "вешает" индикатор
# LANG1="us"
# LANG2="ua"
# CURRENT_LANG=$(setxkbmap -query | tail -n 1 | cut -f6 -d ' ')
# if [ "$CURRENT_LANG" = $LANG1 ]; then
#     setxkbmap $LANG2
# else
#     setxkbmap $LANG1
# fi

#LANG="us"
#CURRENT_LANG=$(setxkbmap -query | tail -n 1 | cut -f6 -d ' ')
#if [ "$CURRENT_LANG" = $LANG ]; then
#    #xdotool key Shift_L+Capslock
#	xdotool keydown Shift_L+Capslock
#	sleep 1
#	xdotool keyup Shift_L+Capslock
#else
#	xdotool keydown Capslock
#	sleep 1
#	xdotool keyup Capslock
#fi

# этот вариант тоже не прокатил
#xdotool keydown Shift+Shift
#sleep 1
#xdotool keyup Shift+Shift

# shift иногда может залипать, это решает проблему
# xdotool key Shift

# notify-send "Change Layout" -t 2000
```
