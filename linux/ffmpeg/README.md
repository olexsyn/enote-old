# Linux. Programs. ffmpeg

`ffmpeg -r 60 -g 600 -s 1680x1050 -f x11grab -i :0.0 -s 800x600 -vcodec qtrle screencast.mov`

- 1-f x11grab - брать поток с экрана
- 2-r 60 - 60 кадров
- 3-s 1680x1050 - моё разрешение экрана
- 4-i :0.0 - в качестве источника мой экран
- 5-vcodec qtrle - кодек,
- 6-s 800x500 - получаемое разрешение
- 7-screencast.mov - выходной файл

---

Режет, конвертирует, например mkv в avi.

Установка:

`sudo apt-get install ffmpeg`

Пример порезки видео:

`ffmpeg -ss 00:01:30 -t 00:00:15 -i video_in.mov -vcodec copy video_out.mov`

- -ss - откуда резать
- -t - сколько резать
- -vcodec copy - не перекодировать (должно стоять после исходного файла)
- -аcodec copy - пробовал, убрало звук

Без звука (`-an`):

`ffmpeg -ss 00:00:00 -t 00:00:05 -i video.mp4 -vcodec copy -an video_out.mp4`

Пример порезки mp3:

`ffmpeg -acodec copy -ss 00:00:50 -t 00:00:30 -i /home/ans/music_in.mp3 /home/ans/music_out.mp3`

## Основные параметры

`-f  fmt` – формат в который происходит конвертация

`-i  filename` – имя входящего файла (который будет конвертироваться)

`-y`  – перезаписать полученный после конвертации файл(ы). Глобальный параметр,  должен быть определен в начале.

### Видео параметры:

`-b  bitrate` – битрейт видео

`-r  fps` – установить частоту кадров (по умолчанию 25)

`-s  size` – установить размер кадра

* ‘qvga’  320×240
* ’sxga’ 1280×1024

`-target type` - specify target file type ("vcd", "svcd", "dvd", "dv", "dv50", "pal-vcd", "ntsc-svcd", ...)
### Аудио параметры

`-ar  freq` – установить частоту аудио

`-ac  channels` – установить количество аудио каналов.

`-acodec  codec` – установить аудио кодек (алиас для -codec:a)

### Дополнительные

`-vhook`  – плагин для создания вотермарки

пример использования:

  -vhook ‘/usr/local/lib/vhook/imlib2.so -x W-w -y H-h -i /watermark.gif’

Пример:

  ffmpeg -y -i /var/video/input_file.mp4 -acodec libfaac -ac 1 -b 225k -s 320x240 -r 25 -ar 22050 -vhook '/usr/local/lib/vhook/imlib2.so -x W-w -y H-h -i /watermark.gif' -f flv /var/video/output_file.flv


## Примеры использования

**Показать информацию по файлу:**

  ffmpeg -i sample.avi

Кроме того, для получения информации следует использовать

  ffprobe video.avi

Так же ffprobe поддерживает несколько форматов для вывода информации ini, json, xml

  ffprobe -v 0 video.avi -print_format json -show_format
  ffprobe -v 0 video.avi -print_format xml -show_format
  ffprobe -v 0 video.avi -print_format ini -show_format

**Превратить набор картинок в видео**

  ffmpeg -f image2 -i image%d.jpg video.mpg

Эта команда преобразует все картинки из текущей директории (названные image1.jpg, image2.jpg и т.д.) в видеофайл video.mpg

(примечание переводчика) мне больше нравится такой формат:

  ffmpeg -r 12 -y -i "image_%010d.png" output.mpg

здесь задаётся frame rate (12) для видео, формат «image_%010d.png» означает, что картинки будут искаться в виде image_0000000001.png, image_0000000002.png и тд, то есть, в формате printf)

будет кадр в секунду. Параметр -r указывает нужный frame rate:

  ffmpeg -r 1 -y -i "image_%010d.png" output.mpg

Можно ставить дробное: -r 0.1 даст кадр в 10 секунд.

**Разложение видеоряда на кадры:**

  ffmpeg -i video.mpg image%d.jpg

Будут сгенерированы файлы image1.jpg, image2.jpg и т.д… Поддерживаемые графические форматы: PGM, PPM, PAM, PGMYUV, JPEG, GIF, PNG, TIFF, SGI.

**Склейка 2х и более видео в один:**

Если ролики в одинаковых форматах с одинаковыми параметрами:

  ffmpeg -i "concat:input1.mpg|input2.mpg|input3.mpg" -c copy output.mpg

Если разные:

  ffmpeg -i input1.mp4 -i input2.webm \
  -filter_complex '[0:0] [0:1] [1:0] [1:1] concat=n=2:v=1:a=1 [v] [a]' \
  -map '[v]' -map '[a]' <encoding options> output.mkv

**Кодирование видеоряда для Apple iPod/iPhone:**

  ffmpeg -i source_video.avi input -acodec aac -ab 128kb -vcodec mpeg4 -b 1200kb -mbd 2 -flags +4mv+trell -aic 2 -cmp 2 -subcmp 2 -s 320x180 -title X final_video.mp4

