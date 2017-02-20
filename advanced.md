# djangotube 시작하기

자 저희는 방금 `djangotube` 라는 이름을 가진 django 프로젝트를 생성했습니다.

처음에 django 프로젝트를 만들게 되면 다음과 같은 구조를 가집니다.

```
.
├── djangotube
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── manage.py
```

프로젝트만 만들고 지켜볼 수는 없겠죠? 한 번 실행시켜봅시다!

그 전에 먼저 다음 명령어를 통해 데이터베이스를 생성해주도록 합니다.

```
$ python manage.py migrate
```

자 이제 `db.sqlite3` 라는 데이터베이스 파일이 생겼습니다.

다음에는 정말 django 서버를 로컬에 띄워보도록 합시다.

다음 명령어를 통해 django 서버를 구동시킬 수 있습니다.

```
$ python manage.py runserver
```

위와 똑같이 명령어를 입력하게 된다면 `127.0.0.1:8000`  주소로 접속해서 작동하는 지를 확인할 수 있습니다.

![](/assets/스크린샷 2017-02-16 오후 6.45.38.png)

위와 같은 페이지가 뜬다면 성공하셨습니다. 축하드립니다 :\)

# 본격적인 코딩 시작하기

django 서버를 띄우는 데에 성공했으니 이제 기능을 구현해봅시다.

먼저 저희는 Youtube 에서 Video Key를 가져와서 제목과 함께 저장해놓으려고 합니다.

그러기 위해서는 django에 있는 Model이라는 개념이 필요합니다.

이 Model을 사용하기 위해서는 App 이라는 개념이 또 필요합니다.

백문이 불여일견. 한 번 App을 만들어볼까요?

App 추가는 다음 명령어로 가능합니다. 저는 video 라는 App을 만들어 보겠습니다.

```
$ django-admin startapp video
```

djangotube 폴더 안에서 다음과 같이 입력해주게 되면 프로젝트 구조는 다음과 같아집니다.

```
.
├── djangotube
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── manage.py
└── video
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── migrations
    │   └── __init__.py
    ├── models.py
    ├── tests.py
    └── views.py
```

이제 진짜진짜 본격적으로 코딩해봅시다.

# MTV\(MVC\)

MVC 패턴은 다른 웹 프레임워크에서 주로 사용되는 디자인 패턴입니다.

이 MVC는 Model, View, Controller 의 약자인데요, 이것을 django는 Model, **Template, View** 로 이름만 조금 다르게 사용합니다.

> 주의하실 점은 django에서의 View는 다른 MVC 에서의 View와 다르다는 점입니다.
>
> django 에서의 View는 MVC에서의 Controller 에 가깝고, Template이 MVC의 View 부분과 비슷합니다.

각각의 역할을 말씀드려보겠습니다.

* **Model** 은 데이터를 표현하는 데 사용되며, 하나의 Model 클래스는 데이터베이스에서 하나의 테이블로 표현됩니다.

* **View** 는 HTTP 요청를 받아 그 결과인 HTTP 응답를 반환하는 부분으로서, Model로부터 데이터를 읽거나 저장할 수 있으며, Template을 호출하여 데이터를 화면 상에 표현하도록 할 수 있다.

* **Template** 은 HTML을 생성하는 것을 목적으로 하는 부분입니다. 주로 템플릿 엔진을 이용해서 템플릿 문법을 사용합니다.

# Model

저희는 Video 라는 모델을 만들고 저장해서 리스트 형식으로 보여줄 것입니다.

그 전에 Django는 ORM 이라는 것으로 데이터베이스를 관리합니다.

그러기 위해선 Video Key와 제목을 저장하기 위한 `Video`모델을 만들어야 합니다.

`video/models.py` 에 다음과 같이 작성해줍니다.

```py
from django.db import models


class Video(models.Model):
    title = models.CharField(max_length=200)
    video_key = models.CharField(max_length=12)
```

먼저 Video의 제목을 저장하기 위한 **title **과  Video Key 를 저장할 수 있는 **video\_key**를 만들어줍니다.

title과 Video Key 모두 문자열 로 구성되어있기 때문에 character field 로 설정해줍니다.

이 변경사항들을 데이터베이스에게 알려주기 위해서는 **Migration** 이라는 작업이 필요합니다.

그러기 위해서는 아래의 명령어로 실행할 수 있습니다.

```
$ python manage.py makemigrations
$ python manage.py migrate
```

윗줄의 명령어를 입력하게 되면 django 에서 자동으로 Migration 파일을 만들어줍니다.

