---
title: Mac M1용 VScode 설치 & 터미널에서 code로 열기
author: Kyungsup Go (Sup)
date: 2022-01-01 00:00:05 +0900
categories: [Environment setting, Mac M1]

tags: [Mac,MacOS,M1,M1 pro,Apple silicon,VScode]
toc: True
comments: true
---

# 1. VScode 설치방법

VScode는 개발자들이 필수적으로 쓰는 IDE의 한 종류일 겁니다.<br>
Window만 사용하다 M1으로 전향했으므로 VScode를 다운로드 해주겠습니다.<br>(저처럼 Window를 사용하다 처음 맥북을 써보시는 분들 기준으로 글을 쓰겠습니다. ) 

VScode 다운로드 방법은 크게 2가지 입니다.<br>
> ***A***. 맥북용 패키지관리자인 Homebrew를 사용해 터미널로 다운로드 하기<br> 
***B***. 공식홈페이지에서 Apple Silicon용 download하기

# 2. 설치

## A. Homebrew를 통한 설치
먼저 ***A***는 빠르고 간단합니다.<br>다만 Homebrew를 모르시는 분들이 있을 수 있으므로 링크의 제 글을 참고해주세요 ➡️
[Homebrew설치](https://suppppppp.github.io/posts/Mac_m1_Homebrew_Install_ko/)
Homebrew설치가 끝났다면 터미널 상에서 아래의 한 줄을 입력해주면 설치가 완료됩니다.<br>
(brew는 `—-cask`는 기본으로 되어있어도 생략해도 되나 그냥 써줬습니다.)

```bash
brew install --cask visual-studio-code
```

## B. 공식홈페이지에서 Apple Silicon용 Download

***B***는 homebrew를 설치하기 싫으실 경우 직접 홈페이지에서 다운로드 방법입니다.<br>
구글에서 vscode를 검색 후 홈페이지를 들어가면 우상단에 Download늘 눌러줍니다.<br>그러면 Aplle silicon용 download가 있습니다.

![Untitled](/assets/img/environment_setting/mac/Mac_M1_VScode_install&_terminalOpen/Untitled_0.png)

이것을 다운로드 해줍니다. 다운로드 압축풀어주고 실행해주면 됩니다.

![Untitled](/assets/img/environment_setting/mac/Mac_M1_VScode_install&_terminalOpen/Untitled_1.png) | ![Untitled](/assets/img/environment_setting/mac/Mac_M1_VScode_install&_terminalOpen/Untitled_2.png) | ![Untitled](/assets/img/environment_setting/mac/Mac_M1_VScode_install&_terminalOpen/Untitled_3.png)

VScode가 열리면 아래처럼 초기 설정에 필요한 설정을 해주고 실행하시면 됩니다.

![Untitled](/assets/img/environment_setting/mac/Mac_M1_VScode_install&_terminalOpen/Untitled_4.png)

사실상  VScode를 설치하는 데 큰 어려움은 없으나 M1용 프로그램을 다운받아야된다~가 중요 포인트입니다.

# 3. 터미널에서 code로 열기 설정

Window의 경우 cmd에서 VScode를 열 수 있는데 이것을 맥북에 적용하는 방법입니다.<br>
왜 window에서는 자동으로 되는데 Mac에서는 따로 설정해줘야하는지가 궁금하신 분들은 여기를 보세요 
<details>
<summary> 💡 여기 </summary>
<div markdown="1">

Visual Studio Code를 터미널에서 실행하기 위해서는 `code` 명령어의 PATH 설정을 해야합니다. 윈도우의 경우 인스톨러로 설치할 때 PATH 설정을 진행합니다만, 맥에서는 단순히 복사만으로 설치가 되기 때문에 PATH가 기본적으로 설정되어있지 않습니다. 윈도우에서도 PATH 설정을 체크하지 않았다면 `code` 명령어를 사용할 수 없습니다. - [출처](https://www.lainyzine.com/ko/article/how-to-execute-visual-studio-code-from-terminal/)

</div>
</details>


이 글에서는 Mac에 code 명령어를 PATH에 추가하고 터미널에서 실행하는 방법에 대해서 알아봅니다.<br>
먼저 위에서의 설명과 같이 Path를 잡지 않았다면 Mac터미널 상에서 `code`를 입력했을 때 아래와 같이<br> `not found`가 나옵니다.

![Untitled](/assets/img/environment_setting/mac/Mac_M1_VScode_install&_terminalOpen/Untitled_5.png){: width="400" height="200"}

이제 Path설정을 해주겠습니다.

1. `cmd` + `shift` + `p`를 눌러주고 생겨난 빈칸에 code를 입력해 줍니다.
2. Shell Commnad: install ‘**code**’~~~ 부분을 클릭해줍니다.


![Untitled](/assets/img/environment_setting/mac/Mac_M1_VScode_install&_terminalOpen/Untitled_6.png)

그럼 아래처럼 나오는데 ok를 눌러줍니다. 일련의 과정들을 물 흐르듯 ok와 확인을 눌러줍니다. 

![Untitled](/assets/img/environment_setting/mac/Mac_M1_VScode_install&_terminalOpen/Untitled_7.png) | ![Untitled](/assets/img/environment_setting/mac/Mac_M1_VScode_install&_terminalOpen/Untitled_8.png) | ![Untitled](/assets/img/environment_setting/mac/Mac_M1_VScode_install&_terminalOpen/Untitled_9.png)

***Successfully installed in Path***라고 하니 터미널을 열어 `code -v`를 입력해보겠습니다.

![Untitled](/assets/img/environment_setting/mac/Mac_M1_VScode_install&_terminalOpen/Untitled_10.png){: width="400" height="200"}

정상적으로 버전이 나오고 code만 입력하면 VScode가 오픈됩니다. 

## 💡 Tip
```zsh
code {실행할 폴더명} # 이렇게 입력하면 해당 폴더경로로 VScode가 열립니다.
```