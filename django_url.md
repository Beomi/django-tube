# Urls

template 파일을 만들기 전에, View 와 template 파일을 연결해주는 `urls.py`를 만들어 볼게요.

urls.py 에는 어떤 URL에 어떤 View를 연결시켜줄 것인지를 작성합니다.

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

`namesapce`는 직역하면 이름공간 이라는 뜻인데 관련있는 url 이름들을 한 곳에 묶고 싶을 때 사용합니다.

아래에서 코드를 마저 작성하고 사용법을 알아볼게요.

우선 `video`폴더안의 `urls.py` 에는 다음과 같이 코드를 적어주세요.

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

이해가 잘 안 되셨다면 언제든지 질문해주세요! 성심성의껏 알려드릴게요.

