# djangotube 시작하기

다음 명령어를 통해 django 프로젝트를 만듭니다.

```
(myvenv) $ django-admin startproject djangotube
```

입력하게 되면 `djangotube`라는 폴더가 하나 생긴답니다.

이 폴더 안에는 `djangotube`라는 이름을 가진 django 프로젝트가 생긴 거랍니다. 장고가 알아서 기본 틀을 만들어 준거죠!

처음에 django 프로젝트를 만들게 되면 다음과 같은 구조를 가져요.

```
.
├── djangotube
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── manage.py
```

프로젝트만 만들고 지켜볼 수는 없겠죠? 한 번 실행시켜볼게요!

그 전에 먼저 다음 명령어를 통해 데이터베이스를 생성해 줍니다.

```
(myvenv) $ python manage.py migrate
```

이제 `db.sqlite3` 라는 데이터베이스 파일이 생겼을 거에요.

다음에는 django 서버를 동작시켜볼게요.

아래 명령어로 통해 django 서버를 구동시킬 수 있답니다.

```
(myvenv) $ python manage.py runserver
```

위와 똑같이 명령어를 입력한다면 브라우저\(크롬, 인터넷익스플로러 등\)로 `127.0.0.1:8000`에 접속해서 장고가 잘 동작하는지 확인할 수 있답니다.

![](/assets/itworks.png)

위와 같은 페이지가 뜬다면 성공적으로 장고가 동작하고 있는거에요. 축하합니다! :\)

# 본격적으로 코딩 시작하기

django 서버를 띄우는 데에 성공했으니 이제 기능을 구현해봅시다.

먼저 저희는 Youtube에서 Video의 주소를 가져와서 제목과 함께 저장할거에요.

그러기 위해서는 django에 있는 `Model`이라는 걸 먼저 알아야 해요.

또, `Model`을 사용하기 위해서는 `App` 이라는 것도 알아야 한답니다.

백문이 불여일견. 한 번 App을 만들어볼까요?

App은 다음 명령어로 만들 수 있어요. 저는 video 라는 App을 만들어 보겠습니다.

> manage.py 파일이 있는 위치에서 명령어를 입력하시면 됩니다.

```
(myvenv) $ python manage.py startapp video
```

djangotube 폴더\(manage.py파일이 있는 곳\) 안에서 다음과 같이 입력해주게 되면 프로젝트 파일의 구조는 다음과 같아집니다.

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

# 

# 

# 

# 



