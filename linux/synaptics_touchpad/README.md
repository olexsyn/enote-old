# Настройка тачпада в Linux (Synaptics TouchPad)

https://mnorin.com/nastrojka-tachpada-v-linux.html

Настройка тачпада в Linux предполагает, что драйвер тачпада позволяет делать гораздо больше, чем с ним обычно делают. Например, можно включить или выключить скроллинг двумя пальцами (как вертикальный, так и горизонтальный), включить клик одним, двумя, тремя пальцами по тачпаду, изменить направление скроллинга (если вы, например, привыкли к скроллингу на планшете). Давайте посмотрим, как же можно тонко настроить тачпад, причем из командной строки.

## Условия

Прежде всего нужно обговорить, если вы упустили это в заголовке, что речь идет о настройке тачпадов, пожалуй, самого известного производителя — Synaptics. За поддержку тачпадов Synaptics в Debian GNU/Linux отвечает пакет xserver-xorg-input-synaptics. Соответственно, он должен быть установлен. Обычно он ставится по умолчанию, но проверить лишним не будет. Это можно сделать командой

    dpkg -l | grep xorg | grep synaptics

И, если такой пакет у вас не установлен, а тачпад Synaptics есть, то этот пакет надо будет поставить командой

    sudo apt-get install xserver-xorg-input-synaptics

В других дистрибутивах название пакета не отличается принципиально, в некоторых даже полностью совпадает.

## Программа synclient

Эта программа — основной инструмент тонкой настройки сенсорной панели (тачпада) Synaptics. Synclient использует интерфейс командной строки, формат команды следующий:

    synclient [-h] [-l] [-V] [-?] [var1=value1 [var2=value2] ...]

Как видите, длинных (GNU) опций нет, только короткие (Posix), и то совсем немного.

- **-h**, -**?** - Вывод справки
- **-V** - Вывод версии программы
- **-l** - Вывод всех используемых опций и их значений
- **var1=value1** - Задать опции с названием var1 ее новое значение value1. Программа может в одной строке принимать сразу много разных опций. После названия переменной перед знаком равенства и после знака равенства пробелов быть не должно

## Опции и их назначение

