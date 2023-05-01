# 책 : 우분투리눅스 08장

# 원격지 시스템 관리하기

## 텔넷 서버

### 텔넷 서버 개요

보안이 취약하기에, 텔넷에 보안 기능을 더해서 사용하는 추세.

텔넷은 가장 기본적인 것이기 때문에 알아야함.

![UL0800](/src/polytech/suyoung/img/UL08/Untitled.png)

원격지의 PC(텔넷 클라이언트)에서 리눅스 서버에 접속하면 서버 앞에 앉아 직접 텍스트 모드로 작업하는 것과 완전 동일한 효과 가능. 

### 텔넷 서버의 구축

![UL0801](/src/polytech/suyoung/img/UL08/Untitled%201.png)

구체적인 과정은 SSH서버를 구축하며 해보기로 한다. 

## SSH 서버

### OpenSSH 서버 개요

텔넷과 거의 동일하지만, 데이터 전송 시 암호화를 함.

보안이 강화된 텔넷 서버보다 일반적으로 SSH서버를 더 많이 사용함. 

![UL0802](/src/polytech/suyoung/img/UL08/Untitled%202.png)

### OpenSSH 서버 구축

![UL0803](/src/polytech/suyoung/img/UL08/Untitled%203.png)

기존에 zabbix를 설치한 virtualbox_ubuntu_zabbix에 OpenSSH 서버를 구축해보자. 

```
sudo apt-get -y install openssh-server
//ssh 서버 설치

sudo systemctl restart ssh
//서비스 재가동
sudo systemctl  enable ssh
//서비스 상시 가동
sudo systemctl status ssh
//서비스 가동 여부 확인(q누르면 종료)
```

![UL0804](/src/polytech/suyoung/img/UL08/Untitled%204.png)

(이미 최신버전이 설치되어있다고 나온다)

```
sudo allow 22/tcp
//방화벽에서 ssh의 포트인 22번을 허용
```

![UL0805](/src/polytech/suyoung/img/UL08/Untitled%205.png)

클라이언트의 cmd를 키고, 접속한다. 

```
ssh poly@192.168.56.200
//openssh 서버의 ip 주소를 입력한다. 
```

![UL0806](/src/polytech/suyoung/img/UL08/Untitled%206.png)

## VNC 서버

### VNC 서버 개요

x윈도우 환경에서도 작업이 하고 싶을 때 사용한다. 

![UL0807](/src/polytech/suyoung/img/UL08/Untitled%207.png)

VNC서버를 사용하면, 원격지에서 X윈도 환경 자체를 사용할 수 있게 된다. 다만 텍스트만 전송하는 텔넷, SSH보다는 속도가 느리다. 

### VNC서버 구축

![UL0808](/src/polytech/suyoung/img/UL08/Untitled%208.png)

vncserver패키지가 설치되어있지 않은 상태인듯함.

![UL0809](/src/polytech/suyoung/img/UL08/Untitled%209.png)

패키지저장소에 패키지가 업로드되지 않았기에, 업데이트를 다시하기로함.

일단 vnc4server설치가 제대로 되지 않기에, 윈도우에서vnc viewer를 통해 vnc를 실현해보고자함. 

![UL0810](/src/polytech/suyoung/img/UL08/Untitled%2010.png)

우분투에서 sharing 설정을 다음과 같이 바꿔준다. 

```
sudo apt install dconf-editor
//dconf-editor는 GNOME 데스크톱 환경에서 사용되는 설정 편집 도구 중 하나

sudo ufw allow 5900/tcp
//방화벽 열기, 5900 포트 허용
```

vnc viewer를 설치하고, ip를 입력하면 접속가능하다. 

![UL0811](/src/polytech/suyoung/img/UL08/Untitled%2011.png)

## 정리 : 3개 비교

![UL0812](/src/polytech/suyoung/img/UL08/Untitled%2012.png)

텔넷 서버는 보안이 완전한 회사 내 네트워크에서만 사용을 권장. 

원격지에서 ssh서버로 접속해 관리하다, x윈도 환경이 필요할 경우 vnc 서버를 구동해 vnc 클라이언트로 접속하기.