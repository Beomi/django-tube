# Django Model \(모델\)

Django 에서 Model은 데이터를 저장하는 역할을 합니다. Django의 모델을 더 알고 싶으시면 [여기](https://tutorial.djangogirls.org/ko/django_models/#django-모델)를 클릭해 주세요!  Model 안의 클래스\(class\) 하나당 데이터베이스 테이블이 하나씩 생기게 되는데요. 우리는 Video 라는 Model을 만들고 저장해서 Video 리스트를 보여줄 것입니다. 그러기 위해선 Video Key와 제목을 저장하기 위한 `Video Model`을 만들어야 합니다.

`video`폴더 안의 `models.py`에 다음과 같이 코드를 적어주세요.

```python
# video/models.py
from django.db import models


class Video(models.Model):
    title = models.CharField(max_length=200)
    video_key = models.CharField(max_length=12)
```

먼저 Video의 제목을 저장하기 위한 **title**, 그리고 Video Key 를 저장할 수 있는 **video\_key** 를 만들어줘야 합니다. title과 Video Key 모두 문자열로 구성되어있기 때문에 `CharField`\(캐릭터필드\)로 설정해줍니다. 이 변경사항들을 데이터베이스에게 알려주기 위해서는 **Migration** 이라는 작업. 즉 실제 데이터 베이스에 적용하는 작업이 필요해요. 그러기 위해서는 아래의 명령어로 실행할 수 있습니다. `makemigrations` 명령어를 입력하게 되면 django 에서 자동으로 Migration 파일을 만들어주고, `migrate` 명령어로 만들어진 Migration 파일을 데이터베이스에 적용하는 작업을 하는 거에요.

```
(myvenv) $ python manage.py makemigrations video
(myvenv) $ python manage.py migrate video
```

> makemigrations / migrate 명령어는 models.py 파일을 수정한 후 사용합니다.

자, 벌써 모델 만들기가 끝났어요!

이제 비디오 데이터들을 보여주는 `View`와 `Template`을 만들어볼게요.

