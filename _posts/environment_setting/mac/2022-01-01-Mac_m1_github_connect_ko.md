---
title: Mac M1 github 연결하기
author: Kyungsup Go (Sup)
date: 2021-01-01 00:00:00 +0900
categories: [Environment setting, Mac M1]

tags: [Mac,MacOS,M1,M1 pro,Apple silicon,github]
toc: True
comments: true
---

# Github 인증방식의 변경

글 작성에 앞서 이 글은 github의 기본적인 작동(?)순서를 알고 있다고 가정하고 설명을 진행합니다.<br>
모르시는 분들은 이 링크([링크1](https://sin0824.tistory.com/8), [링크2](https://kkaeruk.tistory.com/3))의 순서를 참고하세요.<br>순서만 알고 내용을 따라하지는 말으시길 권장합니다 그 이유가 있습니다.

그 이유는 2021년 8월 13일부터 github에 Push할 때 인증방법이 바뀌었습니다.<br>
이전에는 Password로 인증을 진행한 후 push가 가능했지만 이제는 **PAT**(Personal Access Token)와 **SSH key** 방식 2가지로만 가능합니다.  그래서 21년 8월 기준으로 이전 글들을 보시고 따라하시면 push할 때 오류가 생깁니다.<br>아래는 기존에 사용하던 Password방식으로 인증했을 때 나오는 문구입니다.  [공식 github에서 인증방식 변경에 관한 글](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/)

```zsh
remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
remote: Please see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/ for more information.
fatal: unable to access 'https://github.com/userName/repoName.git/': The requested URL returned error: 403
```

# SSH 연결
각각의 방식에 대한 장단점은 아래처럼 정리해 볼 수 있습니다.<br>(실제로 하나의 Mac에서 여러 github을 사용할 경우 ssh를 사용하여 할 수 있습니다.)
![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_0.png){: width="400" height="200"}*[출처](https://blog.neonkid.xyz/277)*<br>
이 글에서는 ssh key 기준으로 github을 연결해보겠습니다.  (token이 편하신 분들을 위해 글 맨 마지막 하단에 잘 설명되어있는 링크들 달아 놓겠습니다.)<br> 
[공식 Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh)에 나와있는 ssh key 연결 방법입니다. <br>
ssh key 연결방법이 영어로 나와 있으므로 불편하실 분들을 위해 저의 방식대로 정리해보겠습니다.

1. 큰 개념인 ssh key 인증방식이 무엇인지 ?
2. ssh key 발급 방법 (ed25519 ,rsa)
3. 발급받은 ssh key를 github에 등록하기
4. github에 등록된 키와 통신을 위한 Local (Mac) 설정
5. 연결확인을 위한 Test
 

순으로 진행하겠습니다. (본인이 이미 진행하신 부분이 있다면 다음부터 보시면 됩니다.) 

## 1. SSH key란??

ssh의 개념은 파고들면 복잡해지기 때문에 간단히 설명해놓은 제 글 링크를 첨부합니다.<br>
좀 더 알고 싶은신분들은 아래 영상을 참고하세요 

<details>
<summary> 📁  생활코딩님의 참고영상 </summary>
<div markdown="1">

<iframe width="750" height="450" src="https://www.youtube.com/embed/qkGaUqlH47s" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

</div>
</details>

ssh key발급에 앞서 기존에 본인도 모르게 key를 발급받은 적이 있을 수 있으므로 발급된 key가 있나 확인해봅니다.<br>ssh key는 보통 ~/.ssh 위치에 저장됩니다. 터미널을 열어 ls(파일목록) 을 보면 `.`경로는 숨겨지기 때문에 ls -al로 조회해보겠습니다.  -al 옵션을 주면 보이게 되는 `.`경로들에 ssh항목이 없으므로 ssh key가 발급된 적이 없는 것으로 확인됩니다.<br>이렇게 보아도 되고 `cd ~/.ssh` 로 이동해서 `id_rsa`와 `id_rsa.pub` 의 파일쌍을 확인해도 됩니다.

![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_1.png)*현재는 .ssh경로가 없습니다.*

## 2. ssh key 발급방법 (ed25519, rsa)

ssh key 파일이 없으므로 발급을 받아주겠습니다.<br> 
ssh key 발급방식에는 여러 옵션이 있습니다. `dsa`,`ecdsa`,`ed25519`,`rsa`,`rsa1`등<br>
저는 암호학 전문가가 아니므로 보통 많이 쓰이는 `ed25519`와 `rsa`방식만 알고 있습니다.<br>일반적으로 ed25519가 지원하면 사용하고 지원하지않으면 rsa방식을 사용하기도 하고 각각의 장단점이 있다.<br>(출처는 다양한 분들의 의견이 있지만 좀 더 차이를 비교해주신 [이 분](https://www.nemonein.xyz/2018/10/1124/)의 글이 신빙성이 있어보인다.)<br>요즘 `ed25519`를 왠만하면 지원하기도 하고 github공식사이트에서도 가급적 `ed25519`방식으로 안내하므로 `ed25519`방식으로 생성하겠습니다. (`rsa` 방식도 크게 다르지 않기 때문에 설명은 같이 달아두겠습니다.)

```zsh
ssh-keygen -t ed25519 -C "your_email@example.com" 
# ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
# 여기서 e-mail은 github가입 이메일을 넣어주세요 
# rsa 쓰실분은 위에코드 사용하여 만들면 됩니다. 
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



![스크린샷 2021-12-22 오후 6.53.34.png](/assets/img/environment_setting/mac/Mac_m1_github_connect/스크린샷_2021-12-22_오후_6.53.34.png)


위의 코드를 터미널에 입력해주면 중간중간 물어보는 게 나옵니다.
1. 어디 경로에 그리고 이름은 뭘로 만들거야?   Enter file in which to save the key (/Users/계정명/.ssh/ ~~
2. 비밀번호는 따로 설정할거야?  Enter passphrase (empty for no passphrase): ~~ 

![스크린샷 2021-12-22 오후 6.53.48.png](/assets/img/environment_setting/mac/Mac_m1_github_connect/스크린샷_2021-12-22_오후_6.53.48.png)

2-1 한번더 입력해줘  

![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_2.png)

1번의 경우 Enter(Mac이므로 return키)를 입력하면 기본경로에 생성되고 2번의 경우 따로 비밀번호 설정 안 할 경우 동일하게 Enter(return)을 입력해주면 됩니다.<br>(github에서는 비밀번호를 권장하지만 저는 그냥 귀찮음의 문제로 하지 않았으나 중요한게 많으신 분들은 나중에라도 지정이 가능하니 설정하는 걸 추천드립니다.)<br>
그래서 모두 다 입력하면 아래처럼 다 만들어 졌다고 나옵니다.

![스크린샷 2021-12-22 오후 7.05.25.png](/assets/img/environment_setting/mac/Mac_m1_github_connect/스크린샷_2021-12-22_오후_7.05.25.png)

잘 생성되었는지 터미널을 열어 ls -al로 확인해주면 기존에는 없던 .ssh 경로가 생성되었고 그 안에 파일이 있는 것을 볼 수 있습니다.

![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_3.png)

ssh 경로로 이동해보면 `id_ed25519` (private key)와 `id_ed25519.pub` (public key) 2가지가 생성되었음을 알 수 있습니다.<br>(***public key***와 ***private key***내용이 궁금하신 분들은 위에 설명을 달아놓은 ssh key동작방식을 읽어보세요 )<br>
만약 `ed25519` 방식으로 Key를 만들어 주었다면 `id_ed25519` 와 `id_ed25519.pub` 두 개가 마찬가지로 생성됩니다.

![스크린샷 2021-12-22 오후 7.09.42.png](/assets/img/environment_setting/mac/Mac_m1_github_connect/스크린샷_2021-12-22_오후_7.09.42.png)

## 3. 발급받은 ssh key를 github에 등록

이제 github에 접속할 때 인증을 위해 우리 ***local***(MacOS)의 ***private key***(`id_ed25519`)와 맞춰볼 <br>***public key***(`id_ed25519.pub`)를 github에 등록해주겠습니다.<br>
pubic key내용을 pbcopy 명령어를 통해 클립보드에 복사하겠습니다.

```bash
pbcopy < ~/.ssh/id_ed25519.pub
# 마찬가지로 rsa로 발급 하셨을 땐 아래와 같이 해주면 됩니다.
# pbcopy < ~/.ssh/id_rsa.pub
```

![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_4.png)
위처럼 복사한 후 github 홈페이지에 접속해 아래의 경로로 이동해줍니다.<br>
`Github의 Settings` ➡️ `SSH and GPG keys` ➡️ `New SSH key`

![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_5.png) | ![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_6.png)

Title에는 본인이 적고 싶은 것 / Key값에는 위의 pbcopy로 복사해온 내용을 적어주면 됩니다.<br> 
( key값 마지막에 e-mail이 있어야지 github에서 권장하는 내용인데 위의 ssh key발급옵션에서 -C값을 정상적으로 주셨다면 key값에 잘 생성되어 있을 겁니다.)

![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_7.png)

Add SSH Key버튼을 눌러주면 

![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_8.png)

정상적으로 등록되었습니다.<br>사실 공개키라 뭐 보여줘도 상관없겠지만 가려주니 한층 비밀스럽게 되었습니다.

## 4. github에 등록된 key와 통신을 위한 Local(Mac) SSH 설정

먼저 ssh key통신을 위한 접속 설정 방법에는 크게 두가지가 있습니다.

> **A.** `~/.ssh/cofig`에 명시적으로 ***private key***값의 정보와 사용자정보(호스트명 ,사용자이름정보 등)을 적어서<br> &nbsp;&nbsp; 서버와 통신시 자동으로 인증하는 방법.<br>
**B.** ssh-agent에 ***private key***를 등록해서 ssh-agent가 서버와 접속시 자동으로 ***public key***를 인증하는 방법

이 글에서는 config파일을 명시적으로 작성해줘서 인증하는 방법으로 진행하겠습니다.<br>(github에 여러개의 계정을 사용할 때 이 방법을 사용하는 것을 추천합니다.)


위에서 github에 Public Key를 정상적으로 등록했다면 Local(Mac)이 서버(github)와 서로 key를 맞춰볼 때 아래의 순서입니다. 
1. local ( 서버가 아닌 본인 pc)의 ssh-key 발급 (public, private)
2. 발급된 ssh key (Public key)파일은 ssh서버(github)에 등록
3. local에서 ssh서버로 접속할 때 설정해주는 config 파일에 key파일정보기재<br>
    (config 파일 안에 key파일을 기재해주면 너한테 등록한 내 key파일은 여깄어~라고 알려주게 되고 인증이 된다.)

`~./ssh/config` 파일을 따로 설정해준 적이 없다면 해당 경로에 만들어줍니다. 

```zsh
vi ~/.ssh/config
# vim으로 열면 [i]를 입력해서 입력모드에 들어갑니다.
# 아래 정보 입력 후 [esc] 를 눌러 명령모드 상태로 들어간 후 [:wq]으로 저장 후 종료
####### 본인계정 정보
# Host github.com-sup           \{여러개의 github계정을 사용하시는 분이 아니라면 그냥 github도 상관없습니다\}
#   HostName github.com
#   User git
#   IdentityFile ~/.ssh/id_ed25519    \{private key파일 위치를 적어주세요\}

# Host : 접속할 정보의 이름입니다. 입력한 정보로 ssh 접속 시 $ssh host명 명령 시 아래 접속 정보로 ssh 접속이 실행됩니다.
# HostName : 접속할 서버의 IP 주소입니다.
# User : 접속할 서버의 user 정보입니다.
# IdentityFile : 인증 키파일이 필요한 경우, 로컬환경의 키파일 경로를 설정합니다. 키파일이 필요 없는 서버의 경우 생략 가능합니다.
# Port : ssh 접속 포트입니다. 생략 가능하며, 생략 시 기본 22번 포트로 실행됩니다.
# 출처:[https://ibks-platform.tistory.com/113](https://ibks-platform.tistory.com/113)
```

![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_9.png)| ![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_10.png)

저는 현재  새로 환경설정을 세팅하고 있기때문에 git config설정을 따로 해주겠습니다만(git config user.name&email)<br>이미 되어있으신분들은 remote주소 설정을 해주시면 됩니다. (저같은경우는 여러개의 깃헙계정으로 접속하는 상황을 염두해주었기때문에 remote를 Host명인 github.com-sup로 지정해주었습니다. 여러개의 github계정을 사용하는 경우 당연히 ssh key도 여러개를 발급받기 때문에 Host에 적힌 내용으로 구분해줍니다.)

```bash
git remote add origin git@github.com-sup:Suppppppp/suppppppp.github.io.git
#                     User@ Host : 실제 연결할 github repository
```

![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_11.png)

## 5. 연결확인을 위한 Test
연결이 잘 되었는지 테스트를 해보겠습니다.

```bash
ssh -T git@github.com-sup # User@Host로 입력해주면됩니다.
```

![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_12.png)

여기서 yes입력해주면 됩니다. 입력해주면 이렇게 successfully authenticated 라는 문구를 보면 성공입니다.

![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_13.png)

이제 특정 repository를 clone해주겠습니다.<br>(이미 git repo가 있는 것을 가정하고 있으므로 없으신분들은 git repo를 만드시면됩니다.)

<details>
<summary> ⚙️ git repository가 없을 경우</summary>
<div markdown="1">

```zsh
cd *git사용 원하는 폴더로 이동*
git init
git remote add origin *git 주소*
git add .
git commit -m "The first commit" 
git push -u origin master

```

</div>
</details>
<br>
만약 ssh config설정 시 Host을 github.com으로 했다면 아래처럼 원하는 repo에 ssh부분을 복사하면 됩니다.<br>
그러나 저는 ssh로 여러 github계정을 접속하는 것을 염두해둔 상태로 ssh config를 구성했으므로<br> Host가 github.com이 아닌 github.com-sup이므로 해당부분을 수정해서 clone을 해주겠습니다.

![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_14.png)

```bash
git clone git@github.com-sup:repository url 
#         User@ Host : Repo.git 입니다.
# 근데 -sup이없어도 github으로 되긴합니다.
```

![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_15.png)


정상적으로 연결이 되었습니다. push가 잘 되는지 test라는 내용의 README.md를 만들어 push해보겠습니다.

```bash
echo 'test' > README.md
git add .
git commit -m "Test README"
git push origin master
```

![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_16.png)
![Untitled](/assets/img/environment_setting/mac/Mac_m1_github_connect/Untitled_17.png)

정상적으로 push가 되었음을 확인했습니다.

사실 코드만 적으면 금방 완료될 글이지만 그래도 왜 하는지는 알고 해야한다는 게 제 생각이라 처음으로 github에 ssh연결하시는 분들이라면 도움이 되셨으면 좋겠습니다.
살펴본 블로그들의 링크를 아래 달아놓겠습니다. 내용은 다 비슷합니다.
<br>혹시나 제가 모르는 게 있을까봐 일부러 많이 블로그들을 살펴봤습니다.
<br>틀린 내용이 있을 경우 댓글로 남겨주시면 감사드리겠고 또한 지금까지 읽어주신 분들 감사드립니다.

---
---
# 참고
- 📚 ref
>
[https://www.lainyzine.com/ko/article/creating-ssh-key-for-github/](https://www.lainyzine.com/ko/article/creating-ssh-key-for-github/)<br>
[https://medium.com/@sunnkis/github-ssh-를-활용하여-여러-계정-관리-방법-7ec29bd0186d](https://medium.com/@sunnkis/github-ssh-%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%98%EC%97%AC-%EC%97%AC%EB%9F%AC-%EA%B3%84%EC%A0%95-%EA%B4%80%EB%A6%AC-%EB%B0%A9%EB%B2%95-7ec29bd0186d)<br>
[https://velog.io/@igotoo/github-접속을-https에서-ssh-접속으로-변경하기](https://velog.io/@igotoo/github-%EC%A0%91%EC%86%8D%EC%9D%84-https%EC%97%90%EC%84%9C-ssh-%EC%A0%91%EC%86%8D%EC%9C%BC%EB%A1%9C-%EB%B3%80%EA%B2%BD%ED%95%98%EA%B8%B0)<br>
[https://triplexlab.tistory.com/105](https://triplexlab.tistory.com/105)<br>
[https://bbaktaeho-95.tistory.com/101](https://bbaktaeho-95.tistory.com/101)<br>
[https://jintelli.tistory.com/34](https://jintelli.tistory.com/34)<br>
[https://cfdf.tistory.com/20](https://cfdf.tistory.com/20)<br>
[https://cresumerjang.github.io/2020/11/15/multiple-GitHub-accounts-on-a-single-machine-with-SSH-keys/](https://cresumerjang.github.io/2020/11/15/multiple-GitHub-accounts-on-a-single-machine-with-SSH-keys/)<br>
    
---

- 📚 token방식으로 github연결 글 링크

> [token 방법 공식 docs (영어버전 한국어버전은 없습니다)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)<br>
>⬇️개인블로그<br>
[https://hyeo-noo.tistory.com/184](https://hyeo-noo.tistory.com/184)<br>
[https://curryyou.tistory.com/344](https://curryyou.tistory.com/344)<br>
[https://velog.io/@jini_eun/Github-2021년-8월-13일부터-토큰-인증-로그인-변화](https://velog.io/@jini_eun/Github-2021%EB%85%84-8%EC%9B%94-13%EC%9D%BC%EB%B6%80%ED%84%B0-%ED%86%A0%ED%81%B0-%EC%9D%B8%EC%A6%9D-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%EB%B3%80%ED%99%94)<br>
[https://developer0809.tistory.com/148](https://developer0809.tistory.com/148)<br>
