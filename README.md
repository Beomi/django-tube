# Django-Tube를 만들어봅시다!

![](/assets/djangogirls.jpg)

> 이 튜토리얼은 Creative Commons Attribution-ShareAlike 4.0 International 저작권을 따르고 있습니다. 라이센스 전문은
>
> [http://creativecommons.org/licenses/by-sa/4.0](http://creativecommons.org/licenses/by-sa/4.0)
>
> 에서 확인하세요.

이 문서는 장고걸스 서울 운영진이 만든 코딩 초심자를 위한 Django로 간단한 비디오 사이트를 만드는 튜토리얼입니다.

## 장고걸스는 어떤 단체인가요? {#번역}

[장고걸스](http://djangogirls.org/)는 여성들의 프로그래밍 학습의 기회를 제공하고 지지해주고자 설립된 국제비영리단체입니다. 2014년 7월, 올라시타스카\(Ola Sitarska\)와 올라 센데카\(Ola Sendecka\) 두 폴란드 여성들에 의해 베를린에서 시작하였으며 STEM 분야에 상대적으로 소수인 여성분들의 진출을 도와 Tech 분야의 다양성을 높이고자 노력하고 있습니다.

## 저자 {#번역}

이 튜토리얼은 열정적인 장고걸스서울 코치와 자원봉사자들의 수고로 작성되었습니다.

> 작성: [강명서](https://github.com/Leop0ld), [이소은](https://github.com/mojosoeun), [이준범](https://github.com/beomi), [황지영](https://github.com/jyhwng), [고명진](https://github.com/rjs1197), [김지형](https://github.com/roamgom), [이소영](https://github.com/SoYoung210), [서미지](#)

## 도움주신 분들 {#도움주신-분들}

장고걸스서울의 운영진과 코치들이 함께 튜토리얼을 준비했습니다.

> 강석진, 강명서, 고명진, 구지원, 김준영, 조다영, 배두식, 서미지, 송다운, 안자올, 양미림, 양민지, 윤병호, 이미희, 이소영, 이소은, 이준범, 이화랑, 양미림, 하현주, 한홍근, 황지영, Marta Allina

## 튜토리얼에서 무엇을 배우게 되나요? {#튜토리얼에서-무엇을-배우게-되나요}

이 튜토리얼은 **Django로 간단한 비디오 사이트**를 만드는 튜토리얼입니다. 튜토리얼이 끝나면 여러분들은 스스로 웹사이트를 만들 수 있을 거에요!

## 소개 {#소개}

이 튜토리얼은 [장고걸스 튜토리얼](https://tutorial.djangogirls.org/ko/)을 본격적으로 시작하기 전에 간단히 맛보기를 할 수있는 Django-Tube 튜토리얼입니다. Dev Django 행사 동안 함께 Django를 이용하여 비디오 사이트를 만드는 튜토리얼을 실습하시면서 자신감을 가져보아요!

## 설명 {#설명}

### 1. 들어가며 {#들어가며}

장고\(\[쟁고\]: Django\)는 전 세계에서 가장 인기 있는 언어인 파이썬으로 작성된 [오픈소스](https://github.com/django/django) 웹 프레임워크로 다양하고 복잡한 기능을 지원하고 있습니다. 여러분은 장고로 어플리케이션과 사이트 개발을 할 수 있어요. 이 튜토리얼은 [장고걸스 튜토리얼](https://tutorial.djangogirls.org/ko/)을 본격적으로 해보기 전에 장고를 연습할 수 있는 예고편이라고 할 수 있어요! 우리는 이미 어느정도 만들어진 소스를 깃헙에서 다운 받아 여러 기능을 추가하고 코드를 조금씩 수정해볼 거에요. 그럼 함께 시작해 볼까요?

### 2. 준비사항 {#준비사항}

노트북 그리고 즐거운 마음!

### 3. 튜토리얼의 목적

* 장고프로젝트를 시작하기 전에 가상환경을 올바른 방법으로 다룰 수 있습니다.
* 장고 관리자의 역할과 기능에 대해 이해할 수 있습니다.
* 장고 모델에 대해 알아봅니다.
* Git/Github의 기본 명령어로 프로젝트를 Github에 배포할 수 있습니다.

### 4. 따라하기 {#따라하기}

그럼 지금부터 시작해봅시다!

