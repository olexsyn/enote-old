# Більше одного відео YouTube на одній сторінці

```html
<div id="video0"></div>
<div id="video1"></div>
...
<div id="videoN"></div>
```

```javascript
var tag = document.createElement('script');
    tag.src = "https://www.youtube.com/iframe_api";
    var firstScriptTag = document.getElementsByTagName('script')[0];
    firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
    var player = [];
    function onYouTubeIframeAPIReady() {
            player[0] = new YT.Player('video0', {
                width: '100%',
                height: '679',
                videoId: 'youtube_id_video0',
            });
            player[1] = new YT.Player('video1', {
                width: '640',
                height: '360',
                videoId: 'youtube_id_video1',
            });

            ...

            player[N] = new YT.Player('videoN', {
                width: '640',
                height: '360',
                videoId: 'youtube_id_videoN',
            });

}
```
