# Django Model (모델)

Django 에서 Model은 데이터를 저장하는 역할을 합니다. Django의 모델을 더 알고 싶으시면 [여기](https://tutorial.djangogirls.org/ko/django_models/)를 클릭해 주세요!

Model 안의 클래스(class) 하나당 데이터베이스 테이블이 하나씩 생기게 되는데요.

우리는 Video 라는 Model을 만들고 저장해서 Video 리스트를 보여줄 것입니다. 그러기 위해선 Video Key와 제목을 저장하기 위한 `Video Model` 을 만들어야 합니다.

`video` 폴더 안의 `models.py` 에 다음과 같이 코드를 적어주세요.

```py
# video/models.py
from django.db import models

class Video(models.Model):
    title = models.CharField(max_length=200)
    video_key = models.CharField(max_length=12)
```

- `title` - 비디오의 제목을 저장

- `video_key` - 비디오의 키를 저장

title과 video_key 모두 문자로 되어있기 때문에 문자열을 저장할 수 있는 `CharField` 를 사용합니다.

우리는 방금 기존에 없던 새로운 모델인 `Video` 를 만들었다는 것을 데이터베이스에 알려줄 필요가 있습니다.

모델에 대한 변경사항을 데이터베이스에 알려주는 작업을 **Migration** 이라고 부릅니다. 이는 아래의 명령어로 실행할 수 있습니다.

- `makemigration` - 장고에서 모델에서 수정한 내역에 대해 migration파일로 생성해줍니다.

- `migrate` - makemigration 명령어로 만들어진 migration을 데이터베이스에 적용시켜 줍니다.

```shell
$ python manage.py makemigrations
$ python manage.py migrate
```

> makemigrations / migrate 명령어는 `models.py` 파일을 수정한 후 사용합니다.

자, 벌써 모델 만들기가 끝났어요!

이제 비디오 데이터들을 보여주는 `View` 와 `Template` 을 만들어볼게요.
