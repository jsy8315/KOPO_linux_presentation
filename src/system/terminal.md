---
layout: home
---

# 터미널 과 쉘


## 쉘이란
쉘이란 키보드로 입력한 명령어 를 운영체제에 전달하여 이 명령어 를 실행하게 하는 프로그램이다. 
대부분의 리눅스 배포판은 bash 라고 하는 GNU 프로젝트의 쉘 프롬프트를 제공합니다.


### 쉘의 종류



### 터미널 에뮬레이터
만일 x-windows의 GUI 환경을 사용하고 이싿면 쉘과 직접 작업을 할 수 있도록 터미널 에물레이터 프로그램이 필요합니다.


### 쉘 프롬프트
처음 터미널로 리눅스를 실행하게 되면 다음과 같은 명령 입력 상태를 볼 수 있다.

```
hojin@hojin3:~$
```
이를 쉘 프롬프트라고 합니다. 셀의 프롬프트 모양은 배포판에 따라서 약간씩 차이가 있습니다.

프롬프트만 으로 터미널 세션의 권환을 확인할 수 있습니다. 마지막 글자가 `$`로 나타나면 일반사용자를 말하며, `#`로 끝나면 슈퍼유저(superuser) 권환을 의미 합니다.

### 명령어 히스토리
셀은 사용자가 입력한 명령들을 기억하고 있습니다. 키보드의 화살표 위/아래 방향키를 입력하면 마지막에 입력한 명령어가 다시 나타나는 것을 볼 수 있습니다.  

이러한 기능을 `명령어 히스토리`라고 한다. 기본적으로 최근 `500`개의 명령어를 기억할 수 있습니다.

### 커서이동
키보드 좌/우 방향키를 사용하여 명령어를 쉽게 편집할 수 있다.

> 만일, 셀을 gui에서 터미널 창을 통하여 실행을 하는 경우, 마우스를 통하여 함께 조작을 할 수 있다.

### 터미널 세션 종료
셀 프롬프트에서 `exit`명령을 입력합니다. 현재의 셀이 종료 됩니다.

```bash
hojin@hojin3:~$ exit
logout
```

### 가상터미널