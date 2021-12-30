---
title: Writing a New Post
author: Cotes Chung
date: 2019-08-09 15:10:00 +0900
categories: [Blogging, Tutorial]
tags: [writing]
---


# Mac M1 github 연결하기

Created: December 20, 2021 9:40 PM

글 작성에 앞서 이 글은 github의 기본적인 작동(?)순서를 알고 있다고 가정하고 설명을 진행합니다. 
모르시는 분들은 이 링크  [https://sin0824.tistory.com/8](https://sin0824.tistory.com/8)  [https://kkaeruk.tistory.com/3](https://kkaeruk.tistory.com/3)의 순서를 참고하세요. 순서만 알고 내용을 따라하지는 말으시길 권장합니다 그 이유가 있습니다.

그 이유는 2021년 8월 13일부터 github에 Push할 때 인증방법이 바뀌었습니다.
이전에는 Password로 인증을 진행한 후 push가 가능했지만 이제는 PAT(Personal Access Token)와 ssh key 방식 2가지로만 가능합니다. 그래서 21년 8월 기준으로 이전 글들을 보시고 따라하시면 push할 때 오류가 생깁니다.  각각의 방식에 대한 장단점은 아래처럼 정리해 볼 수 있습니다. (실제로 하나의 Mac에서 여러 github을 사용할 경우 ssh를 사용하여 할 수 있습니다.)

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled.png)

출처 : [https://blog.neonkid.xyz/277](https://blog.neonkid.xyz/277)

(공식 github에서 인증방식 변경에 관한 글)

[https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/)

```bash
remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
remote: Please see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/ for more information.
fatal: unable to access 'https://github.com/userName/repoName.git/': The requested URL returned error: 403
```

이 글에서는 ssh key 기준으로 github을 연결해보겠습니다. (token이 편하신 분들을 위해 글 맨 마지막 하단에 잘 설명되어있는 링크들 달아 놓겠습니다.) 

공식 docs 에 나와있는 ssh key 연결 방법입니다. [https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh) 

ssh key 연결방법이 영어로 나와 있으므로 불편하실 분들을 위해 저의 방식대로 정리해보겠습니다.

먼저

1.  큰 개념인 ssh key 인증방식이 무엇인지 ?

2. ssh key 발급 방법 (ed25519 ,rsa)

3. 발급받은 ssh key를 github에 등록하기

4. github에 등록된 키와 통신을 위한 Local(Mac 설정)

~~ 기타 

순으로 진행하겠습니다. (본인이 이미 진행하신 부분이 있다면 다음부터 보시면 됩니다.) 

1. ssh key란 ??

ssh의 개념은 파고들면 복잡해지기 때문에 간단히 설명해놓은 제 글 링크를 첨부합니다. 좀 더 알고 싶은신분들은 링크 ~~  유투브~~ 이거 보세요  

ssh key발급에 앞서 기존에 본인도 모르게 key를 발급받은 적이 있을 수 있으므로 발급된 키가 있나 확인해봅니다. ssh key는 보통 ~/.ssh 위치에 저장됩니다. 터미널을 열어 ls(파일목록) 을 보면 .경로는 숨겨지기 때문에 ls -al로 조회해보겠습니다.  -al 옵션을 주면 보이게 되는 .경로들에 ssh항목이 없으므로 ssh key가 발급된 적이 없는 것으로 확인됩니다. 이렇게 보아도 되고 cd ~/.ssh 로 이동해서 `id_rsa`와 `id_rsa.pub` 의 파일쌍을 확인해도 됩니다.

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%201.png)

2. ssh key 발급 방법 (ed25519 ,rsa)

ssh key 파일이 없으므로 발급을 받아주겠습니다. 

ssh key 발급방식에는 여러 옵션이 있습니다. 

