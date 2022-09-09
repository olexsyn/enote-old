## Мои опыты

Пример, когда подключаемый раздел FAT32:

`sudo mount /dev/sda4 /mnt/backup -t vfat -o rw,uid=olex,gid=olex,umask=133,dmask=022,noatime,nofail`

для него можно задать пользователя и разрешения файлов, которые поменять нельзя. При

- `umask=133,dmask=022` - файлы - 0644, директории - 0755
- `umask=111,dmask=000` - файлы - 0666, директории - 0777

Если подключаемый раздел EXT4 - он всегда будет от _root_, поэтому обычный пользователь linux вносить изменения не сможет.
Но можно создать директорию(-ии) от root'а, выполнить `chown user:user dirname` - и для пользователя _user_ не будет ограничений на запись.

### Мой fstab

```
UUID=e4f...a52    /       ext4   errors=remount-ro,noatime 0       1
UUID=37c...f7e    /home   ext4   defaults,noatime          0       2
UUID=b01...838    somedir ext4   noauto,noatime            0       2
UUID=f4c...3f1    none    swap   sw                        0       0
```
- <span class="ques">?</span> Не совсем понятно... Когда в **fstab** прописать точку монтирования `/media/somedir` - то linux (lite) показывает на рабочем столе непримонтированный диск.
А если просто `somedir` (как в верху), то диск после загрузки не отображается. При монтировании монтируется в корень `/somedir`.

{% include f.htm f="my_exp.md" %}
