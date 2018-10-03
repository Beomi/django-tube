# 비디오 리스트 보여주기

## View (뷰) 추가하기

우리는 앞에서 유튜브 비디오를 저장하기 위해 `video` 라는 새로운 모델을 만들어줬습니다.

이제, 각 비디오를 보여주는 페이지와 전체 비디오의 목록을 보여주는 페이지를 만들어야겠군요.

Django에서 이러한 부분을 보여주도록 설계해주는게 바로 View입니다.

View는 어떻게 구성되어 있는지 볼까요?

`video` 폴더 안의 `views.py` 에 아래와 같이 코드를 써 주세요.

```py
# video/views.py
from django.shortcuts import render, redirect
from django.core.urlresolvers import reverse
from .models import Video
​
​
def video_list(request):
    video_list = Video.objects.all()
    return render(request, 'video/video_list.html', {'video_list': video_list})
```

`video_list`는 비디오 목록 데이터를 보여주도록 만든 합수입니다.

- 7번 째 줄: 앞서 추가한 `Video` 모델 구조로 된 정보를 전부 불러오겠다는 의미입니다. 즉, 전체 비디오의 목록을 불러오는거죠.

```py
video_list = Video.object.all()
```

- 8번 째 줄: 앞에서 받은 비디오 목록을 웹페이지로 넘겨 보여준다는 의미입니다.

```py
return render(request, 'video/video_list.html', {'video_list': video_list})
```

8번 째 줄, `render` 에 대해 추가 설명을 하자면, `Video` 목록을 받아 `{'video_list': video_list}` 와 같이 파이썬의 Dictionary(사전) 형태로 `video/video_list.html` 이라는 Template에 넘겨준다는 얘기입니다. 

그렇게 되면, `video/video_list.html` 에서 'video_list'를 불러올 수 있습니다. 이 부분은 Template 파트에서 좀 더 자세히 알려드릴게요.

위에 `views.py` 에서 작성한 코드는 아직 동작하지 않아요. 

아직 Template `video/video_list.html` 파일을 만들지 않았고,  View와  Template을  연결해주는 Url을 생성해줘야해요!

이제 Template과 Url을 만들어줍시다!

---

## Url 추가하기

Template 파일을 만들기 전에, View 와 template 파일을 연결해주는 `urls.py` 를 만들어 볼게요.

Url은 사이트의 경로에 따라 어떤 View를 보여줄 것인지 판별해줘요.

예를 들어, `https://www.naver.com/` 은 네이버의 기본 페이지를 불러와주고,

`https://www.naver.com/login/` 은 네이버의 로그인 페이지를 불러와주는거죠.

우리는 앞서 만든 비디오 목록을 가져와주는 View를 Url을 통해 Template에 연결해줄거에요.

먼저 `djangotube` 폴더 안의 `urls.py` 에 다음과 같이 코드를 적어주세요.

```py
# djangotube/urls.py
from django.conf.urls import url, include
from django.contrib import admin
​
urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^video/', include('video.urls', namespace='video')),
]
```

앞서 얘기한 것처럼 urls에서는 어떤 'Url'로 들어왔을 때 어떤 'View'를 보여줄 지에 대해 알려주는데, `urlpatterns` 이라는 리스트 안에 `url` 들을 적어준 것을 볼 수 있을거에요. `namesapce` 는 직역하면 이름공간 이라는 뜻인데 관련있는 url 이름들을 한 곳에 묶고 싶을 때 사용합니다. 아래에서 코드를 마저 작성하고 사용법을 알아볼게요.

우선 `video` 폴더안의 `urls.py` 라는 파일을 새로 만들어서 다음과 같이 코드를 적어주세요.

> `djangotube/urls.py` 와 `video/urls.py` 를 헷갈리지 않도록 주의하세요.

```py
# video/urls.py
from django.conf.urls import url, include
from . import views
​
urlpatterns = [
    url(r'^$', views.video_list, name='list')
]
```

이렇게 작성해주시면 Template 쪽에서 video_list 라는 view로 링크를 걸어주고 싶다면

```html
<a href=“{% url ‘video:list’ %}”>링크</a>
```

와 같이 HTML파일에서 URL​ 작성이 가능하답니다. 부가적인 설명을 드리자면, url 경로를 하나하나 다 외우기는 정말 어려운 일이니 이걸 간소화 하기 위해(쉽게 url을 찾기 위해) url 에 이름을 붙여주는 것입니다. 

위에서 `{% url ‘video:list’ %}` 에서  `video:list` 는 video 앱 안(namespace)의 list 라는 이름(name)을 가진 링크를 불러오겠다는 얘기에요.

위에서 언급했던 namespace는 그 이름들을 관련 있는 것들끼리 묶어놓기 위해 쓰이는 것이구요. 

어떠세요? 조금 이해가 가셨나요?

---

## Template (템플릿) 추가하기
Django는 `django template` 이라는 템플릿 엔진이라는 것을 통해서 html에 **특별한 구문** 을 작성할 수 있습니다.

역시나 한 번 `video/templates/video/video_list.html` 을 작성해봅시다!

> `video` 폴더 안에 `templates` 라는 폴더를 만드시고, 그 안에 `video` 폴더를 만드신 후 `video_list.html` 파일을 만드셔서 입력하시면 됩니다.

```html
{% load staticfiles %}
​
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

맨 첫 줄부터 당황스러울 수 있어요. 일단 저희는 CSS Framework인 **Bootstrap** 을 사용하는데요.

 지금 튜토리얼에서는 크게 중요하지 않으니 그냥 복붙 하셔도 무방합니다. 

하지만 중간에 나오는 `{% for video in video_list %}` 안쪽은 직접 쳐보시길 추천할게요.

그리고 위에서 잠깐 설명드렸던 `{% url '~~' %}` 가 나오는데, 이 부분을 **템플릿 태그**라고 부른답니다.

템플릿 태그는 Django의 정말 강력한 기능 중에 하나이고, 잘 사용하시면 정말 편리한 기능이기 때문에 잘 봐두시는 걸 추천드립니다.

그리고 중간에 나오는 `{% for video in video_list %}` 이 부분은 템플릿 태그로 python의 `for .. in` 구문을 사용한 부분입니다. `{% for ~~ %}` 로 시작했다면 반드시 `{% endfor %}` 로 for 블록을 닫아주어야 합니다.

이제 그 블록 안에 원하는 로직을 작성하면 됩니다. 저희는 일단 video의 제목이 리스트로 쭉 보여지게 하는 것이 목표입니다. 

위의 view 에서 설명했던 video_list라는 이름으로 video_list를 넘겨줍니다. 

video_list는 Video의 배열이라고 생각하시면 편하실거에요. 

그렇기 때문에 video_list 를 for .. in 문으로 돌리게 되면 video 에는 Video 데이터 객체 하나하나가 들어가게 됩니다. 

때문에 이 표현식 -> `{{` `}}` 을 사용해서 video.title 로 Video의 제목을 출력해주게 됩니다.

이렇게 작성해보고 한 번 실행시켜보도록 하겠습니다.

> 명령어 앞에 (myvenv) 즉 가상 환경이 떠 있는지 확인하세요!

```shell
(myvenv) $ python manage.py runserver
```

위의 명령어를 입력한 후에 http://localhost:8000/video 로 들어가보세요!

![](/assets/empty-video-list.png)


아무것도 없어요. 조금 허무한가요? 우리가 아직 아무 Video도 넣어주지 않아서 아무것도 뜨지 않는 것이랍니다.

그렇다면 이제 Video를 추가하러 가 볼게요! 고고!