[-t dsa | ecdsa | ed25519 | rsa | rsa1] 저는 암호학 전문가가 아니므로 보통 많이 쓰이는 ed25519와 rsa방식만 알고 있습니다.  일반적으로 ed25519가 지원하면 사용하고 지원하지않으면 rsa방식을 사용하기도 하고 각각의 장단점이 있다. (출처는 여러분들의 의견이 있지만 좀 더 차이를 비교해주신 [https://www.nemonein.xyz/2018/10/1124/](https://www.nemonein.xyz/2018/10/1124/) 이분의 글이 신빙성이 있어보인다.)  요즘 ed25519를 왠만하면 지원하기도 하고 github공식사이트에서도 가급적 ed25519방식으로 안내하므로 ed25519방식으로 생성하겠습니다. (rsa 방식도 크게 다르지 않기 때문에 설명은 같이 달아두겠습니다.)

```bash
ssh-keygen -t ed25519 -C "your_email@example.com" 
# ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
# 여기서 e-mail은 github가입 이메일을 넣어주세요 
# ed25119 쓰실분은 위에코드 사용하여 만들면 됩니다. 
########## 설명#################
# -t 옵션 => 암호화 타입 설정
# ssh는 public key 방식으로 동작할 수 있는 여러가지의 암호화 알고리즘을 사용하고 있습니다.
# 위에서 설명한 이유들로 저는 ed25519로 설정하도록 하겠습니다.
###########################
# rsa의 -b 옵션 => 생성할 key의 bit수를 지정
# 각 암호화 타입마다 필요한 비트수가 다릅니다.
# rsa 타입은 최소 768 비트가 필요하고 default로 2048 비트로 설정되어 있습니다.
# 여기서는 두 배 큰 4096으로 더 견고한 키를 만들겠습니다.
# (일반적으로 ssh-key할때 4096으로 많이 하기도 한다.)
###########################
#-C는 주석을 입력할 수 있습니다.
#주석은 서버에 따라 특별한 용도로 사용할 수 있습니다.
#github에서는 사용자의 로그인 ID를 적어놓으라고 가이드합니다.
#############################

# 옵션에 대한 설명은 
# https://storycompiler.tistory.com/112 을 참고하였습니다.

```

![스크린샷 2021-12-22 오후 6.53.34.png](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2021-12-22_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_6.53.34.png)

위의 코드를 터미널에 입력해주면 중간중간 물어보는 게 나옵니다.
1. 어디 경로에 그리고 이름은 뭘로 만들거야?   Enter file in which to save the key (/Users/계정명/.ssh/ ~~
2. 비밀번호는 따로 설정할거야?  Enter passphrase (empty for no passphrase): ~~ 

![스크린샷 2021-12-22 오후 6.53.48.png](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2021-12-22_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_6.53.48.png)

2-1 한번더 입력해줘  

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%202.png)

1번의 경우 Enter(Mac이므로 return키)를 입력하면 기본경로에 생성되고 2번의 경우 따로 비밀번호 설정 안 할 경우 동일할게 Enter(return)을 입력해주면 된다. (github에서는 비밀번호를 권장하지만 저는 그냥 귀찮음의 문제로 하지 않았으나 중요한게 많으신 분들은 나중에라도 지정이 가능하니 설정하는 걸 추천드립니다.)
그래서 모두 다 입력하면 아래처럼 다 만들어 졌다고 나옵니다.

![스크린샷 2021-12-22 오후 7.05.25.png](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2021-12-22_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_7.05.25.png)

잘 생성되었는지 터미널을 열어 ls -al로 확인해주면 기존에는 없던 .ssh 경로가 생성되었고 그 안에 파일이 있는 것을 볼 수 있습니다.

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%203.png)

.ssh 경로로 이동해보면 id_ed25519 (private key)와 id_ed25519.pub (public key) 2가지가 생성되었음을 알 수 있습니다.( public key와 private key내용이 궁금하신 분들은 위에 설명을 달아놓은 ssh key동작방식을 읽어보세요 )
만약 ed25519 방식으로 Key를 만들어 주었다면 id_ed25519 와 id_ed25519.pub 두 개가 마찬가지로 생성됩니다.

![스크린샷 2021-12-22 오후 7.09.42.png](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2021-12-22_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_7.09.42.png)

3.  발급받은 ssh key를 github에 등록하기

이제 github에 접속할 때 인증을 위해 우리 local(MacOS)의 private key(id_ed25519)와 맞춰볼 public key(id_ed25519.pub)를 github에 등록해주겠습니다.
pubic key내용을 pbcopy 명령어를 통해 클립보드에 복사하겠습니다.

```bash
pbcopy < ~/.ssh/id_ed25519.pub
# 마찬가지로 rsa로 발급 하셨을 땐 아래와 같이 해주면 됩니다.
# pbcopy < ~/.ssh/id_rsa.pub
```

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%204.png)