그 다음 만들어진 Migration 파일을 데이터베이스에 적용하는 작업은 아랫줄의 명령어로 가능합니다.

자, 벌써 모델 만들기가 끝났습니다!

이제 모델을 조작하기 위한 View와 Template을 만들어보겠습니다.

# View

django에서의 View는 각종 로직을 처리하는 곳입니다.

이렇게 말만 하면 어떤 것인지 감이 안오시죠?! 바로 만들어보겠습니다.

가장 먼저 저희가 하고 싶은 건 현재 저희가 만든 Video의 목록을 보고 싶은 것입니다.

그럼 `video/views.py` 에 작성해보겠습니다.

```py
from django.shortcuts import render, redirect
from django.core.urlresolvers import reverse
from .models import Video


def video_list(request):
    video_list = Video.objects.all()
    return render(request, 'video/video_list.html', {'video_list': video_list})

```

7번째 줄은 저장된 Video 객체들을 전부 가져오겠다는 뜻입니다.

저렇게 가져온 Video 들을 Python의 Dictionary\(사전\) 형태로 Template 쪽으로 넘겨주게 됩니다.

그렇게 되면 Template 쪽에서 ‘video\_list’ 라는 이름으로 video\_list 라는 리스트를 사용할 수 있게 되는 것입니다.

Template 쪽에서 좀 더 자세히 말씀 드리겠습니다.

하지만 정작 문제는 `video/video_list.html` 이라는 파일이 없다는 것이죠.

게다가 이 View를 어느 url에서 보여줄 지를 아직 설정하지 않았습니다.

해야할 게 많죠...

하지만 괜찮습니다. 곧 만들테니까요!

자 그럼 template 파일을 만들고 연결해봅시다!

# Urls

template 파일을 만들기 전에 View 와 template 파일을 연결해주기 위한 urls.py 를 작성해볼 것입니다.

urls.py 에는 어떤 URL에 어떤 View를 연결시켜줄 것인지를 작성합니다.

먼저 djangotube/urls.py 에는 다음과 같이 작성합니다.

```
from django.conf.urls import url, include
from django.contrib import admin

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^video/', include('video.urls', namespace='video')),
]
```

보시다시피 url을 이렇게 정의해줍니다.

namesapce 라는 개념은 직역하면 이름공간 이라는 뜻인데 관련있는 url 이름들을 한 곳에 묶고 싶을 때 사용합니다.

아래에서 마저 작성하고 사용법을 알아보도록 하겠습니다.

그리고 `video/urls.py` 에는 다음과 같이 작성합니다.

```
from django.conf.urls import url, include
from . import views

urlpatterns = [
    url(r'^$', views.video_list, name='list')
]
```

이렇게 작성해주시면 Template 쪽에서 video_list 라는 view로 링크를 걸어주고 싶다면 

```
<a href=“{% url ‘video:list’ %}”>링크</a>
```

와 같이 작성이 가능합니다.

이해가 되셨나요? 그렇다면 정말 대단하신 것입니다!

부가적인 설명을 드리자면 url 경로를 하나하나 다 외우기는 정말 어려운 일이니 이걸 간소화 하기 위해(쉽게 url을 찾기 위해) url 에 이름을 붙여주는 것입니다.

위에서 언급했던 namespace는 그 이름들을 관련 있는 것들끼리 묶어놓기 위해 쓰이는 것이구요.

어떠세요? 조금 이해가 가셨나요?

이해가 잘 안 되셨다면 따로 질문 해주세요! 성심성의껏 답변 해드리겠습니다.

# Template

Django는 django template 이라는 템플릿 엔진이라는 것을 통해서 html에 **특별한 구문** 을 작성할 수 있습니다.

역시나 한 번 `video/templates/video/video_list.html` 을 작성해봅시다!

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
        <h1><a href="{% url 'video:list' %}" style="float: left;">Video List</a></h1>
    </header>
    <div class="row">
        <div class="col-md-12">
            {% for video in video_list %}
                <h4>{{ video.title }}</h4>
            {% endfor %}
        </div>
    </div>
