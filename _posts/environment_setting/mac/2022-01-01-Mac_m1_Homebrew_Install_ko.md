---
title: Mac M1 Homebrew 설치
author: Kyungsup Go (Sup)
date: 2021-01-01 00:00:00 +0900
categories: [Environment setting, Mac M1]

tags: [Mac,MacOS,M1,M1 pro,Apple silicon]
toc: True
comments: true
---

# Mac m1 Homebrew 설치


window만 열심히 사용해오던 저는 MacBook m1 pro를 구입했습니다.　
<br>정말.. 정말 윈도우랑 많이 달라서 열심히 적응해 나가는 중에 개발환경세팅을 위해 많은 글들을 찾아보았는데 그 중 필수적으로 깔아야하는게 Homebrew라고 합니다. 
<br>일반적으로 Apple생태계에서 프로그램 설치는 App store에서 설치 또는 해당 프로그램 사이트에 직접 방문하여 다운로드 받아 파일로 설치인데  Homebrew는 이것을 터미널에서 가능하게 해주고 각종 패키지를 관리할 수 있는 좋은 프로그램입니다. (파이썬 유저라면 pip install 느낌으로 생각하시면 될 것 같습니다.) 

Apple Silicon( 흔히 말하는 m1)용 Homebrew는 2021년 2월 경 3.0.0부터 정식지원한다고 발표했기 때문에<br>글을 쓰는 현재 (21년 12월 12일)버전은 따로 고민해줄 필요없이 홈페이지에서 다운받아 진행해주면 됩니다. 구글링을 해보니 예전 Homebrew버전(3.0.0미만)을 m1용 으로 사용하려면 Rosetta 2를 사용해 인텔버전으로 사용하는 방법으로 했던 것 같습니다. 
현재 홈페이지 최신버전을 설치해본 결과 구글링하면 나오는 Homebrew의 문제점이 발생하지 않으니 m1의 경우 그대로 진행하셔도 무방할 듯 합니다.

이상의 설명은 거두절미하고 Homebrew를 설치해보겠습니다.<br>
[https://brew.sh/](https://brew.sh/)   공식 홈페이지로 들어가줍니다. 

![Untitled](/assets/img/environment_setting/mac/Mac_m1_Homebrew_Install/Untitled.png){: width="400" height="200"}

들어가게 되면 언어가 english로 되어있는데 한국어로 변경이 가능하니 불편하신 분들은 바꿔주시면 되겠습니다.
Install Homebrew 아래의 명령어가 있는데 맨 오른쪽 버튼을 누르면 자동으로 복사가 됩니다. 이 복사된 내용을 터미널에 입력해줍니다.

![Untitled1](/assets/img/environment_setting/mac/Mac_m1_Homebrew_Install/Untitled_1.png)

터미널은 spotlight(`Cmd`+`Space bar`)로 터미널을 검색하면 들어갈 수 있습니다.  붙여넣기는 `Cmd` + `V` 입니다. 

![Untitled](/assets/img/environment_setting/mac/Mac_m1_Homebrew_Install/Untitled_2.png)

입력하고  리턴(엔터)를 눌러주면 아래처럼 mac 관리자 패스워드를 입력해주라고 나옵니다
<br>

![Untitled](/assets/img/environment_setting/mac/Mac_m1_Homebrew_Install/Untitled_3.png)

![Untitled](/assets/img/environment_setting/mac/Mac_m1_Homebrew_Install/Untitled_4.png)

다시 리턴키를 눌러주면  아래처럼 진행됩니다. 몇 분정도가 소요되니 기다려주세요 

![Untitled](/assets/img/environment_setting/mac/Mac_m1_Homebrew_Install/Untitled_5.png){: width="500" height="300"}

중간에 이렇게 비빌번호를 입력해달라고 나옵니다. 다시입력해줍니다.

![Untitled](/assets/img/environment_setting/mac/Mac_m1_Homebrew_Install/Untitled_6.png){: width="500" height="300"}

설치가 완료되면 아래처럼 나옵니다.
그런데 Warning부분을 읽어보면 Path가 문제가 있다고 알려줍니다. 그래서 Next step에 있는 Path를 그대로 복사해서 입력후 리턴(엔터)을 눌러줍니다

![Untitled](/assets/img/environment_setting/mac/Mac_m1_Homebrew_Install/Untitled_7.png){: width="500" height="300"}

![Untitled](/assets/img/environment_setting/mac/Mac_m1_Homebrew_Install/Untitled_8.png){: width="500" height="300"}

위의 작업들이 정상적으로 끝났다면 아래와 같이 다시 터미널을 켜고 Homebrew버전을 확인해줍니다.

![Untitled](/assets/img/environment_setting/mac/Mac_m1_Homebrew_Install/Untitled_9.png){: width="500" height="300"}
<br>정상적으로 Homebrew설치를 마쳤습니다.


>참고<br>
>homebrew path관련 자세한 설명이 궁금하신 분들은 아래 블로그를 참고하시면 됩니다.
><br>[Path참고](https://www.lainyzine.com/ko/article/how-to-install-homebrew-for-m1-apple-silicon/#%EC%95%A0%ED%94%8C-%EC%8B%A4%EB%A6%AC%EC%BD%98m1-%EC%9A%A9-homebrew-%EC%84%A4%EC%B9%98-%EB%B0%8F-%ED%99%95%EC%9D%B8)