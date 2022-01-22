---
title: Mac M1에 git 설치하기
author: Kyungsup Go (Sup)
date: 2021-01-01 00:00:00 +0900
categories: [Environment setting, Mac M1]

tags: [Mac,MacOS,M1,M1 pro,Apple silicon,git]
toc: True
comments: true
---

Window에서 M1으로 넘어오고 하나씩 필수적인 것들을 설치하고 있는데 이번엔 git을 설치하겠습니다.<br>
git은 먼저 Homebrew를 통하여 설치하는 것을 추천드립니다.<br>
Homebrew라는 것을 설치하기 싫으실 분이 계실 수도 있는데 아래의 사진에서처럼 공식홈페이지에서도 Homebrew를 설치하라고 말하고 있으니 안정적인 멘탈유지를 위해 시키는대로 설치 해줍니다.<br>
설치방법은 예전에 작성한 설치글을 링크로 남겨드립니다.<br> 
[Homebrew 설치](https://suppppppp.github.io/posts/Mac_m1_Homebrew_Install_ko/)

(참고로 IOS개발을 위한 IDE인 Xcode를 설치할 경우는 사진에 나와있듯이 git이 자동으로 설치됩니다.<br>내장이 올바른 표현일 수도 있겠습니다. 그렇기 떄문에 이미 Xcode부터 설치하신분이라면 터미널에 `git —version`을 입력하시면 자신도 모르는 git이 이미 설치되어 있을 수 있습니다.) 

![Untitled](/assets/img/environment_setting/mac/Mac_m1_git_install/Untitled_0.png)


Homebrew를 설치하였다면 git 공식 홈페이지에서 안내하는대로 Homebrew를 사용하여 설치해줍니다.

```zsh
brew install git
```

터미널에 git —version을 입력해보면 정상적으로 설치가 되었습니다.

![Untitled](/assets/img/environment_setting/mac/Mac_m1_git_install/Untitled_1.png)


github 연결은 다음 글을 참고해주세요.

[다음글](https://suppppppp.github.io/posts/Mac_m1_github_connect_ko/)