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

# Urls



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

위에 코드 설명해야

다만 문제는 video/video\_list.html 이라는 파일이 없다는 것이죠.

게다가 이 View를 어느 url에서 보여줄 지를 아직 설정하지 않았습니다.

자 그럼 template 파일을 만들고 연결해봅시다!

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

위의 코드 설명해야함!

이렇게 간단하게 현재 만들어둔 Video를 볼 수 있는 화면을 만들어봤습니다.