**Извлечь звуковую дорожку из видео и сохранить в MP3:**

  ffmpeg -i source_video.avi -vn -ar 44100 -ac 2 -ab 192 -f mp3 sound.mp3

Пояснения:

* Источник: source_video.avi
* Битрейт аудио: 192kb/s
* Выходной формат: mp3
* Полученный аудиофайл: sound.mp3

**Преобразование WAV в MP3:**

  ffmpeg -i son_original.wav -vn -ar 44100 -ac 2 -ab 192 -f mp3 son_final.mp3

**Выдираем звук из видео в формате MP4 и сжимаем его в MP3:**

```
$ cat mp4tomp3.sh
#!/bin/sh
for file in "$@" ; do
name=`echo "$file" | sed -e "s/.mp4$//g"`
ffmpeg -i "$file" -ac 2 -f wav - | lame --preset standard - "$name.mp3"
done
```

**AVI в MPG:**

  ffmpeg -i video_source.avi video_final.mpg

**MPG в AVI:**

  ffmpeg -i video_source.mpg video_final.avi

**Кодирование видеоряда для Apple iPod/iPhone:**

  ffmpeg -i source_video.avi input -acodec aac -ab 128kb -vcodec mpeg4 -b 1200kb -mbd 2 -flags +4mv+trell -aic 2 -cmp 2 -subcmp 2 -s 320x180 -title X final_video.mp4

Пояснения:

* Источник: source_video.avi
* Аудио кодек: aac
* Битрейт аудио: 128kb/s
* Видео кодек: mpeg4
* Битрейт видео: 1200kb/s
* Размер видео: 320 на 180 пикселей
* Полученное видео: final_video.mp4

**Для Sony PSP:**

  ffmpeg -i source_video.avi -b 300 -s 320x240 -vcodec xvid -ab 32 -ar 24000 -acodec aac final_video.mp4

Пояснения:

* Источник: source_video.avi
* Аудио кодек: aac
* Битрейт аудио: 32kb/s
* Видео кодек: xvid
* Битрейт видео: 1200kb/s
* Размер видео: 320 на 180 пикселей
* Полученное видео: final_video.mp4


**Конвертация AVI-файла в несжатый анимированный GIF:**

  ffmpeg -i video_source.avi gif_anime.gif

**Смешение аудио- и видеопотока в один результирующий файл:**

  ffmpeg -i son.wav -i video_source.avi video_final.mpg

**Преобразование AVI в FLV:**

  ffmpeg -i video_source.avi -ab 56 -ar 44100 -b 200 -r 15 -s 320x240 -f flv video_final.flv

**FLV в AVI:**

  ffmpeg -i video_source.flv -ab 56 -ar 44100 -b 200 -s 320x240 video_final.avi

**FLAC в MP3:**

  ffmpeg -i audio_original.flac -ab 320k -ac 2 -ar 48000 audio_final.mp3

**Конвертировать .avi в mpeg для DVD-плееров**

  ffmpeg -i source_video.avi -target pal-dvd -ps 2000000000 -aspect 16:9 finale_video.mpeg

Пояснения:

Выходной формат: pal-dvd
Максимальный размер для выходного файла: 2000000000 (2 Gb)
Широкоэкранный формат: 16:9

**Сжать .avi в DivX**

  ffmpeg -i video_origine.avi -s 320x240 -vcodec msmpeg4v2 video_finale.avi

**Сжать OGG Theora в mpeg DVD**

  ffmpeg -i film_sortie_cinelerra.ogm -s 720x576 -vcodec mpeg2video -acodec mp3 film_termin.mpg

**Сжать .avi в SVCD mpeg2**

Формат NTSC:

  ffmpeg -i video_origine.avi -target ntsc-svcd video_finale.mpg

Формат PAL:

  ffmpeg -i video_origine.avi -target pal-svcd video_finale.mpg

**Сжать .avi в VCD mpeg2**

Формат NTSC:

  ffmpeg -i video_origine.avi -target ntsc-vcd video_finale.mpg

Формат PAL:

  ffmpeg -i video_origine.avi -target pal-vcd video_finale.mpg

**Многопроходное кодирование с помощью ffmpeg**

  ffmpeg -i fichierentree -pass 2 -passlogfile ffmpeg2pass fichiersortie-2

**Вырезать один кадр из видео** для создания, например, превью на сайте или в админке

  ffmpeg -i "file.flv" -f image2 -vframes 1 -ss 00:00:02 "file_out.jpg"

Вырезает первый кадр второй секунды из файла file.flv и сохраняет её в файле file_out.jpg.

**Повернуть видео на 90°**

  ffmpeg -vf transpose=1 -i file.avi file1.avi

Опции transpose:

  0 — против часовой стрелки и зеркально;
  1 — по часовой стрелке;
  2 — против часовой стрелки;
  3 — по часовой стрелке и зеркально

