# more

{% include cl.htm cmd="more --help"
out="Usage:
 more [options] <file>...

A file perusal filter for CRT viewing. / Фільтр перегляду файлів на екрані

Options:
 -d, --silent          display help instead of ringing bell / відображати довідку замість дзвінка
 -f, --logical         count logical rather than screen lines / count logical rather than screen lines
 -l, --no-pause        suppress pause after form feed / придушити паузу після подачі форми
 -c, --print-over      do not scroll, display text and clean line ends / не прокручувати, відображати текст і чисті кінці рядків
 -p, --clean-print     do not scroll, clean screen and display text / не прокручувати, очищати екран і відображати текст
 -s, --squeeze         squeeze multiple blank lines into one / стиснути кілька порожніх рядків в один
 -u, --plain           suppress underlining and bold / придушити підкреслення та жирний
 -n, --lines <number>  the number of lines per screenful / кількість рядків на екрані
 -<number>             same as --lines / те саме, що й --lines
 +<number>             display file beginning from line number / відобразити файл, починаючи з номера рядка
 +/<pattern>           display file beginning from pattern match / відобразити файл, починаючи з відповідності шаблону

 -h, --help            display this help
 -V, --version         display version

For more details see more(1).
" %}
