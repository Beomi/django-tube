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

django

# View



# Template