위처럼 복사한 후 github 홈페이지에 접속해 아래의 경로로 이동해줍니다.

Github의 Settings -> SSH and GPG keys -> New SSH key

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%205.png)

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%206.png)

Title에는 본인이 적고 싶은 것 
Key값에는 위의 pbcopy로 복사해온 내용을 적어주면 됩니다. 
( key값 마지막에 e-mail이 있어야지 github에서 권장하는 내용인데 위의 ssh key발급옵션에서 -C값을 정상적으로 주셨다면 key값에 잘 생성되어 있을 겁니다.)

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%207.png)

Add SSH Key버튼을 눌러주면 

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%208.png)

정상적으로 등록되었습니다. 사실 공개키라 뭐 보여줘도 상관없겠지만 가려주니 한층 비밀스럽게 되었습니다.

4. github에 등록된 키와 통신을 위한 Local(Mac) SSH 설정

먼저 ssh key통신을 위한 접속 설정 방법에는 크게 두가지가 있습니다.

A. ~/.ssh/cofig에 명시적으로 private key값의 정보와 사용자정보( 호스트명 , 사용자이름정보 등)을 적어서 서버와 통신시 자동으로 인증하는 방법.

B. ssh-agent에 private key를 등록해서 ssh-agent가 서버와 접속시 자동으로 public key를 인증하는 방법

이 글에서는 config파일을 명시적으로 작성해줘서 인증하는 방법으로 진행하겠습니다. (github에 여러개의 계정을 사용할 때 이 방법을 사용하는 것을 추천합니다.)

 

위에서 github에 Public Key를 정상적으로 등록했다면 Local(Mac)이 서버(github)와 서로 key를 맞춰볼 때 아래의 순서입니다. 
1. local ( 서버가 아닌 본인 pc)의 ssh-key 발급 (public, private)
2. 발급된 ssh key (Public key)파일은 ssh서버(github)에 등록
3. local에서 ssh서버로 접속할 때 설정해주는 config 파일에 key파일정보기재 
    (config 파일 안에 key파일을 기재해주면 너한테 등록한 내 key파일은 여깄어~라고 알려주게 되고 인증이 된다.)

~./ssh/config 파일을 따로 설정해준 적이 없다면 해당 경로에 만들어줍니다. 

```bash
vi ~/.ssh/config
# vim으로 열면 [i]를 입력해서 입력모드에 들어갑니다.
# 아래 정보 입력 후 [esc] 를 눌러 명령모드 상태로 들어간 후 [:wq]으로 저장 후 종료
####### 본인계정 정보
# Host github.com-sup           {{여러개의 github계정을 사용하시는 분이 아니라면 그냥 github도 상관없습니다}}
#   HostName github.com
#   User git
#   IdentityFile ~/.ssh/id_ed25519    {{{private key파일 위치를 적어주세요}}

# Host : 접속할 정보의 이름입니다. 입력한 정보로 ssh 접속 시 $ssh host명 명령 시 아래 접속 정보로 ssh 접속이 실행됩니다.
# HostName : 접속할 서버의 IP 주소입니다.
# User : 접속할 서버의 user 정보입니다.
# IdentityFile : 인증 키파일이 필요한 경우, 로컬환경의 키파일 경로를 설정합니다. 키파일이 필요 없는 서버의 경우 생략 가능합니다.
# Port : ssh 접속 포트입니다. 생략 가능하며, 생략 시 기본 22번 포트로 실행됩니다.
# 출처:[https://ibks-platform.tistory.com/113](https://ibks-platform.tistory.com/113)
```

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%209.png)

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%2010.png)

