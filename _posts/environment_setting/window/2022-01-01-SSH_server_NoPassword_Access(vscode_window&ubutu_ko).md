---
title: SSH key발급 & Password없이 접속(vscode, window & ubuntu)
author: Kyungsup Go (Sup)
date: 2022-01-01 00:00:03 +0900
categories: [Environment setting, Window]

tags: [Window,Ubuntu,SSH]
toc: True
comments: true
---

# SSH key 발급 및 Password 등록순서

일반적으로 연구나 개발(단체소속)을 하시는 분들은 ssh 서버에 접속해서 각종 작업을 하는 경우가 많이 있습니다. 보통 이런 작업들은 하나의 자산이기때문에 보안 문제로 Password를 설정해놓습니다.<br> 그래서 매번 작업을 할 때마다 Password를 입력해줘야하는데 초기설정으로 번거롭게 Password를 매번 입력하는 일을 없애보겠습니다. 

해줘야할 일은 크게 3가지로 나뉩니다.


>1. local ( 서버가 아닌 본인 pc)의 ssh-key 발급
2. 발급된 ssh-key 파일은 ssh서버에 등록
3. local에서 ssh서버로 접속할 때 설정해주는 config 파일에 key파일정보기재<br>(config 파일 안에 key파일을 기재해주면 너한테 등록한 내 key파일은 여깄어~라고
       알려주게 되고 우리가 직접 Password를 매번 입력하지않아도 된다..)

# 1. Local의 ssh-key 발급 (공통)

먼저 작성자는 Window, Vscode에서 진행하였습니다.<br>아래에세 window powershell을 사용하는 데 명령어만 다를 뿐  우분투의 경우도 동일하게 key 발급 후<br>아래순서대로 진행하면 됩니다. ssh-key를 발급해봅시다.  

## 1-A. Window ssh key발급

### Window

<details>
<summary> 💻 window </summary>
<div markdown="1">

Window powerShell 을 열어줍니다.

![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_0.png) | ![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_1.png)

ssh-key 발급을 위한 명령어를 입력해줍니다. ( Enter입력하라고 나오면 그냥 해주면됩니다.)<br>
아래는 명령어& 설명입니다.

```powershell
ssh-keygen -t rsa -b 4096

########## 설명#################
# -t 옵션 => 암호화 타입 설정
# ssh는 public key 방식으로 동작할 수 있는 여러가지의 암호화 알고리즘을 사용하고 있습니다.
# 일반적으로 사용하는 rsa타입으로 설정하도록 하겠습니다.
###########################
# -b 옵션 => 생성할 key의 bit수를 지정
# 각 암호화 타입마다 필요한 비트수가 다릅니다.
# rsa 타입은 최소 768 비트가 필요하고 default로 2048 비트로 설정되어 있습니다.
# 여기서는 두 배 큰 4096으로 더 견고한 키를 만들겠습니다.
# (일반적으로 ssh-key할때 4096으로 많이 하기도 한다.)
###########################

# 옵션에 대한 설명은 
# https://storycompiler.tistory.com/112 을 참고하였습니다.

```

![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_2.png)

key발급은 private & public으로 이루어지는데 정상적으로 이루어지면<br>
`C:\Users\{Window 사용계정명}\.ssh`에 key 발급이 이루어집니다.<br>
우리가 서버에 복사해줄 key는 public key입니다.
```powershell
C:\Users\{Window 사용계정명}/.ssh/id_rsa.pub#이 public key입니다.
```

</div>
</details>



## 1-B. Ubuntu ssh key 발급

<details>
<summary> 🖥 Ubuntu </summary>
<div markdown="1">


    
우분투의 경우 현재 사용하고 있는 환경이 없어 글로만 설명합니다.<br>
ssh-key 발급을 위한 명령어를 입력해줍니다.( Enter입력하라고 나오면 그냥 해주면됩니다.)<br>아래는 명령어& 설명입니다.

