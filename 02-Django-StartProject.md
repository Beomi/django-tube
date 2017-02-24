# 나의 첫번째 DjangoTube 프로젝트!

오늘 우리는 Django로 유튜브동영상을 추가할 수 있는 간단한 동영상 서비스를 만들어 볼거에요!

앞에서 Python과 Django를 설치 해 보았으니 본격적으로 프로젝트를 시작해 보는 첫 단추를 끼워 봅시다. 장고의 기본 골격을 만들어주는 스크립트를 실행해 볼건데요. 이 디렉토리와 파일 묶음은 나중에 사용할 것입니다. 장고에서는 디렉토리 이름과 파일 이름이 무척 중요하므로 파일이름을 마음대로 변경해서도, 다른곳으로 옮기면 안되는 것을 꼭 기억해 주세요!

다음 명령어를 실행해서 여러분의 첫번째 django 프로젝트를 만들어 봅시다.

```
(myvenv) $ django-admin startproject djangotube .
```
> 점 .은 현재 디렉토리에 장고를 설치하라고 스크립트에 알려주기 때문에 중요해요. 꼭 잊지 말아주세요!


`djangotube`라는 이름을 가진 django 프로젝트를 생성하게 되면 아래와 같은 디렉토리 구조를 가지게 됩니다.

```
.
├── djangotube
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── manage.py
```

데이터베이스를 생성해 주기 위해 아래의 명령어를 입력해 줍니다.

```
(myvenv) $ python manage.py migrate

```

`db.sqlite3`라는 데이터베이스 파일이 생겼을 거에요.

이제 웹 서버를 시작해 웹사이트가 잘 작동하는지 확인해봅시다.

```
(myvenv) $ python manage.py runserver

```

윈도우에서 UnicodeDecodeError를 썼는데 오류가 난다면 아래 명령을 대신 써보세요.

```
(myvenv) python manage.py runserver 0:8000

```

브라우저\(크롬, 인터넷익스플로러 등\)로 `127.0.0.1:8000`에 접속해서 장고가 잘 동작하는지 확인해보세요!

![](/assets/itworks.png)

위와 같은 페이지가 뜬다면 성공적으로 장고가 동작하고 있는거에요.
우와아아 축하합니다! :\)

## 어플리케이션 추가하기

우선 장고 서버를 Ctrl키와 C를 누르셔서(`Ctrl+C`) 꺼 주시고, 아래 과정을 진행해 주세요.

여러분의 첫번째 프로젝트를 만들었어니 djangotube 프로젝트 안에 video 라는 App을 만들어 볼거에요!

> manage.py 파일이 있는 위치에서 다음 명령어를 입력해 보도록 하죠.

```
(myvenv) $ python manage.py startapp video
```

djangotube 폴더\(manage.py파일이 있는 곳\) 안에서 위의 명령어를 입력해 주게 되면 아래와 같은 디렉토리 구조를 가지게 됩니다.

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

어플리케이션을 생성한 후 장고에게 사용해야한다고 알려줘야 합니다. 이 역할을 하는 파일이 mysite/settings.py인데요. 이 파일 안에서 INSTALLED_APPS를 열어, )바로 위에 `video`를 추가하세요. 최종 결과물은 아래와 다음과 같을 거에요.

```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'video',
]

```

다음 챕터로 넘어가 볼까요!!