- **LeftEdge** - Координаты левой стороны тачпада
- **RightEdge** - Координаты правой стороны тачпада
- **TopEdge** - Координаты верхней стороны тачпада
- **BottomEdge** - Координаты нижней стороны тачпада
- **FingerLow** - Минимальная степень нажатия. Если давление становится ниже, чем указанное, считается, что произошло отпускание
- **FingerHigh** - Максимальная степень нажатия. Если давление стало выше указанного, значит произошло нажатие
- **MaxTapTime** - Таймаут, до истечения которого касание считается одиночным нажатием. После истечения интервала считается, что происходит удержание
- **MaxTapMove** - Максимальное движение пальца, допустимое при клике по тачпаду. Его значение отбрасывается и не считается перемещением.
- **MaxDoubleTapTime** - Аналогично MaxTapTime, но для двойного клика
- **SingleTapTimeout** - Когда вы делаете одно касание, в течение данного таймаута ожидается, что последует следующее касание. Если в течение указанного временного интервала повторное касание не произошло, считается, что произошло одно касание
- **ClickTime** - Продолжительность клика. То есть, длительность касания, интервал времени, в течение которого засчитывается клик, если вы в пределах этого интервала коснулись, а затем подняли палец
- **EmulateMidButtonTime** - Интервал времени, в течение которого обрабатывается нажатие на среднюю кнопку мыши, которое может быть настроено на нажатие одним, двумя или тремя пальцами
- **EmulateTwoFingerMinZ** - Минимальный уровень давление, который будет определен как касание двумя пальцами
- **EmulateTwoFingerMinW** - Минимальное расстояние между точками нажатия, которое будет определено как касание двумя пальцами
- **VertScrollDelta** - Расстояние, на которое надо передвинуть палец для вертикального скроллинга
- **HorizScrollDelta** - Расстояние, на которое надо передвинуть палец для горизонтального скроллинга
- **VertEdgeScroll** - Включить вертикальный скроллинг при проведении пальцем вдоль правого края тачпада (1 — включить, 0 — выключить)
- **HorizEdgeScroll** - Включить горизонтальный скроллинг при проведении пальцем вдоль верхнего края тачпада (1 — включить, 0 — выключить)
- **CornerCoasting** - Опция, которая используется при скроллинге проведением пальца вдоль правой стороны тачпада. Она определяет, использовать ли продолжение скроллинга после того, как палец дошел до правого нижнего угла.
- **VertTwoFingerScroll** - Включить вертикальный скроллинг двумя пальцами (1 — включить, 0 — выключить)
- **HorizTwoFingerScroll** - Включить горизонтальный скроллинг двумя пальцами (1 — включить, 0 -выключить)
- **MinSpeed** - Минимальная скорость движения курсора
- **MaxSpeed** - Максимальная скорость движения курсора. Если максимальная скорость равна минимальной, то ускорения движения курсора не будет
- **AccelFactor** - Коэффициент ускорения курсора. Чем он больше, тем быстрее скорость увеличивается с минимальной до максимальной
- **TouchpadOff** - Выключить тачпад (0 — тачпад включен, 1 — тачпад выключен, любые значения больше 1 — включено только перемещение курсора)
- **LockedDrags** - При перетаскивании касаниями (tap-and-drag), если эта опция выставлена в 1, отпускание кнопки мыши происходит только после дополнительного клика. Это позволяет отрывать палец от поверхности тачпада до окончания перетаскивания
- **LockedDragTimeout** - Опция, определяющая, по истечении какого временного интервала после отрывания пальца от тачпада автоматически закончить перетаскивание касаниями.
- **RTCornerButton** - Какую кнопку мыши эмулировать при нажатии на правый верхний угол тачпада (0 — отключено, 1 — левая кнопка, 2 — средняя кнопка, 3 — правая кнопка)
- **RBCornerButton** - Какую кнопку мыши эмулировать при нажатии на правый нижний угол тачпада (0 — отключено, 1 — левая кнопка, 2 — средняя кнопка, 3 — правая кнопка)
- **LTCornerButton** - Какую кнопку мыши эмулировать при нажатии на левый верхний угол тачпада (0 — отключено, 1 — левая кнопка, 2 — средняя кнопка, 3 — правая кнопка)
- **LBCornerButton** - Какую кнопку мыши эмулировать при нажатии на левый нижний угол тачпада (0 — отключено, 1 — левая кнопка, 2 — средняя кнопка, 3 — правая кнопка)
- **TapButton1** - Какую кнопку мыши эмулировать при касании одним пальцем не у края тачпада (0 — отключено, 1 — левая кнопка, 2 — средняя кнопка, 3 — правая кнопка)
- **TapButton2** - Какую кнопку мыши эмулировать при касании двумя пальцами не у края тачпада (0 — отключено, 1 — левая кнопка, 2 — средняя кнопка, 3 — правая кнопка)
- **TapButton3** - Какую кнопку мыши эмулировать при касании тремя пальцамине у края тачпада (0 — отключено, 1 — левая кнопка, 2 — средняя кнопка, 3 — правая кнопка)
- **ClickFinger1** - Какую кнопку мыши эмулировать при касании одним пальцем в левой стороне тачпада (0 — отключено, 1 — левая кнопка, 2 — средняя кнопка, 3 — правая кнопка)
- **ClickFinger2** - Какую кнопку мыши эмулировать при касании двумя пальцами в левой стороне тачпада (0 — отключено, 1 — левая кнопка, 2 — средняя кнопка, 3 — правая кнопка)
- **ClickFinger3** - Какую кнопку мыши эмулировать при касании тремя пальцами в левой стороне тачпада (0 — отключено, 1 — левая кнопка, 2 — средняя кнопка, 3 — правая кнопка)
- **CircularScrolling** - Интересная возможность — круговая прокрутка. Это работает следующим образом: вы делаете круговые движения по тачпаду, и таким образом заменяете прокрутку колесиком мыши. По часовой стрелке — прокрутка вниз, против часовой стрелки — прокрутка вверх. 0 — выключено, 1 — включено
- **CircScrollDelta** - Угол смещения пальца относительно центра тачпада при прохождении которого генерируется такое же системное событие, как при прокрутке колесика на одно деление
- **CircScrollTrigger** - Область тачпада, при начале движения по которой будет активироваться скроллинг при использовании круговой прокрутки.
  - 0 — любая сторона тачпада
  - 1 — верхняя сторона
  - 2 — верхний правый угол
  - 3 — правая сторона
  - 4 — правый нижний угол
  - 5 — нижняя сторона
  - 6 — нижний левый угол
  - 7 — левая сторона
  - 8 — левый верхний угол