```zsh
ssh-keygen -t rsa -b 4096

########## 설명#################
# -t 옵션 => 암호화 타입 설정
# ssh는 public key 방식으로 동작할 수 있는 여러가지의 암호화 알고리즘을 사용하고 있습니다.
# 일반적으로 사용하는 rsa타입으로 설정하도록 하겠습니다.
###########################
# -b 옵션 => 생성할 key의 bit수를 지정
# 각 암호화 타입마다 필요한 비트수가 다릅니다.
# rsa 타입은 최소 768 비트가 필요하고 default로 2048 비트로 설정되어 있습니다.
# 여기서는 두 배 큰 4096으로 더 견고한 키를 만들겠습니다.
# (일반적으로 ssh-key할때 4096으로 많이 하기도 한다.)
###########################

# 옵션에 대한 설명은 
# https://storycompiler.tistory.com/112 을 참고하였습니다.

```

정상적으로 발급시 

```zsh
ls ~/.ssh/
# 위의 경로에 없다면 사용중인 ubuntu의 사용자계정명의 폴더에서 찾아주세요 
# 보통 사용자계정명 밑에 .ssh파일에 key들이 생깁니다.
# id_rsa  와 id_rsa.pub 가 생겼다면 정상적으로 발급된 것입니다.
```

여기서 `id_rsa`와 `id_rsa.pub` 2개가 생겼는데 각 ***private key***와 ***public key***입니다.

</div>
</details>

## ✏️ SSH 간략 개념글
ssh, public&private key개념글은 나중에 쓸테지만 간략하게 알고싶다면 아래를 읽어주세요

<details>
<summary> 💾 설명 </summary>
<div markdown="1">

ssh key는 public / private 으로 발급됩니다.

- ***public*** : key의 암호화를 진행   (`~./ssh/id_rsa.pub` 으로 생성)
- ***private*** : key의 복호화를 진행  (`~./ssh/id_rsa` 으로 생성)

***public***과 ***private***가 key발급시 암호화 (public ) → 복호화 (private)
이렇게 한쌍으로 이루어집니다.<br>
***🔥private은 절대 외부에 유출하면 안됩니다.🔥***

그럼 이 key들로 어떻게 서버와 passwword입력없이 통신을 하게 하느냐?
우리 local (개인사용 pc) = 클라이언트( Client) 컴퓨터라고 해보겠습니다.

>1. 통신을 원하는 서버 컴퓨터에 클라이언트의 public key를 저장한다.
2. 클라이언트 컴퓨터가 접속요청을 할 때 요청을 받는 서버컴퓨터에 저장된
public key와 접속요청을 한 컴퓨터의 public key가 동일한지 확인한다 
1. 동일하면 클라이언트 컴퓨터에서 보낸 암호문을 private key로 복호화해 평서문으로 변환한다 ⇒<br>이게 우리가 보는 일반적인 글자들
<br>( 위에서 언급했듯이 public과 private은 한쌍으로 만들어지기 때문에 public key가
같은방식이면 private key로 복호화해 보냈던 내용과 동일하게 동일 수 있는 것입니다.)

아래는 위의 내용을 그림으로 도식화해 제작한 것입니다.

![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_3.png)

</div>
</details>

# 2. ssh 서버에 key 정보 등록

<details>
<summary> 💻 Window</summary>
<div markdown="1">

