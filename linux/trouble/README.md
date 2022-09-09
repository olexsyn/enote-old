## Проблемы

- [Failed to start casper-md5check Verify Live ISO checksums](casper-md5check)
- ![+][pl] [Scanning for BTRFS file system](scanning4btrfs) - остановка ~15с во время загрузки
- ![+][pl] Reverce scroll direction (Natural Scrolling)

[bug](https://bugzilla.xfce.org/show_bug.cgi?id=11193)

Отключить Reverce scroll direction в настройках touchpad! Потом это:

<https://askubuntu.com/questions/690512/how-to-enable-natural-scrolling-in-xfce4>

I searched a lot and also found a bugreport about it, but the solution was easy:

You have to select the Touchpad-device in the selectbox at the top of the mouse-settings.

(It was a bit hard, to find, because I didn't expect that the settings for mouse and touchpad are separately configureable.)

On older xfce versions, where the setting doesn't exist, check the value with

    synclient | grep VertScrollDelta

and use the negative value, you find there (for example -58 instead of 58).

The best method that have worked for me to make this reboot-safe is to add your changes into Xsession.d, so it will load automatically for all users when you log into X:

(the file doesn't exists, so you can name it whatever you want. The numbers on the left means the order in which it will be executed in comparison with the other files.)

    sudo nano /etc/X11/Xsession.d/80synaptics

Add just the synclient commands in that file:

    synclient VertScrollDelta=-58
    synclient HorizScrollDelta=-58

(should be owned by root, with permissions 644)

    chmod 644 /etc/X11/Xsession.d/80synaptics

There is still something odd: the horizontal scrolling is still wrong, This can be fixed with:

    echo 'pointer = 1 2 3 4 5 7 6 8 9 10 11 12' >> .Xmodmap
    xmodmap .Xmodmap

<span class="ques">WTF?</span>

Еще много написано здесь: <https://askubuntu.com/questions/91426/reverse-two-finger-scroll-direction-natural-scrolling>


[pl]: /i/pl.png
