# Template \(템플릿\)

Django는 `django template`이라는 템플릿 엔진이라는 것을 통해서 html에 **특별한 구문** 을 작성할 수 있습니다.

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
        <h1>Video List</h1>
        <a class="btn btn-default" href="/video/new" style="float: right;">New Video</a>
    </header>
    <div class="row">
        <div class="col-md-12">
            {% for video in video_list %}
                <a href="{% url 'video:detail' video.id %}">
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

> 명령어 앞에 \(myvenv\)가 떠 있는지 확인하세요!

```
(myvenv) $ python manage.py runserver
```

를 입력한 후에 [http://localhost:8000/video](http://localhost:8000/video)로 들어가보세요.

![](/assets/empty-video-list.png)

아무것도 없습니다. 조금 허무한가요?

우리가 아직 아무 Video도 넣어주지 않아서 아무것도 뜨지 않는 것이랍니다.

그렇다면 이제 Video를 추가하는 페이지를 만들어 볼게요.

이제 Model 을 건드릴 일은 없어요.

다만, Model에 데이터를 추가할 수 있게 해주는 View 와 Template를 만들어 볼게요!

다시 `video`폴더 안의 `views.py`부터 코드를 작성해 봐요.

```python
# video/views.py
# 기존 코드(video_list) 아래에 이 코드를 추가해주세요

def video_new(request):
    if request.method == 'POST':
        title = request.POST['title']
        video_key = request.POST['video_key']
        Video.objects.create(title=title, video_key=video_key)
        return redirect(reverse('video:list'))
    elif request.method == 'GET':
        return render(request, 'video/video_new.html')
```

이 코드는 HTTP 요청이 GET 방식일 경우와 POST 방식일 경우 의 응답이 서로 다릅니다.

먼저 GET 요청의 경우에는 `video/video_new.html` 을 보여줍니다.

이게 전부랍니다.

다만 POST 방식 경우에는 조금 더 처리를 해주는데요,

POST 방식의 경우 첫 줄에 나오는 if 구문으로 분기를 합니다.

그 다음 `request.POST['title']` 과 `request.POST['video_key']` 라는 문법이 나옵니다.

이 부분은 POST 파라미터로 넘어온 title 이라는 키를 가진 값과 video\_key 키를 가진 값을 꺼내오는 작업입니다.

이 부분은 template 부분을 보면서 좀 더 자세히 설명해 드릴게요.

그렇게 POST에서 꺼내온 값으로 `Video.objects.create` 구문을 이용해서 새로운 Video 객체를 만듭니다.

다음은 `video`폴더 안의 `urls.py`파일의 코드입니다.

```python
# video/urls.py
from django.conf.urls import url, include
from . import views

urlpatterns = [
    url(r'^$', views.video_list, name='list'),
    # 아래 코드 추가하기
    url(r'^new$', views.video_new, name='new'),
]
```

이렇게 `/video/new` 경로로 들어가면 사용자에게 입력받을 수 있게끔 연결시켜줍니다.

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

일단 이 template 파일에서 가장 낯선 부분은 아마도 `{% csrf_token %}` 부분일 거에요.

이 템플릿 태그는 특별한 템플릿 태그인데요, 웹사이트 공격기법으로 `Cross-Site Request Forgery(CSRF)`라는 것이 있는데 이 공격을 장고가 기본적으로 막아주는 것이랍니다.

`form` 태그 안에는 꼭 써주셔야만 합니다. \(만약 `csrf_token`을 잊으신다면 장고가 경고를 띄울거에요!\)

이제 form 태그 쪽을 보게되면, method를 POST로 지정하고 input을 2개 받는 걸 볼 수 있어요.

input 태그는 name 값을 잘 봐야 하는데요,

django의 view 쪽에서 input 안에 있는 값을 받게 되는데 그 값을 가져올 때 저 `name` 값을 통해서 가져오기 때문입니다.

위에 `video/views.py` 에서 저희가 `request.POST['title']` 과 `request.POST['video_key']` 로 작성했으므로 input 태그의 name 속성도 이에 맞춰서 작성해 주세요.

다 작성되었다면 다시한번 장고 서버를 실행해 보세요!

> 잊지 않으셨죠? 장고 서버는 `python manage.py runserver`명령어로 띄울 수 있답니다!

![](/assets/void-new-video.png)

잘 보이네요!

![](/assets/fill-input-new-video.png)

이제 값을 입력하고 Submit 버튼을 눌러봅시다.

![](/assets/complete-video-list.png)

다음과 같이 생성되는 것을 볼 수 있어요.

하지만 뭔가 허전하죠?

Video의 제목을 클릭하면 그 비디오의 상세 페이지로 가고, 상세 페이지에서는 우리가 저장한 영상이 나오게끔 만들어 볼게요.

먼저 `video`폴더 안의 `views.py`에 코드를 추가해 볼게요.

```python
# video/views.py
# 기존 코드 아래에 다음 코드를 작성해주세요

def video_detail(request, video_id):
    video = Video.objects.get(id=video_id)
    return render(request, 'video/video_detail.html', {'video': video})
```

이 코드의 의미는 `video_id` 라는 이름을 가진 값을 인자로 받아, 그 값을 `id`로 가지는 Video 데이터를 불러와주는 것이랍니다.

이 `video_url` 은 `urls.py` 에서 넘어옵니다. 그럼 `video/urls.py` 도 작성해봅시다.

```python
from django.conf.urls import url, include
from . import views

urlpatterns = [
    url(r'^$', views.video_list, name='list'),
    url(r'^new$', views.video_new, name='new'),
    url(r'^(?P<video_id>\d+)/$', views.video_detail, name='detail'),
]
```

이렇게 작성해주시면 됩니다.

맨 아래에서 두 번째 줄이 추가가 되었는데, 이 부분의 의미는 video\_id 라는 숫자로 이루어진 값을 받아서 `video_detail` 라는 뷰에 인자로 넘겨주겠다는 의미입니다.

따라서 우리는 `video_detail` 함수에서 `video_id` 라는 인자를 받아서 사용했어요.

그럼 이제 `video/views.py` 에서 작성했었던 `video/templates/video_detail.html` 을 수정해볼게요.

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