이제 public key를 서버의 ~/.ssh/**authorized_keys**  안에 내용을 바꿔주면 됩니다.<br>
할 수 있는 방법에는 여러가지가 있습니다.(어차피 복사하여 넣는다는 건 같습니다)

**첫번째.** CLI방식으로 scp을 사용하여 서버로 직접 파일대체<br>
**두번째.** window powershell에서 `Get-Content .\.ssh\id_rsa.pub` 입력후 내용복사하여 대체
<details>
<summary> 두번째 방법</summary>
<div markdown="1">
![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_4.png)

`Get-Content .\.ssh\id_rsa.pub` 을 입력하면 key값들이 쭉 뜰거고 이거를 복사해서 아래 서버 key값등록절차를 진행하면 된다.
</div>
</details>

**세번째.** GUI 방식으로 직접 파일을 확인하고 복사하여 대체

제일 쉬운 3번째 방식으로 진행하겠습니다. 

![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_5.png)

전 window사용계정명이 PC 이기때문에 pc아래에 .ssh볼더에 `id_rsa.pub`이 만들어져 있습니다.<br>
만약 사용자 계정명 폴더를 들어가는 방법을 모르신다면<br>
로컬디스크(C:) → 사용자 → 사용자계정명 폴더 → .ssh폴더 로 이동하시면 됩니다.<br>
`id_rsa.pub` 파일을 메모장으로 열어주면 안에 내용이 있고 이 내용을 복사해줍니다.

![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_6.png)

이제 복사한 내용을 붙여넣기 해주기위해서 서버에 접속합니다.

![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_7.png)

접속 후  단축키 `Ctrl` + `k`,`O`  을 누르거나  왼쪽 상단 **파일 → 폴더열기** 를 클릭하여 줍니다.

![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_8.png)

그럼 home/사용자계정명 밑에 .ssh폴더로 들어갑니다.

authorized_keys 파일안에 key값들이 있을 텐데 이걸 로컬에서 복사한 내용으로 바꿔줍니다.
(authorized_keys 파일이 없을 경우 그냥 만들어주면 됩니다)

![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_9.png)
</div>
</details>


    

<details>
<summary> 🖥 Ubuntu</summary>
<div markdown="1">

이제 public key를 서버의 ~/.ssh/**authorized_keys**  안에 내용을 바꿔주면 됩니다.
할 수 있는 방법에는 여러가지가 있습니다. (어차피 복사하여 넣는다는 건 같습니다)

- 직접 열어서 복사
- scp로 파일 전송하여 key 정보등록
- 공개키자체 내용복사하여 추가

위의 3번째 방식으로 진행해보겠습니다.

```zsh
cat ~/.ssh/id_rsa.pub
# public key값 내용 복사
```

이제 복사한 내용을 붙여넣기 해주기위해서 서버에 접속합니다.<br>
(사실 CLI로 해야하는데 위의 window내용을 작성하다 진이빠져 GUI방식으로 진행이되었습니다.<br>어차피 복사한 내용 붙여넣는 내용이니 같다고 보시면 됩니다.)

![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_7.png)

접속 후  단축키 `Ctrl` + `k`,`O`  을 누르거나  왼쪽 상단 **파일 → 폴더열기** 를 클릭하여 줍니다.

![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_8.png)

그럼 home/사용자계정명 밑에 .ssh폴더로 들어갑니다.

authorized_keys 파일안에 key값들이 있을 텐데 이걸 로컬에서 복사한 내용으로 바꿔줍니다.
(authorized_keys 파일이 없을 경우 그냥 만들어주면 됩니다)

![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_9.png)

</div>
</details>

# 3. Local config에 key파일 정보기재 (공통)

이제 서버에 접속요청을 할 때 Local의 public key값 파일이 서버가 알 수 있도록<br>Local의 config파일에 private key값 위치를 적어줍니다.

![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_10.png)

사진은 window라 `C:\User\{pc(사용자계정명)}\.ssh\config` 에 위치했지만 ubuntu도 마찬가지의<br>사용자계정명의 아래의 config를 찾아줍니다.<br>
해당 config를 열면 IdentityFile정보가 없을 텐데 이 부분에 private key값인  id_rsa 위치를 추가해줍니다. 
(public이 아닌 private key값인 id_rsa 를 적어줘야합니다. id_rsa .pub아닙니다!)

![Untitled](/assets/img/environment_setting/window/SSH_server_NoPassword_Access(vscode_window&ubutu)/Untitled_11.png)

이 상태로 저장하고 다시 ssh 서버에 접속하면 비밀번호를 입력하지않고 자동으로 접속이 가능해집니다.