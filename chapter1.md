# 설치하기

본격적으로 튜토리얼을 실습하기 전에 몇가지 설치해야 되는 것이 있어요!

# 파이썬 설치하기

장고는 파이썬으로 만들어졌는데요! 장고를 하기 위해서는 파이썬이 설치되어 있어야 합니다. 파이썬 3.5 를 사용할 거에요.

먼저 Mac/Linux 환경에서는 terminal\(터미널\), Windows 환경에서는 prompt\(명령 프롬포트, CMD\)을 열고 프로젝트를 만들 폴더로 이동해봅시다. Command Line 여는 방법은 [여기](https://tutorial.djangogirls.org/ko/intro_to_command_line/#커맨드-라인-열기)를 참고 하면 됩니다!

### 윈도우 {#윈도우}

윈도우용 파이썬은 [여기](https://www.python.org/downloads/release/python-353/)에서 다운 받을 수 있습니다.  이 사이트에서 [설치파일을 다운로드](https://www.python.org/ftp/python/3.5.3/python-3.5.3.exe) 받아 설치합니다. 파이썬을 설치한 경로를 기억해주시면 좋답니다.

> 기본적으로 python은 `C:\Users\윈도우유저이름\AppData\Local\Programs\Python\Python35-32`에 설치됩니다.

한가지 주의: 파이썬 설치 중 아래의 "Add Python 3.5 to PATH"를 꼭! 체크하신 후 Install Now를 눌러주세요.

![](https://www.dropbox.com/s/oi3i8d7dxl7l6nm/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-02-23%2020.13.35.png?dl=1)

만약 아래와 같은 화면이 뜬다면 '예'를 눌러주세요.

![](https://www.dropbox.com/s/loxaxfk0wr7ka2f/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-02-23%2020.16.56.png?dl=1)

파이썬이 성공적으로 설치되면 아래와 같은 화면이 나올거에요.

![](https://www.dropbox.com/s/9miyxofq94ftjdy/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-02-23%2020.17.55.png?dl=1)

파이썬이 잘 설치되었는지 확인하려면, 명령 프롬포트\(prompt\)를 켜 아래 명령어를 입력해 보세요!

```bash
$ python --version
Python 3.5.3
```

만약 아래 사진과 같은 에러가 난다면,

![](https://www.dropbox.com/s/9cribp2hnpikipi/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-02-23%2020.24.00.png?dl=1)

제어판에서 "시스템 환경 변수"를 검색해 "시스템 환경 변수 편집"을 눌러주세요.

![](https://www.dropbox.com/s/iebgr1hspfa8bta/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-02-23%2020.28.28.png?dl=1)

아래와 같은 화면이 뜨면

![](https://www.dropbox.com/s/gcn6yvw9761ldpu/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-02-23%2020.28.59.png?dl=1)

아래의 "환경 변수\(N\)..."을 눌러 주신 후,

![](https://www.dropbox.com/s/aw422rg4m9wpj3f/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-02-23%2020.30.17.png?dl=1)

위 화면의 "Path"를 더블 클릭해 나온 화면에서

![](https://www.dropbox.com/s/745q16o9y5r6oae/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202017-02-23%2020.31.12.png?dl=1)

"새로 만들기\(N\)"을 누르신 후 아래 두 줄을 각각 입력해 주세요.\(새로 만들기를 두번 하셔야 합니다.\)

`C:\Users\윈도우유저이름\AppData\Local\Programs\Python\Python35-32`

`C:\Users\윈도우유저이름\AppData\Local\Programs\Python\Python35-32\Scripts`

> 경로는 위에서 파이썬을 설치한 경로입니다.

### 리눅스 {#리눅스}

리눅스는 이미 파이썬이 설치 되어 있어요!

```bash
$ python3 --version
Python 3.5.3
```

혹시 파이썬이 설치되어 있지 않거나 버전이 다르면 아래의 명령어를 작성해주세요!

콘솔에서 다음 명령을 실행하세요.\(Debian 또는 Ubuntu\)

```bash
$ sudo apt-get install python3.5
```

### OS X / Mac OS {#os-x}

[여기](https://www.python.org/downloads/release/python-353/)에서 파이썬 [설치프로그램을 다운](https://www.python.org/ftp/python/3.5.3/python-3.5.3-macosx10.6.pkg) 받으신 후, 다운받은 파일을 더블클릭해 설치를 진행해 주세요.

설치가 다 진행되었다면, 터미널\(terminal\)창을 켜신 후 아래 명령어를 통해 파이썬이 잘 설치되었는지 확인해 보세요!

```bash
$ python3 --version
Python 3.5.3
```

# 가상환경 설정 및 Django 설치

본격적으로 Django를 설치하기 전에 개발환경을 좀 더 편리하고, 깨끗하게 관리 할수 있는 가상환경을 설정해 봅시다. 파이썬 가상환경이 좀 더 궁금하다면 [여기](https://tutorial.djangogirls.org/ko/installation/#가상-환경)에서 좀 더 자세한 내용을 찾아 볼수 있답니다!

## 가상환경 설정

#### Windows:

```bash
> python -m venv myvenv
```

#### Mac: {#mac}

```bash
$ python3 -m venv myvenv
```

#### Linux: {#linux}

리눅스에서 venv를 사용하려면 `python3-venv`를 먼저 설치해 주어야 한답니다.

```bash
$ sudo apt-get install python3-venv
```

```bash
$ python3 -m venv myvenv
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

# Django 설치하기

## Django란 무엇인가요?

Django는 파이썬으로 만들어진 무료 오픈소스 웹 어플리케이션 프레임워크\(web application framework\) 입니다. 쉽고 빠르게 웹사이트를 개발할 수 있도록 돕는 구성요소로 이루어진 웹 프레임워크이랍니다. Django에 대해서 좀 더 자세히 알아보려면 [여기](https://tutorial.djangogirls.org/ko/django/)를 클릭해 주세요!

## Django 설치

가상환경을 설정하고 활성화 하고 나면 터미널 또는 prompt에서 다음과 같이 보일거에요! 혹시 보이지 않는다면 언제든지 도움을 요청해 주세요!

```
(myvenv)...
```

그리고 이제 아래 명령어를 이용해서 django를 설치합니다.

> 앞에 myvenv가 있는지 확인 후 진행하세요!

```bash
(myvenv)$ pip install django
```

축하합니다! 이제 장고 프로젝트를 시작할 준비가 되었습니다!

# 코드에디터 설치하기

코드에디터를 설치하면 개발에 좀 더 도움이 되는 환경에서 개발을 할 수 있어요. 여러 에디터 중 여러분들이 마음에 드는 코드 에디터 하나를 골라 컴퓨터에 설치해 주세요!

#### 1. Atom[\[다운로드 링크\]](https://atom.io/)

#### 2. Sublime Text [\[다운로드 링크\]](https://www.sublimetext.com/3)

# Github 계정 만들기

[https://github.com/](https://github.com/)로 접속하여 계정을 하나 만들어 봅시다.

##### 우와! 이제 코딩 할 준비를 다 하게 되었어요! 고생하셨습니다!

##### 이제 본격적으로 시작해볼까요? :\)



