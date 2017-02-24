# 상세 비디오 페이지 만들기

## View 추가하기

먼저 `video`폴더 안의 `views.py`에 코드를 추가해 볼게요.

```python
# video/views.py
# 기존 코드 아래에 다음 코드를 작성해주세요

def video_detail(request, video_id):
    video = Video.objects.get(id=video_id)
    return render(request, 'video/video_detail.html', {'video': video})

```

이 코드의 의미는 `video_id` 라는 이름을 가진 값을 인자로 받아, 그 값을 `id`로 가지는 Video 데이터를 불러와주는 것이랍니다.

## Url 추가하기

이 `video_url` 은 `urls.py` 에서 넘어옵니다. 그럼 `video`폴더 안의 `urls.py`에도 추가해 볼게요.

```python
# video/urls.py
from django.conf.urls import url, include
from . import views

urlpatterns = [
    url(r'^$', views.video_list, name='list'),
    url(r'^new$', views.video_new, name='new'),
    # 이 코드를 추가해 주세요
    url(r'^(?P<video_id>\d+)/$', views.video_detail, name='detail'),
]
```

이렇게 작성해주시면 됩니다.

> 역시 url 끝에 콤마(,) 찍는 것 잊지마세요!

맨 아래에서 두 번째 줄이 추가가 되었는데, 이 부분의 의미는 video_id 라는 숫자로 이루어진 값을 받아서 `video_detail` 라는 뷰에 인자로 넘겨주겠다는 의미랍니다.

따라서 우리는 `video_detail` 함수에서 `video_id` 라는 인자를 받아서 사용했어요.

## Template 추가하기

그럼 이제 `video/views.py` 에서 지정했던 `video/templates/video/video_detail.html` 파일을 만들어볼게요.

> 새로 파일을 만들어주세요! 폴더 위치를 잘 확인하세요!

```html
{% load staticfiles %}

<html>
<head>
    <title>Video Detail</title>
    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
</head>
<body>
<div class="content container">
    <header class="page-header">
        <h1>Video Detail</h1>
    </header>
    <div class="row">
        <div class="col-md-16">
            <div id="player"></div>
        </div>
    </div>
</div>
</body>
<script>
    var tag = document.createElement('script');

    tag.src = "https://www.youtube.com/iframe_api";
    var firstScriptTag = document.getElementsByTagName('script')[0];
    firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);

    var player;
    function onYouTubeIframeAPIReady() {
        player = new YT.Player('player', {
            videoId: '{{ video.video_key }}'
        });
    }
</script>
</html>
```

이렇게 작성해 보세요.

우선, 아래쪽의 script 태그쪽은 Youtube Player를 부르기 위해서 작성해놓은 API 부분입니다.

그 부분은 django에 관한 내용은 아니니 지금은 넘어갈게요. 최대한 django 부분에 집중 해보겠습니다.

script 태그쪽에서 `video.video_key` 라는 부분을 보실 수 있을거에요.

이 부분은 저희가 `New Video` 페이지에서 입력했던 것을 Youtube API를 통해서 넘겨주는 부분입니다.

Youtube API는 그 Key를 가지고 저희가 원했던 동영상을 가져와줍니다.

그 가져온 동영상을 id가 `player` 인 div 태그에 렌더링 해주게 됩니다.

따라서 원하는 페이지를 볼 수 있게 됩니다!

아래 사진처럼요.

![](/assets/video-detail.png)

와! 모든 과정을 마치셨어요!

비록 짧은 시간이었지만 django의 기초가 되는 내용을 훑어보는 시간을 가졌어요.

시간이 짧아서 `배포` 부분이나 좀 더 다양한 내용을 다루지는 못했으나 더 배우시고 싶으시면 [장고걸스 튜토리얼](https://djangogirlsseoul.gitbooks.io/tutorial/content/) 을 찾아주세요!
