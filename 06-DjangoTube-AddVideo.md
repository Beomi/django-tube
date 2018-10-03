# 비디오 추가 페이지 만들기

이제 Model 을 건드릴 일은 없어요. 다만, Model에 데이터를 추가할 수 있게 해주는 View 와 Template를 만들어 볼게요!

## View 추가하기

다시 `video` 폴더 안의 `views.py` 부터 코드를 작성해 봐요.

```py
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

이 코드는 HTTP 요청이 **GET** 방식일 경우와 **POST** 방식일 경우 의 응답이 서로 다릅니다.

- GET: Url을 통해 페이지를 받아올 때 실행됩니다. **Ex) 비디오 목록 조회**

- POST: Url을 통해 정보를 보낼 때 실행됩니다. **Ex) 새로운 비디오 등록**

먼저 GET 요청의 경우에는 `video/video_new.html` 을 보여주는데 반해 POST 방식 경우에는 조금 더 처리를 해주는데요.

POST 방식의 경우 첫 줄에 나오는 if 구문으로 분기를 합니다. 그 다음 `request.POST['title']` 과 `request.POST['video_key']` 라는 문법이 나옵니다. 이 부분은 POST 파라미터로 넘어온 title 이라는 key를 가진 값과 video_key 키를 가진 값을 꺼내오는 작업입니다.

이 부분은 template 부분을 보면서 좀 더 자세히 설명해 드릴게요.

그렇게 POST에서 꺼내온 값으로 `Video.objects.create` 구문을 이용해서 새로운 Video 객체를 만듭니다.

---

## Url 추가하기

비디오를 추가하는 url을 만들기 위해 `video` 폴더 안의 `urls.py` 파일을 수정해 보도록 합시다.

```py
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

> 각 url 끝에 콤마(,)를 붙여주는 것을 잊지마세요!

---

## Template 추가하기
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

일단 이 template 파일에서 가장 낯선 부분은 아마도 `{% csrf_token %}` 부분일 거에요.이 템플릿 태그는 특별한 템플릿 태그인데요.
웹사이트 공격기법으로 `Cross-Site Request Forgery(CSRF)`라는 것이 있는데 이 공격을 장고가 기본적으로 막아주는 것이랍니다.

`form` 태그 안에는 꼭 써주셔야만 합니다. (만약 `csrf_token` 을 잊으신다면 장고가 경고를 띄울거에요!) 이제 form 태그 쪽을 보게되면, method를 POST로 지정하고 input을 2개 받는 걸 볼 수 있어요.

`input` 태그는 `name` 값을 잘 봐야 하는데요. Django의 view 쪽에서 `input` 안에 있는 값을 받게 되는데 그 값을 가져올 때 저name값을 통해서 가져오기 때문입니다.

위에 `video/views.py` 에서 저희가 `request.POST['title']` 과 `request.POST['video_key']` 로 작성했으므로 input 태그의 name 속성도 이에 맞춰서 작성해 주세요.

다 작성되었다면 다시한번 장고 서버를 실행해 보세요!

> 잊지 않으셨죠? 장고 서버는 `python manage.py runserver` 명령어로 띄울 수 있답니다!

이제 http://localhost:8000/video/new 로 들어가 보세요!

잘 보이네요!

![](/assets/fill-input-new-video.png)

이제 값을 입력하고 Submit 버튼을 눌러봅시다.

![](/assets/complete-video-list.png)

다음과 같이 생성되는 것을 볼 수 있어요.

하지만 뭔가 허전하죠?

Video의 제목을 클릭하면 그 비디오의 상세 페이지로 가고, 상세 페이지에서는 우리가 저장한 영상이 나오게끔 만들어 볼게요.