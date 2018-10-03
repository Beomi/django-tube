# 설치하기

본격적으로 튜토리얼을 실습하기 전에 몇가지 설치 해야 되는 것이 있어요!

# 파이썬 설치하기

장고는 파이썬으로 만들어졌는데요! 장고를 하기 위해서는 파이썬이 설치되어 있어야 합니다. 파이썬 3.6 를 사용할 거에요.

먼저 Mac/Linux 환경에서는 terminal\(터미널\), Windows 환경에서는 prompt\(명령 프롬포트, CMD\)을 열고 프로젝트를 만들 폴더로 이동해봅시다. Command Line 여는 방법은 [여기](https://tutorial.djangogirls.org/ko/intro_to_command_line/#커맨드-라인-열기)를 참고 하면 됩니다!

### 윈도우 {#윈도우}

먼저, 사용 중인 컴퓨터 윈도우 운영체제가 32비트인지 64비트인지 확인해야 합니다.  `내 PC` 의 속성 페이지에 `시스템 종류` 부분을 보면 확인할 수 있습니다.  

윈도우용 파이썬은 [여기](https://www.python.org/downloads/release/python-361/)에서 다운 받을 수 있습니다.  Scroll을 아래로 내려서, `Python 3.6.1` 클릭하세요.  

![](/assets/pythonHompae1.PNG)

**64 비트** 버전의 Windows인 경우 Windows x86-64 executable installer를 다운로드하세요. 이외에는 Windows x86 executable installer을 다운로드하세요. 

> 기본적으로 python은 `C:\Users\윈도우유저이름\AppData\Local\Programs\Python\Python36`에 설치됩니다.

한가지 주의: 파이썬 설치 중 아래의 **"Add Python 3.6 to PATH"** 를 꼭! 체크하신 후 Install Now를 눌러주세요.

![](/assets/pinstall1.PNG)


파이썬이 성공적으로 설치되면 아래와 같은 화면이 나올거에요.

![](/assets/pinstall2.PNG)

파이썬이 잘 설치되었는지 확인하려면, 명령 프롬포트\(prompt\)를 켜 아래 명령어를 입력해 보세요!

```bash
$ python --version
Python 3.6.1
```

만약 다음과 같은 에러가 난다면,

```bash
'python'은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는 배치 파일이 아닙니다.
```

제어판에서 "시스템 환경 변수"를 검색해 "시스템 환경 변수 편집"을 눌러주세요.

![](/assets/system1.png)

아래와 같은 화면이 뜨면

![](/assets/system2.png)

아래의 "환경 변수\(N\)..."을 눌러 주신 후,

![](/assets/system-path1.PNG)

위 화면의 "Path"를 더블 클릭해 나온 화면에서

![](/assets/system-path2.PNG)

"새로 만들기\(N\)"을 누르신 후 아래 두 줄을 각각 입력해 주세요.\(새로 만들기를 두번 하셔야 합니다.\)

`C:\Users\윈도우유저이름\AppData\Local\Programs\Python\Python36`

`C:\Users\윈도우유저이름\AppData\Local\Programs\Python\Python36\Scripts`

> 경로는 위에서 파이썬을 설치한 경로입니다.

### 리눅스 {#리눅스}

리눅스는 이미 파이썬이 설치 되어 있어요!

```bash
$ python3 --version
Python 3.6.1
```

혹시 파이썬이 설치되어 있지 않거나 버전이 다르면 아래의 명령어를 작성해주세요!

콘솔에서 다음 명령을 실행하세요.\(Debian 또는 Ubuntu\)

```bash
$ sudo apt-get install python3.6
```

### OS X / Mac OS {#os-x}

[여기](https://www.python.org/downloads/release/python-361/)에서 파이썬 [설치프로그램을 다운](https://www.python.org/ftp/python/3.6.1/python-3.6.1-macosx10.6.pkg) 받으신 후, 다운받은 파일을 더블클릭해 설치를 진행해 주세요.

설치가 다 진행되었다면, 터미널\(terminal\)창을 켜신 후 아래 명령어를 통해 파이썬이 잘 설치되었는지 확인해 보세요!

```bash
$ python3 --version
Python 3.6.1
```

# Django 설치하기

## Django란 무엇인가요?

Django는 파이썬으로 만들어진 무료 오픈소스 웹 어플리케이션 프레임워크\(web application framework\) 입니다. 쉽고 빠르게 웹사이트를 개발할 수 있도록 돕는 구성요소로 이루어진 웹 프레임워크이랍니다. Django에 대해서 좀 더 자세히 알아보려면 [여기](https://tutorial.djangogirls.org/ko/django/)를 클릭해 주세요!

## Django 설치

아래 명령어를 이용해서 django를 설치합니다.

```bash
$ pip install django~=1.11.0
```
`pip install django~=1.11.0`(Django를 설치하려면 물결표 뒤에 등호 :~=)를 입력해 장고를 설치하세요.

![](/assets/django-install2.PNG)

축하합니다! 이제 장고 프로젝트를 시작할 준비가 되었습니다!

# 코드에티터 설치하기

코드에디터를 설치하면 개발에 좀 더 도움이 되는 환경에서 개발을 할 수 있어요. 여러 에디터 중 여러분들이 마음에 드는 코드 에디터 하나를 골라 컴퓨터에 설치해 주세요!

### Atom[\[다운로드 링크\]](https://atom.io/)

### sublime text [\[다운로드 링크\]](https://www.sublimetext.com/3)

### 왜 코드 에디터를 설치해야 하나요?
워드나 노트패드가 있는데도, 굳이 코드 에디터 소프트웨어를 설치해야 하는 이유가 궁금할 거에요.

첫 번째로 코드는 **일반 텍스트**여야 하는데, 워드나 텍스트에딧(Textedit)과 같은 프로그램에서는 일반 텍스트가 아닌 [RTF(Rich Text Format)](https://en.wikipedia.org/wiki/Rich_Text_Format)와 같은 사용자 서식을 쓴 리치 텍스트(폰트와 서식이 있는 텍스트)가 생성되기 때문입니다.

두 번째는 코드 에디터 프로그램은 개발에 유용한 여러 기능을 제공하기 때문입니다. 대표적인 예로, 코드를 해석해 문법을 하이라이팅해주는 기능이라든가 큰따옴표("")를 자동으로 닫아주는 기능이지요.

앞으로 코드 에디터가 어떻게 작동하는지 알아볼 거에요. 곧 여러분은 내가 사용하는 코드 에디터를 제일 좋아하게 될 거랍니다.

# Github 계정 만들기

[https://github.com/](https://github.com/)로 접속하여 계정을 하나 만들어 봅시다.

##### 우와! 이제 코딩 할 준비를 다 하게 되었어요! 고생하셨습니다!

##### 이제 본격적으로 시작해볼까요? :\)