- **CircularPad** - Если эта опция выставлена в 1, то область тачпада определяется не как прямоугольник, а как эллипс, вписанный в стороны тачпада
- **PalmDetect** - Определять нажатие ладонью. Эта опция полезна, когда вы печатаете на клавиатуре и случайно нажимаете частью ладони на тачпад. Если она включена, то при нажатии на большую площадь движение курсора будет выключено. 0 — выключено, 1 — включено
- **PalmMinWidth** - Минимальная ширина касания, при которой касание будет определено как касание ладонью.
- **PalmMinZ** - Минимальное давление, при котором будет определено касание ладонью
- **CoastingSpeed** - Скорость, с которой должны генерироваться события скроллинга, чтобы поддерживалось продолжение скроллинга при достижении пальцем стороны тачпада
- **CoastingFriction** - Количество событий скроллинга делёное на секунду в квадрате, на которые будет снижаться скорость скроллинга при достижении стороны тачпада
- **PressureMotionMinZ** - Минимальное давление пальца на тачпад, при котором будет происходить определение движения по тачпаду
- **PressureMotionMaxZ** - Максимальное давление на тачпад, при котором будет определяться движение пальцем по тачпаду
- **PressureMotionMinFactor** - Минимальный множитель усиления коэффициента давления при определении движения пальцем
- **PressureMotionMaxFactor** - Максимальный множитель усиления коэффициента давления при определении движения пальцем
- **GrabEventDevice** - Эта опция имеет смысл только при использовании событий устройств в ядре linux 2.6. При использовании других протоколов эта опция игнорируется. Если опция выставлена в 1, драйвер будет эксклюзивно захватывать устройство для обработки событий с него.
- **TapAndDragGesture** - Включить перетаскивание при помощи двойного касания (первое короткое, второе постоянное) аналогично перетаскиванию левой кнопкой мыши (0 — выключено, 1 — включено)
- **AreaLeftEdge** - Координата с левой стороны, любые движения и клики слева от которой
- **AreaRightEdge** - Включить (1) или выключить (0) область вдоль правой стороны тачпада
- **AreaTopEdge** - Включить (1) или выключить (0) область вдоль верхней стороны тачпада
- **AreaBottomEdge** - Включить (1) или выключить (0) область вдоль нижней стороны тачпада
- **HorizHysteresis** - Минимальное аппаратное расстояние по горизонтали, необходимое для генерации события движения. Может указываться в процентах
- **VertHysteresis** - Минимальное аппаратное расстояние по вертикали, необходимое для генерации события движения. Может указываться в процентах
- **ClickPad** - Является ли устройство клик-падом, то есть панелью без аппаратных кнопок

## Сохранение настроек

Для сохранения настроек тачпада придется вызывать команду synclient удобным для вас способом. Для этого можно сделать скрипт, который будет вызывать эту команду, и который будет запускаться при входе в учетную запись, например.

Вот как это сделать в LXDE. Создаем скрипт _**/home/user/bin/touchpad**_ следующего содержания:

```bash
#!/bin/bash
synclient TapButton1=1 TapButton2=3 TapButton3=2 PalmDetect=1

```
После этого создаем файл _**/home/user/.config/autostart/touchpad.desktop**_

```
[Desktop Entry]
Name=Touchpad
GenericName=Touchpad settings
Exec=/home/user/bin/touchpad
Terminal=false
Type=Application
StartupNotify=false

```

И при входе в систему настройки тачпада должны подгрузиться автоматически.