</div>
</body>
</html>
```

맨 첫 줄부터 낯설 겁니다.

일단 저희는 CSS Framework인 **Bootstrap** 을 사용합니다.

지금 튜토리얼에서는 크게 중요하지 않으니 그냥 복붙 하셔도 무방합니다.

하지만 중간에 나오는 `{% for video in video_list %}` 이 부분은 직접 쳐보시길 추천 드립니다.

그리고 위에서 잠깐 설명드렸던 `{% url ‘~~’ %}` 가 나옵니다.

이 부분은 **템플릿 태그** 라고 합니다.

템플릿 태그는 django의 정말 강력한 기능 중에 하나 입니다.

잘 사용하시면 정말 좋은 기능이므로 중요하게 보시는 걸 추천드립니다.

그리고 중간에 나오는 `{% for video in video_list %}` 이 부분은 템플릿 태그로 python의 `for .. in` 구문을 사용한 부분입니다.

`{% for ~~ %}` 로 시작했다면 반드시 `{% endfor %}` 로 닫아주어야 합니다.

이제 그 블록 안에 원하는 로직을 작성하면 됩니다.

저희는 일단 video의 제목이 리스트로 쭉 보여지게 하는 것이 목표입니다.

위의 view 에서 설명했던 video\_list라는 이름으로 video\_list를 넘겨줍니다.

video\_list는 Video의 배열이라고 생각하시면 편하실 듯 합니다.

그렇기 때문에 video\_list 를 for .. in 문으로 돌리게 되면 video 에는 Video 객체 하나하나가 들어가게 됩니다.

때문에 이 표현식 -&gt; \{\{  }} 을 사용해서 video.title 로 Video의 제목을 출력해주게 됩니다.

이렇게 작성해보고 한 번 실행시켜보도록 하겠습니다.

```
$ python manage.py runserver
```

를 입력한 후에 http://localhost:8000/video 로 들어가보겠습니다.

![](/assets/스크린샷 2017-02-20 오후 7.19.23.png)

아무것도 없습니다. 조금 허무할까요 ㅠㅠ...

그렇다면 이제 Video를 추가하는 페이지를 만들어 보겠습니다.

이제는 Model 을 건드릴 일은 없습니다.

Model을 추가할 수 있게 해주는 View 와 Template 을 만들어 봅시다!

다시 `video/views.py` 부터 작성해보겠습니다.

```python
# 아래에 이 코드 추가하기 

def video_new(request):
    if request.method == 'POST':
        title = request.POST['title']
        video_key = request.POST['video_key']
        Video.objects.create(title=title, video_key=video_key)
        return redirect(reverse('video:list'))

    return render(request, 'video/video_new.html')

```
이 코드는 HTTP 요청이 GET 방식일 경우와 POST 방식일 경우 의 응답이 서로 다릅니다.

먼저 GET 요청의 경우에는 `video/video_new.html` 을 렌더링 해줍니다.

그게 끝- 입니다.

다만 POST 방식 경우에는 조금의 처리가 더 들어갑니다.

POST 방식의 경우 첫 줄에 나오는 if 구문으로 분기를 합니다.

그 다음 `request.POST['title']` 과 `request.POST['video_key']` 라는 문법이 나옵니다.

이 부분은 POST 파라미터로 넘어온 title 이라는 키를 가진 값과 video_key 키를 가진 값을 꺼내오는 작업입니다.

이 부분은 template 부분을 보면서 좀 더 자세히 설명드리겠습니다.

그렇게 POST에서 꺼내온 값으로 `Video.objects.create` 구문을 이용해서 새로운 Video 객체를 만듭니다.

다음은 `video/urls.py` 의 코드입니다.

```python
from django.conf.urls import url, include
from . import views

urlpatterns = [
    url(r'^$', views.video_list, name='list'),
    # 아래 코드 추가하기
    url(r'^new$', views.video_new, name='new'),
]

```

요렇게 /video/new 경로로 들어가면 사용자에게 입력받을 수 있게끔 연결시켜줍니다.

다음은 `video/templates/video/video_new.html` 의 코드입니다.

```html
{% load staticfiles %}

<html>
<head>
    <title>New Video</title>
    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
</head>
<body>
<div class="content container">
    <header class="page-header">
        <h1>New Video</h1>
    </header>
    <div class="row">
        <div class="col-md-16">
            <form method="POST">
                {% csrf_token %}
                <div class="form-group">
                    <label for="title">Title</label>
                    <input type="text" name="title" class="form-control" id="title" placeholder="Title">
                </div>
                <div class="form-group">
                    <label for="video_key">Video Key</label>
                    <input type="text" name="video_key" class="form-control" id="video_key" placeholder="Video Key">
                </div>
                <button type="submit" class="btn btn-default">Submit</button>
            </form>
        </div>
    </div>
</div>
</body>
</html>
```

csrf token 설명
POST, GET 처리 방식 설명


