# 시작하기

#### 이 튜토리얼은 아래의 링크에서 확인하실 수 있습니다. {#이-튜토리얼을-찍고-내-리퍼지토리로-복사하세요}

[링크](https://github.com/Leop0ld/djangotube)로 가서 오른쪽 위에 있는 Fork 버튼을 누릅니다.

![](/assets/스크린샷 2017-02-15 오후 7.20.21.png)

`git clone`을 사용하여 여러분의 컴퓨터에 코드를 복사합니다.

![](/assets/스크린샷 2017-02-15 오후 7.22.11.png)

```bash
$ git clone https://github.com/<USER_NAME>/djangotube.git
```

> 주의: `USER_NAME` 이 부분에 여러분의 Github username을 적어주세요. 여러분의 레파지토리에 fork 되어야 합니다.

Mac/Linux 환경에서는 terminal, window 환경에서는 prompt을 열고 djangocupcakeshop 폴더로 이동합니다.

`cd djangotube`치고 djangotube 폴더 안으로 이동합니다.

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
$ pip install -r requirements.txt
```

`python manage.py migrate`통해 데이터 베이스를 만듭니다.

다음 명령어를 쳐서 데이터베이스를 만듭니다.

```
$ python manage.py migrate
```

입력하게 되면 `db.sqlite3` 라는 파일이 하나 생깁니다. 성공했습니다!