저는 현재 세팅을 새로 환경설정하고 있기때문에 git config설정을 따로 해주겠습니다만(git config user.name&email) 이미 되어있으신분들은 remote주소 설정을 해주시면 됩니다. (저같은경우는 여러개의 깃헙계정으로 접속하는 상황을 염두해주었기때문에 remote를 Host명인 github.com-sup로 지정해주었습니다. 여러개의 github계정을 사용하는 경우 당연히 ssh key도 여러개를 발급받기 때문에 Host에 적힌 내용으로 구분해줍니다.)

```bash
git remote add origin git@github.com-sup:Suppppppp/suppppppp.github.io.git
#                     User@ Host : 실제 연결할 github repository
```

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%2011.png)

연결이 잘 되었는지 테스트를 해보겠습니다.

```bash
ssh -T git@github.com-sup # User@Host로 입력해주면됩니다.
```

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%2012.png)

여기서 yes입력해주면 됩니다. 입력해주면 이렇게 successfully authenticated 라는 문구를 보면 성공입니다.

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%2013.png)

이제 특정 repository를 clone해주겠습니다. (이미 git repo가 있는 것을 가정하고 있으므로 없으신분들은 git repo를 만드시면됩니다.)

- git repository가 없을 경우
    
    ```bash
    cd {{git사용 원하는 폴더로 이동}}
    git init
    git remote add origin {{git 주소}}
    git add .
    git commit -m "The first commit" 
    git push -u origin master
    
    ```
    

만약 ssh config설정 시 Host을 github.com으로 했다면 아래처럼 원하는 repo에 ssh부분을 복사하면 됩니다.
그러나 저는 ssh로 여러 github계정을 접속하는 것을 염두해둔 상태로 ssh config를 구성했으므로 Host가 github.com이 아닌 github.com-sup이므로 해당부분을 수정해서 clone을 해주겠습니다.

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%2014.png)

```bash
git clone git@github.com:repository url 
#         User@ Host : Repo.git 입니다.
```

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%2015.png)

정상적으로 연결이 되었습니다. push가 잘 되는지 test라는 내용의 README.md를 만들어 push해보겠습니다.

```bash
echo 'test' > README.md
git add .
git commit -m "Test README"
git push origin master
```

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%2016.png)

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%2017.png)

정상적으로 push가 되었음을 확인했습니다.

사실 코드만 적으면 금방 완료될 글이지만 그래도 왜 하는지는 알고 해야한다는 게 제 생각이라 처음으로 github에 ssh연결하시는 분들이라면 도움이 되셨으면 좋겠습니다.
살펴본 블로그들의 링크를 아래 달아놓겠습니다. 내용은 다 비슷합니다. 혹시나 제가 모르는 게 있을까봐 일부러 많이 블로그들을 살펴봤습니다.
읽어주신 분들 감사합니다.

- ref
    
    

---

---

---

token방식으로 github연결 글 링크

token 방법 공식 docs (영어버전 한국어버전은 없습니다)
[https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) 

개인블로그

[https://hyeo-noo.tistory.com/184](https://hyeo-noo.tistory.com/184)

[https://curryyou.tistory.com/344](https://curryyou.tistory.com/344)

[https://velog.io/@jini_eun/Github-2021년-8월-13일부터-토큰-인증-로그인-변화](https://velog.io/@jini_eun/Github-2021%EB%85%84-8%EC%9B%94-13%EC%9D%BC%EB%B6%80%ED%84%B0-%ED%86%A0%ED%81%B0-%EC%9D%B8%EC%A6%9D-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%EB%B3%80%ED%99%94)

[https://developer0809.tistory.com/148](https://developer0809.tistory.com/148)

[](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%209981d53112604e65a2f6e21d01046e33.md)

![Untitled](Mac%20M1%20github%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%203966ed2428bc48d8b3d94eaf99083b18/Untitled%2018.png)