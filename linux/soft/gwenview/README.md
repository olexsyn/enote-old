# Gwenview

Gwenview - функціональний, з гнучким налаштуванням переглядач зображень від KDE. Але його можна встановити і в інших оточеннях, наприклад, у XFCE.

https://userbase.kde.org/Gwenview/uk

[Gwenview 21.08 worse image quality when enlarging images](https://www.reddit.com/r/kde/comments/slwmyn/gwenview_2108_worse_image_quality_when_enlarging/)

## Встановлення

{% include cl.htm cmd="sudo apt install gwenview" %}

Якщо ваше оточення не KDE, будьте готові, що разом з Gwenview буде встановлено багато KDE-бібліотек, необхідних для фунціювання програми.

## KImageFormats

[Бібліотека плагінів](https://api.kde.org/frameworks/kimageformats/html/index.html), які дозволяють програмам підтримувати додаткові формати файлів.

Підтримується читання таких форматів зображень:

- Animated Windows cursors (ani)
- Gimp (xcf)
- OpenEXR (exr)
- Photoshop documents (psd, psb, pdd, psdt)
- Sun Raster (ras)

Наступні формати зображень підтримують як читання, так і запис:

- AV1 Image File Format (AVIF)
- Encapsulated PostScript (eps)
- JPEG XL (jxl)
- Personal Computer Exchange (pcx)
- SGI images (rgb, rgba, sgi, bw)
- Softimage PIC (pic)
- Targa (tga): supports more formats than Qt's version
- XView (xv)

В деяких дистрибутивах Linux вона **не встановлюється за умовчанням**, тому за потреби її необхідно встановити.

Спочатку треба з'ясувати, яку назву вона має у вашому оточенні:

{% include cl.htm cmd="apt search kimageformat"
out="<b>kimageformat-plugins</b>/jammy,now 5.92.0-0ubuntu1 amd64 [installed]
  Додаткові втулки форматів зображень для QtGui" %}

наприклад, в Ubuntu ця бібліотека має назву **kimageformat-plugins**. І встановити її:

{% include cl.htm cmd="sudo apt install kimageformat-plugins" %}

Після встановлення, також і Okular (переглядач .PDF з KDE), почав відкривати файли, створені Photoshop.

## Гарячі клавіші

У Linux Lite 6.0, (не знаю, як справи у батьківської Ubuntu 22.04) Gwenview встановлюється без жодної "гарячої" комбінації і працює лише через меню та панелі кнопок. Це можна виправити, створивши і завантаживши файл-схему (`Параметри` -> `Налаштувати клавіатурні скорочення` -> `Керування схемами` -> `Додаткові дії` -> `Імпортувати схему`)

Файл **gwenview.shortcuts**, який можна імпортувати у програму. Експорт, налаштувань буде наново переформатовано, можливо, навіть не всі комбінації будуть відтворені, тому зберігаю його тут:

```ini
[Shortcuts]
# файл - додати каталог до вибраних
add_folder_to_places=none
align_with_sidebar=none
browse=Esc
# редагувати - обрізати
crop=Shift+C
# файл - видалити
deletefile=Shift+Del
edit_copy=none
edit_cut=none
edit_location=none
edit_paste=none
# редагувати - повернути останні відхилені зміни
edit_redo=Ctrl+Shift+Z
# редагувати теги (не працює коректно)
edit_tags=none
# редагувати - відхилити останні зміни
edit_undo=Ctrl+Z
# файл - копіювати
file_copy_to=F5; C
# створити каталог
file_create_folder=F7
# створити посилання?
file_link_to=none
# файл - перенести
file_move_to=F6
file_open=Ctrl+O
file_open_containing_folder=none
file_open_recent=none
file_open_with=none
file_print=none
# вийти з програми
file_quit=Q
# файл - перейменувати
file_rename=F2
# ? чим відр. від reload?
file_restore=none
# файл - зберегти
file_save=Ctrl+S
# # файл - зберегти як
file_save_as=Ctrl+Shift+S
# файл - показати властивості
file_show_properties=Alt+Return
# файл - видалити у кошик
file_trash=Del
# редагувати - розвернути по вертикалі
flip=V
fullscreen=Ctrl+Shift+F; F11
# перегляд - стандартна комбінація (home)
go_first=Home; A
# перегляд - стандартна комбінація (end)
go_last=End; Z
# перегляд - вперед
go_next=Space; PgDown; Right
# перегляд - назад
go_previous=Backspace; PgUp; Left
go_start_page=none
go_up=Alt+Up
hamburger_menu=none
help_about_app=none
help_about_kde=none
help_contents=F1
help_donate=none
help_report_bug=none
help_whats_this=Shift+F1
leave_fullscreen=none
mainToolBar=none
# редагувати - розвернути по горизонталі
mirror=H
# панель команд
open_kcommand_bar=Ctrl+Alt+I
options_configure=Ctrl+Shift+,
options_configure_keybinding=Ctrl+Alt+,
options_configure_toolbars=none
# інтерфейс - меню
options_show_menubar=Alt+M
# інтерфейс - смужка статусу
options_show_statusbar=F3
rate_0=none
rate_1=none
rate_2=none
rate_3=none
rate_4=none
rate_5=none
# редагувати - виправити "червоні очі"
red_eye_reduction=Shift+E
# ? чим відр. від file_restore?
reload=Shift+F5
replace_location=none
# редагувати - змінити розмір
resize=Shift+R
# редагувати - повернути ліворуч
rotate_left=L
# редагувати - повернути праворуч
rotate_right=R
# файл - поділитися
share=none
sort_desc=none
# інтерфейс
switch_application_language=none
# ??
synchronize_views=Ctrl+Y
# ??
toggle_operations_sidebar=none
# показати/сховати бокову панель
toggle_sidebar=F4
# перегляд - слайдшоу
toggle_slideshow=none
# інтерфейс - показати мініатюри
toggle_thumbnailbar=Ctrl+B
view=none
# перегляд - актуальний розмір (O)riginal
view_actual_size=O
view_background_colormode_auto=none
view_background_colormode_dark=none
view_background_colormode_light=none
view_background_colormode_neutral=none
view_toggle_birdeyeview=none
# перегляд - збільшити
view_zoom_in=+; =
# перегляд - зменшити
view_zoom_out=-;\s
# розтягти зображення до максимуму по меншій стороні
# (весь екран буде заповнений, але зображення буде обрізане по більшій стороні)
view_zoom_to_fill=Ctrl+F
# розтягти зображення до максимуму по більшій стороні
# (вся картинка буде повністю на екрані)
view_zoom_to_fit=F
```

див.
- /home/olex/.config/gwenviewrc
- /home/olex/.local/share/kxmlgui5/gwenview/gwenviewui.rc


