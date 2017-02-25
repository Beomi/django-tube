# 비디오 리스트 보여주기

## View \(뷰\) 추가하기

django에서의 View는 각종 로직을 처리하는 곳입니다.
이렇게 말하면 어떤 것인지 감이 안오시죠? 바로 만들어 볼게요.
가장 먼저, 우리가 만든 Video의 목록을 보고 싶어요!

`video`폴더 안의 `views.py`에 아래와 같이 코드를 써 주세요.

```python
# video/views.py
from django.shortcuts import render, redirect
from django.core.urlresolvers import reverse
from .models import Video


def video_list(request):
    video_list = Video.objects.all()
    return render(request, 'video/video_list.html', {'video_list': video_list})
```

7번째 줄, 즉 아래 부분은 저장된 Video 객체들을 전부 가져오겠다는 뜻입니다

```
video_list = Video.objects.all()
```

저렇게 가져온 Video 들을 Python의 Dictionary\(사전\) 형태로 Template 쪽으로 넘겨주게 됩니다.
그렇게 되면 Template 쪽에서 ‘video\_list’ 라는 이름으로 해당 리스트를 사용할 수 있습니다.
이 부분은 Template 파트에서 좀 더 자세히 알려드릴게요.
하지만 이 코드는 바로 동작하지는 않아요.
왜냐하면, 바로 `video/video_list.html` 파일이 없기 때문이죠.
게다가 이 View를 어떤 url에서 보여줄 지도 아직 설정하지 않았구요.
해야할 게 많죠! 하지만 괜찮아요. 곧 만들테니까요!

자 그럼 template 파일을 만들고 연결해볼게요!

## Url 추가하기

template 파일을 만들기 전에, View 와 template 파일을 연결해주는 `urls.py`를 만들어 볼게요. urls.py 에는 어떤 URL에 어떤 View를 연결시켜줄 것인지를 알려주는 것입니다.

먼저 `djangotube`폴더 안의 `urls.py`에 다음과 같이 코드를 적어주세요.

```python
# djangotube/urls.py
from django.conf.urls import url, include
from django.contrib import admin

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^video/', include('video.urls', namespace='video')),
]
```

urls에서는 '어떤 URL'로 들어올 때 '어떤 View'를 보여줄 지를 알려주는데, `urlpatterns`이라는 리스트 안에 `url`들을 적어준 것을 볼 수 있을거에요.
`namesapce`는 직역하면 이름공간 이라는 뜻인데 관련있는 url 이름들을 한 곳에 묶고 싶을 때 사용합니다. 아래에서 코드를 마저 작성하고 사용법을 알아볼게요.

우선 `video`폴더안의 `urls.py` 라는 파일을 새로 만들어서 다음과 같이 코드를 적어주세요.

> `djangotube/urls.py`와 `video/urls.py`를 헷갈리지 않도록 주의하세요.

```python
# video/urls.py
from django.conf.urls import url, include
from . import views

urlpatterns = [
    url(r'^$', views.video_list, name='list')
]
```

이렇게 작성해주시면 Template 쪽에서 video\_list 라는 view로 링크를 걸어주고 싶다면

```html
<a href=“{% url ‘video:list’ %}”>링크</a>
```

와 같이 HTML파일에서 URL​ 작성이 가능하답니다.
부가적인 설명을 드리자면, url 경로를 하나하나 다 외우기는 정말 어려운 일이니 이걸 간소화 하기 위해\(쉽게 url을 찾기 위해\) url 에 이름을 붙여주는 것입니다.
위에서 언급했던 namespace는 그 이름들을 관련 있는 것들끼리 묶어놓기 위해 쓰이는 것이구요.
어떠세요? 조금 이해가 가셨나요?

## Template \(템플릿\) 추가하기

Django는 `django template`이라는 템플릿 엔진이라는 것을 통해서 html에 **특별한 구문** 을 작성할 수 있습니다.

역시나 한 번 `video/templates/video/video_list.html` 을 작성해봅시다!

> `video`폴더 안에 `templates`라는 폴더를 만드시고, 그 안에 `video`폴더를 만드신 후 `video_list.html`파일을 만드셔서 입력하시면 됩니다.

```html
{% load staticfiles %}

<html>
<head>
    <title>Video List</title>
    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
</head>
<body>
<div class="content container">
    <header class="page-header" style="overflow: auto;">
        <h1 style="display: inline;">Video List</h1>
        <a class="btn btn-default" href="/video/new" style="float: right;">New Video</a>
    </header>
    <div class="row">
        <div class="col-md-12">
            {% for video in video_list %}
                <a href="/video/{{ video.id }}">
                    <h4>{{ video.title }}</h4>
                </a>
            {% endfor %}
        </div>
    </div>
</div>
</body>
</html>
```

맨 첫 줄부터 당황스러울 수 있어요.
일단 저희는 CSS Framework인 **Bootstrap** 을 사용하는데요, 지금 튜토리얼에서는 크게 중요하지 않으니 그냥 복붙 하셔도 무방합니다.
하지만 중간에 나오는 `{% for video in video_list %}` 안쪽은 직접 쳐보시길 추천할게요.
그리고 위에서 잠깐 설명드렸던 `{% url ‘~~’ %}` 가 나오는데, 이 부분을 **템플릿 태그** 라고 부른답니다.
템플릿 태그는 django의 정말 강력한 기능 중에 하나이고, 잘 사용하시면 정말 편리한 기능이기 때문에 잘 봐두시는 걸 추천드립니다.
그리고 중간에 나오는 `{% for video in video_list %}` 이 부분은 템플릿 태그로 python의 `for .. in`구문을 사용한 부분입니다.
`{% for ~~ %}`로 시작했다면 반드시 `{% endfor %}`로 for 블록을 닫아주어야 합니다.

이제 그 블록 안에 원하는 로직을 작성하면 됩니다.
저희는 일단 video의 제목이 리스트로 쭉 보여지게 하는 것이 목표입니다.
위의 view 에서 설명했던 video\_list라는 이름으로 video\_list를 넘겨줍니다.
video\_list는 Video의 배열이라고 생각하시면 편하실거에요.
그렇기 때문에 video\_list 를 for .. in 문으로 돌리게 되면 video 에는 Video 데이터 객체 하나하나가 들어가게 됩니다.
때문에 이 표현식 -&gt; `{{`  `}}` 을 사용해서 video.title 로 Video의 제목을 출력해주게 됩니다.

이렇게 작성해보고 한 번 실행시켜보도록 하겠습니다.

> 명령어 앞에 \(myvenv\) 즉 가상 환경이 떠 있는지 확인하세요!

```
(myvenv) $ python manage.py runserver
```

위의 명령어를 입력한 후에 [http://localhost:8000/video](http://localhost:8000/video)로 들어가보세요! 

![](/assets/empty-video-list.png)

아무것도 없어요. 조금 허무한가요? 우리가 아직 아무 Video도 넣어주지 않아서 아무것도 뜨지 않는 것이랍니다. 

그렇다면 이제 Video를 추가하러 가 볼게요! 고고!

