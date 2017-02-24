# Django Admin으로 비디오 추가하기

Django에는 `Admin`이라는 강력한 기능이 기본적으로 제공된답니다.

이 `Admin`은 앱 폴더(`video`폴더)안의 `admin.py`파일에 코드 몇 줄만 추가해줘도 바로 사용할 수 있어요.

## 최고 관리자(Superuser)만들기

admin 파일을 수정하기 전에, 장고에 들어가는 첫번째 슈퍼 사용자를 만들어 볼게요!

슈퍼 사용자는 장고 웹 사이트의 최고관리자랍니다.

이 슈퍼 사용자는 `createsuperuser`라는 명령어로 만들 수 있답니다.

```bash
(myvenv) $ python manage.py createsuperuser
```

![](https://www.dropbox.com/s/9s9dd8afhseahq0/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-02-24%2021.59.18.png?dl=1)

유저 이름이 ID이고, 이메일 주소는 쓰지 않으셔도 괜찮아요.

이제 장고에서 어드민 페이지에 들어갈 수 있어요. 장고의 기본 어드민 페이지의 주소는 `/admin`이랍니다.

> [http://localhost:8000/admin/](http://localhost:8000/admin/)으로 들어가보세요!

![](https://www.dropbox.com/s/laic7rz2v8pqgd2/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-02-24%2022.00.50.png?dl=1)

## Admin에 Video 앱 추가하기

아직은 우리가 만든 Video 앱을 장고 admin이 관리한다고 알려주지 않았어요.

`admin.py`파일을 아래와 같이 수정해 보세요! 이제 장고가 Video라는 앱을 Admin페이지에서 관리해 줄거에요.

```py
# video/admin.py
from django.contrib import admin
from .models import Video

admin.site.register(Video)
```

장고 서버는 장고 파일들의 수정을 눈치채면 바로 꺼졌다 다시 켜진답니다.

만약 장고 서버를 꺼버리셨다면, 아래의 `runserver`명령으로 다시 켜 주세요!

```bash
(myvenv) $ python manage.py runserver
```

이제 다시 들어가 보면, 아래와 같이 Video라는 앱이 Admin화면에서 보일거에요!

![](https://www.dropbox.com/s/vqp7a943w5uf8qc/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-02-24%2022.02.26.png?dl=1)

## Admin에서 비디오 추가하기

이제 유투브에 가서 동영상의 '키'를 가져올게요!

![](https://www.dropbox.com/s/tqyheqf1hzbdfoc/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-02-24%2022.09.47.png?dl=1)

위 스크린샷을 보면 위쪽 URL에 `watch?v=어쩌구저쩌구`라는 부분이 보이실거에요.(파란색 하이라이트)

이 부분이 바로 유투브 동영상의 고유 키 인데요, 이 키를 복사해서 아래의 Django Admin에서 Video Key부분에 입력해 볼게요.

![](https://www.dropbox.com/s/z4q4gm5veuo4iwi/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-02-24%2022.13.41.png?dl=1)

저장 버튼을 누르면 '성공적으로 추가되었습니다' 라는 메시지가 뜰거에요!

![](https://www.dropbox.com/s/g3g77h4ikzct1xm/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-02-24%2022.14.04.png?dl=1)

축하해요! 첫 비디오를 추가하셨어요!

이제 다시 [비디오 리스트](http://localhost:8000/video/)로 돌아가볼게요.

![](/assets/void-new-video.png)

잘 보이네요!

![](/assets/fill-input-new-video.png)

이제 값을 입력하고 Submit 버튼을 눌러봅시다.

![](/assets/complete-video-list.png)

다음과 같이 생성되는 것을 볼 수 있어요.

이제 장고 Admin이 아니라 우리가 만든 페이지에서 Video를 등록해 볼게요.
