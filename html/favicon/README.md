# favicon для браузеров и устройств

Обычное использование:

```html
<link rel="shortcut icon" href="/favicon.ico" />
<link rel="icon" href="/favicon.ico" sizes="16x16 32x32" />
```
## Links

- <span class="warn">!</span> [realfavicongenerator.net](https://realfavicongenerator.net/) - free service
- <span class="warn">!</span> [Добавление иконок для сайта в мультибраузерном и мультипплатформенном мире](https://webformyself.com/dobavlenie-ikonok-dlya-sajta-v-multibrauzernom-i-multipplatformennom-mire/)
- [видео: Какие нужны фавиконки](https://www.youtube.com/watch?v=iG9WF8VpogY)
- [Favicon сегодня: форматы, поддержка, автоматизация](https://habr.com/ru/post/330584/) 2017
- <https://github.com/audreyr/favicon-cheat-sheet>
- см. [Everything you always wanted to know about touch icons](https://mathiasbynens.be/notes/touch-icons)
- [App Icons on iPad and iPhone](https://developer.apple.com/library/ios/qa/qa1686/_index.html)
- <http://www.favicomatic.com> - беспл. сервис
- [Real FavIcon Generator](http://realfavicongenerator.net/blog/apple-touch-icon-the-good-the-bad-the-ugly/)


<span class="warn">TODO!</span> наведи тут порядок


## Примеры

### мой вариант

сработал и для Opera Mobile

```html
<link rel="shortcut icon" href="/favicon.ico" />
<link rel="shortcut icon"    sizes="32x32"   href="/img/s_logo_032.png" />
<link rel="shortcut icon"    sizes="64x64"   href="/img/s_logo_064.png" />
<link rel="shortcut icon"    sizes="114x114" href="/img/s_logo_114.png" />
<link rel="shortcut icon"    sizes="142x142" href="/img/s_logo_142.png" />
<link rel="apple-touch-icon" sizes="32x32"   href="/img/s_logo_032.png" />
<link rel="apple-touch-icon" sizes="64x64"   href="/img/s_logo_064.png" />
<link rel="apple-touch-icon" sizes="114x114" href="/img/s_logo_114.png" />
<link rel="apple-touch-icon" sizes="142x142" href="/img/s_logo_142.png" />
```

### bootstrap

```html

<link rel="apple-touch-icon" href="/img/favicons/apple-touch-icon.png" sizes="180x180">
<link rel="icon" href="/img/favicons/favicon-32x32.png" sizes="32x32" type="image/png">
<link rel="icon" href="/img/favicons/favicon-16x16.png" sizes="16x16" type="image/png">
<link rel="manifest" href="/img/favicons/manifest.json">
<link rel="mask-icon" href="/img/favicons/safari-pinned-tab.svg" color="#563d7c">
<link rel="icon" href="/img/favicons/favicon.ico">
<meta name="msapplication-config" content="/img/favicons/browserconfig.xml">
<meta name="theme-color" content="#563d7c">
```

### gismeteo

```html
<meta property="og:image" content="http://habr.com/i/habralogo.jpg" />
<link rel="image_src"        href="http://habr.com/i/habralogo.jpg" />
<link rel='apple-touch-icon' type='image/png' href='/images/apple-touch-icon_142x142.png' >

<meta itemprop="image" content="http://s1.gismeteo.ua/static/app/logo_ua.jpg" />
<link rel="shortcut icon" type="image/ico" href="http://s1.gismeteo.ua/favicon2.ico" />
<link rel="icon" type="image/ico" href="http://s1.gismeteo.ua/favicon2.ico" />
<link rel="apple-touch-icon" href='http://s1.gismeteo.ua/static/v5/images/favicons/ios/default_icon_60x60.png'>
<link rel="apple-touch-icon" sizes="57x57" href='http://s2.gismeteo.ua/static/v5/images/favicons/ios/icon_57.png'>
<link rel="apple-touch-icon" sizes="72x72" href='http://s1.gismeteo.ua/static/v5/images/favicons/ios/icon_72.png'>
<link rel="apple-touch-icon" sizes="76x76" href='http://s2.gismeteo.ua/static/v5/images/favicons/ios/icon_76.png'>
<link rel="apple-touch-icon" sizes="114x114" href='http://s2.gismeteo.ua/static/v5/images/favicons/ios/icon_114.png'>
<link rel="apple-touch-icon" sizes="120x120" href='http://s1.gismeteo.ua/static/v5/images/favicons/ios/icon_120.png'>
<link rel="apple-touch-icon" sizes="144x144" href='http://s2.gismeteo.ua/static/v5/images/favicons/ios/icon_144.png'>
<link rel="apple-touch-icon" sizes="152x152" href='http://s2.gismeteo.ua/static/v5/images/favicons/ios/icon_152.png'>
<link rel="shortcut icon" sizes="196x196" href='http://s1.gismeteo.ua/static/v5/images/favicons/android/default-highres-icon.png'>
<link rel="shortcut icon" sizes="128x128"  href='http://s1.gismeteo.ua/static/v5/images/favicons/android/icon_128.png'>
<link rel="shortcut icon" sizes="96x96"  href='http://s2.gismeteo.ua/static/v5/images/favicons/android/icon_for_xhdpi.png'>
<link rel="shortcut icon" sizes="72x72"  href='http://s2.gismeteo.ua/static/v5/images/favicons/android/icon_for_hdpi.png'>
<link rel="shortcut icon" sizes="48x48"  href='http://s2.gismeteo.ua/static/v5/images/favicons/android/icon_for_mdpi.png'>

<link href="//abs.twimg.com/favicons/favicon.ico" rel="shortcut icon" type="image/x-icon">

<link rel="shortcut icon" href="http://ans.kiev.ua/wiki/lib/tpl/dokuwiki/images/favicon.ico" />
<link rel="apple-touch-icon" href="http://ans.kiev.ua/wiki/lib/tpl/dokuwiki/images/apple-touch-icon.png" />  (114-114)

<link rel="shortcut icon" href="https://fbstatic-a.akamaihd.net/rsrc.php/yl/r/H3nktOa7ZMg.ico" />
```

### Хабр

```html
<link rel="apple-touch-icon" sizes="180x180" href="/images/apple-touch-icon.png">
<link rel="icon" type="image/png" sizes="32x32" href="/images/favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="/images/favicon-16x16.png">
<link rel="manifest" href="/site.webmanifest">
<link rel="mask-icon" href="/images/safari-pinned-tab.svg" color="#77a2b6">
<meta name="application-name" content="Хабр"/>
<meta name="msapplication-TileColor" content="#77a2b6">
<meta name="theme-color" content="#77a2b6">
```

В т.ч. присутствует иконка в корне https://habr.com/favicon.ico

```
/favicon.ico
/images/favicon-16x16.png
/images/favicon-32x32.png
/images/apple-touch-icon.png
/images/android-chrome-192x192.png
/images/android-chrome-256x256.png
/images/safari-pinned-tab.svg
```

**site.webmanifest** <span class="ques">?</span>

```xml
{
    "name": "Habr",
    "short_name": "Habr",
    "icons": [
        {
            "src": "/images/android-chrome-192x192.png",
            "sizes": "192x192",
            "type": "image/png"
        },
        {
            "src": "/images/android-chrome-256x256.png",
            "sizes": "256x256",
            "type": "image/png"
        }
    ],
    "theme_color": "#77a2b6",
    "background_color": "#77a2b6",
    "display": "standalone"
}
```

### TicTick

https://ticktick.com

```html
<!doctype html>
<!--[if lt IE 7 ]> <html lang="en" class="ie6"> <![endif]-->
<!--[if IE 7 ]>    <html lang="en" class="ie7"> <![endif]-->
<!--[if IE 8 ]>    <html lang="en" class="ie8"> <![endif]-->
<!--[if IE 9 ]>    <html lang="en" class="ie9"> <![endif]-->
<!--[if (gt IE 9)|!(IE)]><!--> <html lang="en"> <!--<![endif]-->
<head>

<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
<meta name="renderer" content="webkit">
<meta http-equiv="Cache-Control" content="no-siteapp" />
<meta name="viewport" content="width=device-width , initial-scale=1.0, minimum-scale=0.5, maximum-scale=1.5,user-scalable=yes">
  <meta name="keywords" content="TickTick,todo,gtd,to do,list,task manager,checklist,share,tasks,note,notes,android,app,iphone,ipad,ios,">
<meta name="description" content="TickTickis a cross-platform to-do list app & task manager helps you to get all things done and make life well organized.">
<meta name="author" content="TickTick">
<meta name="robots" content="index,follow">
<meta property="qc:admins" content="24614436777641413656375" />
<meta name="apple-mobile-web-app-capable" content="yes" />
<meta name="apple-mobile-web-app-title" content="TickTick">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
<meta name="apple-itunes-app" content="app-id=626144601">
<link rel="shortcut icon" href="//d3qg9zffrnl4ph.cloudfront.net/static/img/favicon.ico">
<link rel="apple-touch-icon" sizes="72x72" href="//d3qg9zffrnl4ph.cloudfront.net/static/img/touch-icon-ipad.png" />
<link rel="apple-touch-icon" sizes="114x114" href="//d3qg9zffrnl4ph.cloudfront.net/static/img/touch-icon-iphone-retina.png" />
<link rel="apple-touch-icon" sizes="144x144" href="//d3qg9zffrnl4ph.cloudfront.net/static/img/touch-icon-ipad-retina.png" />
<link rel="apple-touch-icon" href="//d3qg9zffrnl4ph.cloudfront.net/static/img/touch-icon-iphone.png" />
<!-- Android Lollipop -->
<meta name="theme-color" content="#5f7fb0">
<!-- win8 -->
<meta name="msapplication-TileColor" content="#5f7fb0"/>
<meta name="msapplication-tap-highlight" content="no">
<meta name="msapplication-config" content="none"/>
<!-- old mobile -->
<meta name="HandheldFriendly" content="true">
<meta name="MobileOptimized" content="320">
<!-- uc -->
<meta name="screen-orientation" content="portrait">
<meta name="full-screen" content="yes">
<meta name="browsermode" content="application">
<!-- QQ -->
<meta name="x5-orientation" content="portrait">
<meta name="x5-fullscreen" content="true">
<meta name="x5-page-mode" content="app">
    <title>TickTick</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
      <link rel="stylesheet" href="//d3qg9zffrnl4ph.cloudfront.net/static/build/app/core/webapp.836a083dc95e62ae1f974b5455d908d3.css" type="text/css" media="screen" />

<style>
  .icon_home {
          background-image: url("//d3qg9zffrnl4ph.cloudfront.net/static/build/app/core/app-icons.668cc4be50fb908a5925cdcf136bab7a.png");
      }

  @media
    (min--moz-device-pixel-ratio: 1.5),
    (-o-min-device-pixel-ratio: 3/2),
    (-webkit-min-device-pixel-ratio: 1.5),
    (min-device-pixel-ratio: 1.5),
    (min-resolution: 1.5dppx) {
    .icon_home {
              background-image: url("//d3qg9zffrnl4ph.cloudfront.net/static/build/app/core/app-icons@2.7c6adbef3c7a1e9bfd9f99c3659e9113.png");
          }
  }
</style>
```