**Захват видео с экрана:**

  ffmpeg -f x11grab -s cif -r 25 -i :0.0+10,20 /tmp/out.mpg

здесь -s cif — размер, 0.0 — экран, 10,20 — это смещение относительно верхнего левого угла экрана

при желании можно и звук, например, с alsa или jack присобачить

**Ватермарк:**

  ffmpeg -i in.mp4 -vfilters "movie=0:gif:logo.gif [logo]; [in][logo] overlay=10:mainH-overlayH-10:1 [out]" out.mp4

Но тут все довольно сложно. Старые версии делали ватермарки через vhook, новые делают через libavfilter. Насколько помню за последний год его то включают то выключают из-за разных багов.

http://habr.com/post/171213/

## Все параметры

```
Hyper fast Audio and Video encoder
usage: ffmpeg [options] [[infile options] -i infile]... {[outfile options] outfile}...

Main options:
-L                  show license
-h                  show help
-?                  show help
-help               show help
--help              show help
-version            show version
-formats            show available formats
-codecs             show available codecs
-bsfs               show available bit stream filters
-protocols          show available protocols
-filters            show available filters
-pix_fmts           show available pixel formats
-loglevel loglevel  set libav* logging level
-f fmt              force format
-i filename         input file name
-y                  overwrite output files
-t duration         record or transcode "duration" seconds of audio/video
-fs limit_size      set the limit file size in bytes
-ss time_off        set the start time offset
-itsoffset time_off  set the input ts offset
-itsscale stream:scale  set the input ts scale
-timestamp time     set the timestamp ('now' to set the current time)
-metadata string=string  add metadata
-dframes number     set the number of data frames to record
-timelimit limit    set max runtime in seconds
-v number           set ffmpeg verbosity level
-target type        specify target file type ("vcd", "svcd", "dvd", "dv", "dv50", "pal-vcd", "ntsc-svcd", ...)
-xerror             exit on error

Advanced options:
-map file:stream[:syncfile:syncstream]  set input stream mapping
-map_meta_data outfile:infile  set meta data information of outfile from infile
-benchmark          add timings for benchmarking
-dump               dump each input packet
-hex                when dumping packets, also dump the payload
-re                 read input at native frame rate
-loop_input         loop (current only works with images)
-loop_output        number of times to loop output in formats that support looping (0 loops forever)
-threads count      thread count
-vsync              video sync method
-async              audio sync method
-adrift_threshold threshold  audio drift threshold
-vglobal            video global header storage type
-copyts             copy timestamps
-shortest           finish encoding within shortest input
-dts_delta_threshold threshold  timestamp discontinuity delta threshold
-programid          desired program number
-copyinkf           copy initial non-keyframes
-muxdelay seconds   set the maximum demux-decode delay
-muxpreload seconds  set the initial demux-decode delay
-fpre filename      set options from indicated preset file

Video options:
-b bitrate          set bitrate (in bits/s)
-vb bitrate         set bitrate (in bits/s)
-vframes number     set the number of video frames to record
-r rate             set frame rate (Hz value, fraction or abbreviation)
-s size             set frame size (WxH or abbreviation)
-aspect aspect      set aspect ratio (4:3, 16:9 or 1.3333, 1.7777)
-croptop size       set top crop band size (in pixels)
-cropbottom size    set bottom crop band size (in pixels)
-cropleft size      set left crop band size (in pixels)
-cropright size     set right crop band size (in pixels)
-padtop size        set top pad band size (in pixels)
-padbottom size     set bottom pad band size (in pixels)
-padleft size       set left pad band size (in pixels)
-padright size      set right pad band size (in pixels)
-padcolor color     set color of pad bands (Hex 000000 thru FFFFFF)
-vn                 disable video
-vcodec codec       force video codec ('copy' to copy stream)
-sameq              use same video quality as source (implies VBR)
-pass n             select the pass number (1 or 2)
-passlogfile prefix  select two pass log file name prefix
-newvideo           add a new video stream to the current output stream
-vlang code         set the ISO 639 language code (3 letters) of the current video stream

Advanced Video options:
-pix_fmt format     set pixel format, 'list' as argument shows all the pixel formats supported
-intra              use only intra frames
-vdt n              discard threshold
-qscale q           use fixed video quantizer scale (VBR)
-rc_override override  rate control override for specific intervals
-me_threshold threshold  motion estimaton threshold
-deinterlace        deinterlace pictures
-psnr               calculate PSNR of compressed frames
-vstats             dump video coding statistics to file
-vstats_file file   dump video coding statistics to file
-intra_matrix matrix  specify intra matrix coeffs
-inter_matrix matrix  specify inter matrix coeffs
-top                top=1/bottom=0/auto=-1 field first
-dc precision       intra_dc_precision
-vtag fourcc/tag    force video tag/fourcc
-qphist             show QP histogram
-force_fps          force the selected framerate, disable the best supported framerate selection
-vbsf bitstream_filter
-vpre preset        set the video options to the indicated preset

Audio options:
-ab bitrate         set bitrate (in bits/s)
-aframes number     set the number of audio frames to record
-aq quality         set audio quality (codec-specific)
-ar rate            set audio sampling rate (in Hz)
-ac channels        set number of audio channels
-an                 disable audio
-acodec codec       force audio codec ('copy' to copy stream)
-vol volume         change audio volume (256=normal)
-newaudio           add a new audio stream to the current output stream
-alang code         set the ISO 639 language code (3 letters) of the current audio stream

Advanced Audio options:
-atag fourcc/tag    force audio tag/fourcc
-sample_fmt format  set sample format, 'list' as argument shows all the sample formats supported
-absf bitstream_filter
-apre preset        set the audio options to the indicated preset

Subtitle options:
-sn                 disable subtitle
-scodec codec       force subtitle codec ('copy' to copy stream)
-newsubtitle        add a new subtitle stream to the current output stream
-slang code         set the ISO 639 language code (3 letters) of the current subtitle stream
-stag fourcc/tag    force subtitle tag/fourcc
-sbsf bitstream_filter
-spre preset        set the subtitle options to the indicated preset

Audio/Video grab options:
-vc channel         set video grab channel (DV1394 only)
-tvstd standard     set television standard (NTSC, PAL (SECAM))
-isync              sync read on input

AVCodecContext AVOptions:
-b                 <int>   E.V.. set bitrate (in bits/s)
-ab                <int>   E..A. set bitrate (in bits/s)
-bt                <int>   E.V.. set video bitrate tolerance (in bits/s)
-flags             <flags> EDVA.
   mv4                     E.V.. use four motion vector by macroblock (mpeg4)
   obmc                    E.V.. use overlapped block motion compensation (h263+)
   qpel                    E.V.. use 1/4 pel motion compensation
   loop                    E.V.. use loop filter
   gmc                     E.V.. use gmc
   mv0                     E.V.. always try a mb with mv=<0,0>
   part                    E.V.. use data partitioning
   gray                    EDV.. only decode/encode grayscale
   psnr                    E.V.. error[?] variables will be set during encoding
   naq                     E.V.. normalize adaptive quantization
   ildct                   E.V.. use interlaced dct
   low_delay               EDV.. force low delay
   alt                     E.V.. enable alternate scantable (mpeg2/mpeg4)
   global_header           E.VA. place global headers in extradata instead of every keyframe
   bitexact                EDVAS use only bitexact stuff (except (i)dct)
   aic                     E.V.. h263 advanced intra coding / mpeg4 ac prediction
   umv                     E.V.. use unlimited motion vectors
   cbp                     E.V.. use rate distortion optimization for cbp
   qprd                    E.V.. use rate distortion optimization for qp selection
   aiv                     E.V.. h263 alternative inter vlc
   slice                   E.V..
   ilme                    E.V.. interlaced motion estimation
   scan_offset             E.V.. will reserve space for svcd scan offset user data
   cgop                    E.V.. closed gop
-me_method         <int>   E.V.. set motion estimation method
   zero                    E.V.. zero motion estimation (fastest)
   full                    E.V.. full motion estimation (slowest)
   epzs                    E.V.. EPZS motion estimation (default)
   esa                     E.V.. esa motion estimation (alias for full)
   tesa                    E.V.. tesa motion estimation
   dia                     E.V.. dia motion estimation (alias for epzs)
   log                     E.V.. log motion estimation
   phods                   E.V.. phods motion estimation
   x1                      E.V.. X1 motion estimation
   hex                     E.V.. hex motion estimation
   umh                     E.V.. umh motion estimation
   iter                    E.V.. iter motion estimation
-g                 <int>   E.V.. set the group of picture size
-cutoff            <int>   E..A. set cutoff bandwidth
-frame_size        <int>   E..A.
-qcomp             <float> E.V.. video quantizer scale compression (VBR)
-qblur             <float> E.V.. video quantizer scale blur (VBR)
-qmin              <int>   E.V.. min video quantizer scale (VBR)
-qmax              <int>   E.V.. max video quantizer scale (VBR)
-qdiff             <int>   E.V.. max difference between the quantizer scale (VBR)
-bf                <int>   E.V.. use 'frames' B frames
-b_qfactor         <float> E.V.. qp factor between p and b frames
-rc_strategy       <int>   E.V.. ratecontrol method
-b_strategy        <int>   E.V.. strategy to choose between I/P/B-frames
-wpredp            <int>   E.V.. weighted prediction analysis method
-hurry_up          <int>   .DV..
-ps                <int>   E.V.. rtp payload size in bytes
-bug               <flags> .DV.. workaround not auto detected encoder bugs
   autodetect              .DV..
   old_msmpeg4             .DV.. some old lavc generated msmpeg4v3 files (no autodetection)
   xvid_ilace              .DV.. Xvid interlacing bug (autodetected if fourcc==XVIX)
   ump4                    .DV.. (autodetected if fourcc==UMP4)
   no_padding              .DV.. padding bug (autodetected)
   amv                     .DV..
   ac_vlc                  .DV.. illegal vlc bug (autodetected per fourcc)
   qpel_chroma             .DV..
   std_qpel                .DV.. old standard qpel (autodetected per fourcc/version)
   qpel_chroma2            .DV..
   direct_blocksize         .DV.. direct-qpel-blocksize bug (autodetected per fourcc/version)
   edge                    .DV.. edge padding bug (autodetected per fourcc/version)
   hpel_chroma             .DV..
   dc_clip                 .DV..
   ms                      .DV.. workaround various bugs in microsofts broken decoders
   trunc                   .DV.. trancated frames
-lelim             <int>   E.V.. single coefficient elimination threshold for luminance (negative values also consider dc coefficient)
-celim             <int>   E.V.. single coefficient elimination threshold for chrominance (negative values also consider dc coefficient)
-strict            <int>   EDVA. how strictly to follow the standards
   very                    EDV.. strictly conform to a older more strict version of the spec or reference software
   strict                  EDV.. strictly conform to all the things in the spec no matter what consequences
   normal                  EDV..
   inofficial              EDV.. allow unofficial extensions
   experimental            EDV.. allow non standardized experimental things
-b_qoffset         <float> E.V.. qp offset between P and B frames
-er                <int>   .DVA. set error detection aggressivity
   careful                 .DV..
   compliant               .DV..
   aggressive              .DV..
   very_aggressive         .DV..
-mpeg_quant        <int>   E.V.. use MPEG quantizers instead of H.263
-qsquish           <float> E.V.. how to keep quantizer between qmin and qmax (0 = clip, 1 = use differentiable function)
-rc_qmod_amp       <float> E.V.. experimental quantizer modulation
-rc_qmod_freq      <int>   E.V.. experimental quantizer modulation
-rc_eq             <string> E.V.. set rate control equation
-maxrate           <int>   E.V.. set max video bitrate tolerance (in bits/s)
-minrate           <int>   E.V.. set min video bitrate tolerance (in bits/s)
-bufsize           <int>   E.VA. set ratecontrol buffer size (in bits)
-rc_buf_aggressivity <float> E.V.. currently useless
-i_qfactor         <float> E.V.. qp factor between P and I frames
-i_qoffset         <float> E.V.. qp offset between P and I frames
-rc_init_cplx      <float> E.V.. initial complexity for 1-pass encoding
-dct               <int>   E.V.. DCT algorithm
   auto                    E.V.. autoselect a good one (default)
   fastint                 E.V.. fast integer
   int                     E.V.. accurate integer
   mmx                     E.V..
   mlib                    E.V..
   altivec                 E.V..
   faan                    E.V.. floating point AAN DCT
-lumi_mask         <float> E.V.. compresses bright areas stronger than medium ones
-tcplx_mask        <float> E.V.. temporal complexity masking
-scplx_mask        <float> E.V.. spatial complexity masking
-p_mask            <float> E.V.. inter masking
-dark_mask         <float> E.V.. compresses dark areas stronger than medium ones
-idct              <int>   EDV.. select IDCT implementation
   auto                    EDV..
   int                     EDV..
   simple                  EDV..
   simplemmx               EDV..
   libmpeg2mmx             EDV..
   ps2                     EDV..
   mlib                    EDV..
   arm                     EDV..
   altivec                 EDV..
   sh4                     EDV..
   simplearm               EDV..
   simplearmv5te           EDV..
   simplearmv6             EDV..
   simpleneon              EDV..
   simplealpha             EDV..
   h264                    EDV..
   vp3                     EDV..
   ipp                     EDV..
   xvidmmx                 EDV..
   faani                   EDV.. floating point AAN IDCT
-ec                <flags> .DV.. set error concealment strategy
   guess_mvs               .DV.. iterative motion vector (MV) search (slow)
   deblock                 .DV.. use strong deblock filter for damaged MBs
-pred              <int>   E.V.. prediction method
   left                    E.V..
   plane                   E.V..
   median                  E.V..
-aspect            <rational> E.V.. sample aspect ratio
-debug             <flags> EDVAS print specific debug info
   pict                    .DV.. picture info
   rc                      E.V.. rate control
   bitstream               .DV..
   mb_type                 .DV.. macroblock (MB) type
   qp                      .DV.. per-block quantization parameter (QP)
   mv                      .DV.. motion vector
   dct_coeff               .DV..
   skip                    .DV..
   startcode               .DV..
   pts                     .DV..
   er                      .DV.. error recognition
   mmco                    .DV.. memory management control operations (H.264)
   bugs                    .DV..
   vis_qp                  .DV.. visualize quantization parameter (QP), lower QP are tinted greener
   vis_mb_type             .DV.. visualize block types
   buffers                 .DV.. picture buffer allocations
-vismv             <int>   .DV.. visualize motion vectors (MVs)
   pf                      .DV.. forward predicted MVs of P-frames
   bf                      .DV.. forward predicted MVs of B-frames
   bb                      .DV.. backward predicted MVs of B-frames
-mb_qmin           <int>   E.V.. obsolete, use qmin
-mb_qmax           <int>   E.V.. obsolete, use qmax
-cmp               <int>   E.V.. full pel me compare function
   sad                     E.V.. sum of absolute differences, fast (default)
   sse                     E.V.. sum of squared errors
   satd                    E.V.. sum of absolute Hadamard transformed differences
   dct                     E.V.. sum of absolute DCT transformed differences
   psnr                    E.V.. sum of squared quantization errors (avoid, low quality)
   bit                     E.V.. number of bits needed for the block
   rd                      E.V.. rate distortion optimal, slow
   zero                    E.V.. 0
   vsad                    E.V.. sum of absolute vertical differences
   vsse                    E.V.. sum of squared vertical differences
   nsse                    E.V.. noise preserving sum of squared differences
   w53                     E.V.. 5/3 wavelet, only used in snow
   w97                     E.V.. 9/7 wavelet, only used in snow
   dctmax                  E.V..
   chroma                  E.V..
-subcmp            <int>   E.V.. sub pel me compare function
   sad                     E.V.. sum of absolute differences, fast (default)
   sse                     E.V.. sum of squared errors
   satd                    E.V.. sum of absolute Hadamard transformed differences
   dct                     E.V.. sum of absolute DCT transformed differences
   psnr                    E.V.. sum of squared quantization errors (avoid, low quality)
   bit                     E.V.. number of bits needed for the block
   rd                      E.V.. rate distortion optimal, slow
   zero                    E.V.. 0
   vsad                    E.V.. sum of absolute vertical differences
   vsse                    E.V.. sum of squared vertical differences
   nsse                    E.V.. noise preserving sum of squared differences
   w53                     E.V.. 5/3 wavelet, only used in snow
   w97                     E.V.. 9/7 wavelet, only used in snow
   dctmax                  E.V..
   chroma                  E.V..
-mbcmp             <int>   E.V.. macroblock compare function
   sad                     E.V.. sum of absolute differences, fast (default)
   sse                     E.V.. sum of squared errors
   satd                    E.V.. sum of absolute Hadamard transformed differences
   dct                     E.V.. sum of absolute DCT transformed differences
   psnr                    E.V.. sum of squared quantization errors (avoid, low quality)
   bit                     E.V.. number of bits needed for the block
   rd                      E.V.. rate distortion optimal, slow
   zero                    E.V.. 0
   vsad                    E.V.. sum of absolute vertical differences
   vsse                    E.V.. sum of squared vertical differences
   nsse                    E.V.. noise preserving sum of squared differences
   w53                     E.V.. 5/3 wavelet, only used in snow
   w97                     E.V.. 9/7 wavelet, only used in snow
   dctmax                  E.V..
   chroma                  E.V..
-ildctcmp          <int>   E.V.. interlaced dct compare function
   sad                     E.V.. sum of absolute differences, fast (default)
   sse                     E.V.. sum of squared errors
   satd                    E.V.. sum of absolute Hadamard transformed differences
   dct                     E.V.. sum of absolute DCT transformed differences
   psnr                    E.V.. sum of squared quantization errors (avoid, low quality)
   bit                     E.V.. number of bits needed for the block
   rd                      E.V.. rate distortion optimal, slow
   zero                    E.V.. 0
   vsad                    E.V.. sum of absolute vertical differences
   vsse                    E.V.. sum of squared vertical differences
   nsse                    E.V.. noise preserving sum of squared differences
   w53                     E.V.. 5/3 wavelet, only used in snow
   w97                     E.V.. 9/7 wavelet, only used in snow
   dctmax                  E.V..
   chroma                  E.V..
-dia_size          <int>   E.V.. diamond type & size for motion estimation
-last_pred         <int>   E.V.. amount of motion predictors from the previous frame
-preme             <int>   E.V.. pre motion estimation
-precmp            <int>   E.V.. pre motion estimation compare function
   sad                     E.V.. sum of absolute differences, fast (default)
   sse                     E.V.. sum of squared errors
   satd                    E.V.. sum of absolute Hadamard transformed differences
   dct                     E.V.. sum of absolute DCT transformed differences
   psnr                    E.V.. sum of squared quantization errors (avoid, low quality)
   bit                     E.V.. number of bits needed for the block
   rd                      E.V.. rate distortion optimal, slow
   zero                    E.V.. 0
   vsad                    E.V.. sum of absolute vertical differences
   vsse                    E.V.. sum of squared vertical differences
   nsse                    E.V.. noise preserving sum of squared differences
   w53                     E.V.. 5/3 wavelet, only used in snow
   w97                     E.V.. 9/7 wavelet, only used in snow
   dctmax                  E.V..
   chroma                  E.V..
-pre_dia_size      <int>   E.V.. diamond type & size for motion estimation pre-pass
-subq              <int>   E.V.. sub pel motion estimation quality
-me_range          <int>   E.V.. limit motion vectors range (1023 for DivX player)
-ibias             <int>   E.V.. intra quant bias
-pbias             <int>   E.V.. inter quant bias
-coder             <int>   E.V..
   vlc                     E.V.. variable length coder / huffman coder
   ac                      E.V.. arithmetic coder
   raw                     E.V.. raw (no encoding)
   rle                     E.V.. run-length coder
   deflate                 E.V.. deflate-based coder
-context           <int>   E.V.. context model
-mbd               <int>   E.V.. macroblock decision algorithm (high quality mode)
   simple                  E.V.. use mbcmp (default)
   bits                    E.V.. use fewest bits
   rd                      E.V.. use best rate distortion
-sc_threshold      <int>   E.V.. scene change threshold
-lmin              <int>   E.V.. min lagrange factor (VBR)
-lmax              <int>   E.V.. max lagrange factor (VBR)
-nr                <int>   E.V.. noise reduction
-rc_init_occupancy <int>   E.V.. number of bits which should be loaded into the rc buffer before decoding starts
-inter_threshold   <int>   E.V..
-flags2            <flags> EDVA.
   fast                    E.V.. allow non spec compliant speedup tricks
   sgop                    E.V.. strictly enforce gop size
   noout                   E.V.. skip bitstream encoding
   local_header            E.V.. place global headers at every keyframe instead of in extradata
   bpyramid                E.V.. allows B-frames to be used as references for predicting
   wpred                   E.V.. weighted biprediction for b-frames (H.264)
   mixed_refs              E.V.. one reference per partition, as opposed to one reference per macroblock
   dct8x8                  E.V.. high profile 8x8 transform (H.264)
   fastpskip               E.V.. fast pskip (H.264)
   aud                     E.V.. access unit delimiters (H.264)
   skiprd                  E.V.. RD optimal MB level residual skipping
   ivlc                    E.V.. intra vlc table
   drop_frame_timecode         E.V..
   non_linear_q            E.V.. use non linear quantizer
   reservoir               E..A. use bit reservoir
   mbtree                  E.V.. use macroblock tree ratecontrol (x264 only)
   psy                     E.V.. use psycho visual optimization
   ssim                    E.V.. ssim will be calculated during encoding
-error             <int>   E.V..
-antialias         <int>   .DV.. MP3 antialias algorithm
   auto                    .DV..
   fastint                 .DV..
   int                     .DV..
   float                   .DV..
-qns               <int>   E.V.. quantizer noise shaping
-threads           <int>   EDV..
-mb_threshold      <int>   E.V.. macroblock threshold
-dc                <int>   E.V.. intra_dc_precision
-nssew             <int>   E.V.. nsse weight
-skip_top          <int>   .DV.. number of macroblock rows at the top which are skipped
-skip_bottom       <int>   .DV.. number of macroblock rows at the bottom which are skipped
-profile           <int>   E.VA.
   unknown                 E.VA.
   aac_main                E..A.
   aac_low                 E..A.
   aac_ssr                 E..A.
   aac_ltp                 E..A.
-level             <int>   E.VA.
   unknown                 E.VA.
-lowres            <int>   .DV.. decode at 1= 1/2, 2=1/4, 3=1/8 resolutions
-skip_threshold    <int>   E.V.. frame skip threshold
-skip_factor       <int>   E.V.. frame skip factor
-skip_exp          <int>   E.V.. frame skip exponent
-skipcmp           <int>   E.V.. frame skip compare function
   sad                     E.V.. sum of absolute differences, fast (default)
   sse                     E.V.. sum of squared errors
   satd                    E.V.. sum of absolute Hadamard transformed differences
   dct                     E.V.. sum of absolute DCT transformed differences
   psnr                    E.V.. sum of squared quantization errors (avoid, low quality)
   bit                     E.V.. number of bits needed for the block
   rd                      E.V.. rate distortion optimal, slow
   zero                    E.V.. 0
   vsad                    E.V.. sum of absolute vertical differences
   vsse                    E.V.. sum of squared vertical differences
   nsse                    E.V.. noise preserving sum of squared differences
   w53                     E.V.. 5/3 wavelet, only used in snow
   w97                     E.V.. 9/7 wavelet, only used in snow
   dctmax                  E.V..
   chroma                  E.V..
-border_mask       <float> E.V.. increases the quantizer for macroblocks close to borders
-mblmin            <int>   E.V.. min macroblock lagrange factor (VBR)
-mblmax            <int>   E.V.. max macroblock lagrange factor (VBR)
-mepc              <int>   E.V.. motion estimation bitrate penalty compensation (1.0 = 256)
-skip_loop_filter  <int>   .DV..
   none                    .DV..
   default                 .DV..
   noref                   .DV..
   bidir                   .DV..
   nokey                   .DV..
   all                     .DV..
-skip_idct         <int>   .DV..
   none                    .DV..
   default                 .DV..
   noref                   .DV..
   bidir                   .DV..
   nokey                   .DV..
   all                     .DV..
-skip_frame        <int>   .DV..
   none                    .DV..
   default                 .DV..
   noref                   .DV..
   bidir                   .DV..
   nokey                   .DV..
   all                     .DV..
-bidir_refine      <int>   E.V.. refine the two motion vectors used in bidirectional macroblocks
-brd_scale         <int>   E.V.. downscales frames for dynamic B-frame decision
-crf               <float> E.V.. enables constant quality mode, and selects the quality (x264)
-cqp               <int>   E.V.. constant quantization parameter rate control method
-keyint_min        <int>   E.V.. minimum interval between IDR-frames (x264)
-refs              <int>   E.V.. reference frames to consider for motion compensation (Snow)
-chromaoffset      <int>   E.V.. chroma qp offset from luma
-bframebias        <int>   E.V.. influences how often B-frames are used
-trellis           <int>   E.VA. rate-distortion optimal quantization
-directpred        <int>   E.V.. direct mv prediction mode - 0 (none), 1 (spatial), 2 (temporal), 3 (auto)
-complexityblur    <float> E.V.. reduce fluctuations in qp (before curve compression)
-deblockalpha      <int>   E.V.. in-loop deblocking filter alphac0 parameter
-deblockbeta       <int>   E.V.. in-loop deblocking filter beta parameter
-partitions        <flags> E.V.. macroblock subpartition sizes to consider
   parti4x4                E.V..
   parti8x8                E.V..
   partp4x4                E.V..
   partp8x8                E.V..
   partb8x8                E.V..
-sc_factor         <int>   E.V.. multiplied by qscale for each frame and added to scene_change_score
-mv0_threshold     <int>   E.V..
-b_sensitivity     <int>   E.V.. adjusts sensitivity of b_frame_strategy 1
-compression_level <int>   E.VA.
-use_lpc           <int>   E..A. sets whether to use LPC mode (FLAC)
-lpc_coeff_precision <int>   E..A. LPC coefficient precision (FLAC)
-min_prediction_order <int>   E..A.
-max_prediction_order <int>   E..A.
-prediction_order_method <int>   E..A. search method for selecting prediction order
-min_partition_order <int>   E..A.
-max_partition_order <int>   E..A.
-timecode_frame_start <int64> E.V.. GOP timecode frame start number, in non drop frame format
-request_channels  <int>   .D.A. set desired number of audio channels
-drc_scale         <float> .D.A. percentage of dynamic range compression to apply
-channel_layout    <int64> ED.A.
-request_channel_layout <int64> .D.A.
-rc_max_vbv_use    <float> E.V..
-rc_min_vbv_use    <float> E.V..
-ticks_per_frame   <int>   EDVA.
-color_primaries   <int>   EDV..
-color_trc         <int>   EDV..
-colorspace        <int>   EDV..
-color_range       <int>   EDV..
-chroma_sample_location <int>   EDV..
-psy_rd            <float> E.V.. specify psycho visual strength
-psy_trellis       <float> E.V.. specify psycho visual trellis
-aq_mode           <int>   E.V.. specify aq method
-aq_strength       <float> E.V.. specify aq strength
-rc_lookahead      <int>   E.V.. specify number of frames to look ahead for frametype

AVFormatContext AVOptions:
-probesize         <int>   .D... set probing size
-muxrate           <int>   E.... set mux rate
-packetsize        <int>   E.... set packet size
-fflags            <flags> ED...
   ignidx                  .D... ignore index
   genpts                  .D... generate pts
   nofillin                .D... do not fill in missing values that can be exactly calculated
   noparse                 .D... disable AVParsers, this needs nofillin too
   igndts                  .D... ingore dts
   rtphint                 E.... add rtp hinting
-track             <int>   E....  set the track number
-year              <int>   E.... set the year
-analyzeduration   <int>   .D... how many microseconds are analyzed to estimate duration
-cryptokey         <binary> .D... decryption key
-indexmem          <int>   .D... max memory used for timestamp index (per stream)
-rtbufsize         <int>   .D... max memory used for buffering real-time frames
-fdebug            <flags> ED... print specific debug info
   ts                      ED...

SWScaler AVOptions:
-sws_flags         <flags> E.V.. scaler/cpu flags
   fast_bilinear           E.V.. fast bilinear
   bilinear                E.V.. bilinear
   bicubic                 E.V.. bicubic
   experimental            E.V.. experimental
   neighbor                E.V.. nearest neighbor
   area                    E.V.. averaging area
   bicublin                E.V.. luma bicubic, chroma bilinear
   gauss                   E.V.. gaussian
   sinc                    E.V.. sinc
   lanczos                 E.V.. lanczos
   spline                  E.V.. natural bicubic spline
   print_info              E.V.. print info
   accurate_rnd            E.V.. accurate rounding
   mmx                     E.V.. MMX SIMD acceleration
   mmx2                    E.V.. MMX2 SIMD acceleration
   3dnow                   E.V.. 3DNOW SIMD acceleration
   altivec                 E.V.. AltiVec SIMD acceleration
   bfin                    E.V.. Blackfin SIMD acceleration
   full_chroma_int         E.V.. full chroma interpolation
   full_chroma_inp         E.V.. full chroma input
   bitexact                E.V..

```
