# 시작하기

#### 이 튜토리얼은 아래의 링크에서 확인하실 수 있습니다. {#이-튜토리얼을-찍고-내-리퍼지토리로-복사하세요}

[저장소 링크](https://github.com/DjangoGirlsSeoul/djangotube)

![](/assets/스크린샷 2017-02-15 오후 7.20.21.png)

Mac/Linux 환경에서는 terminal, Windows 환경에서는 prompt을 열고 프로젝트를 만들 폴더로 이동합니다.

아래 명령어를 콘솔에 치고 가상환경을 만듭니다.

#### Windows: {#windows}

```bash
C:\Python35\python -m venv myvenv
```

#### Mac: {#mac}

```bash
$ python3 -m venv myvenv
```

#### Linux: {#linux}

```bash
$ virtualenv --python=python3.4 myvenv
```

이제 만들어진 가상환경을 활성화 시켜 볼까요?

#### Windows: {#windows}

```
myvenv\Scripts\activate
```

#### Mac/Linux: {#maclinux}

```bash
$ source myvenv/bin/activate
```

터미널 또는 prompt에서 다음과 같이 보이는지 확인합니다.

```
(myvenv)...
```

그리고 이제 아래 명령어를 이용해서 django를 설치합니다.

```bash
$ pip install django
```

다음 명령어를 통해 django 프로젝트를 만듭니다.

```
$ django-admin startproject djangotube
```

입력하게 되면 `djangotube` 라는 폴더가 하나 생겼습니다.

django 프로젝트를 만들었으니 본격적으로 코딩할 준비가 끝났습니다!

시작해볼까요? :\)

