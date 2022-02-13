---
title: Mac M1 Github blog를 위한 @1 Jekyll이란?(feat. 블로그 환경세팅을 위한 순서)
author: Kyungsup Go (Sup)
date: 2021-01-01 05:00:00 +0900
categories: [Resume, Blogging]
tags: [Jekyll, Github blog]
toc: True
comments: true
---


# Mac M1 Github blog를 위한 #1 Jekyll이란? <br>(feat. 블로그 환경세팅을 위한 순서)


Macbook M1 pro를 구입 후 여러 개발환경을 세팅하면서 jekyll활용한 블로그 환경도 세팅을 해주는 김에 기록하게 되는 글입니다.
아마 이 글을 읽으시는 분들은 2가지 타입이실 것 같습니다.<br>
- M1에 ruby설치 과정중에 어려움을 겪으신 분들
- 아예 처음 jekyll을 활용한 블로그를 시도해보시는 분들.<br>

이 글은 여러 페이지로 나눠서 작성하고 두 가지를 포괄적으로 합쳐서 쓸 예정이니 필요하신 정보를 잘 보시면 될 것 같습니다.<br>
각각의 자세한 설명에 초점을 맞추진 않을 것입니다. 그러나 글을 작성할 때 늘 제 목적은 왜 이것을 해야하는 지 이유를 알아야된다고 생각하기 때문에 실제 동작과 그 이유에 초점을 맞춰 진행하겠습니다.

큰 흐름의 순서를 살펴보면,
- <span style ="color : #4169E1">**A.**</span> Ruby설치
- <span style ="color : #4169E1">**B.**</span> Jekyll 과 bundler 설치
- <span style ="color : #4169E1">**C.**</span> 사용할 Jekyll 테마 다운로드
- <span style ="color : #4169E1">**D.**</span> github에 repository생성 및 Local 폴더에 테마를 github 페이지에 연동


# Jekyll이란 ?

Jekyll이란 말이 자주 나오는데 Jekyll을 구글에 치면 아래처럼 설명이 나옵니다.<br>
**” Jekyll은 정적 사이트 생성기입니다. <br>GitHub의 공동 설립자인 Tom Preston-Werner가 Ruby로 작성했으며 오픈 소스 MIT 라이선스에 따라 배포됩니다. “** 
<br>Ruby로 만들어진 정석 사이트 생성기라고 하는것인데 왜 우리가 <span style ="color : #4169E1">**A.**</span>에서 Ruby를 설치해야되는 지가 나옵니다.<br>
블로그 페이지를 생성해주는 생성기 자체가 Ruby란 언어로 만들어졌기 때문입니다. 
정적 사이트 생성기라면 동적 사이트 생성기가 있다는 생각을 할 수 있는데 각 세부사항의 자세한 설명은 이 글의 목적이 아니므로 간단히 아래에 설명을 달고 넘어가겠습니다.<br>(이후에도 같은방식으로 전개하겠습니다. )

![Untitled](/assets/img/resume/blogging/compare_webpage.png)_출처 : [https://titus94.tistory.com/4](https://titus94.tistory.com/4)_

쉽게 말해 쇼핑몰처럼 우리가 클릭이나 입력처럼 어떤 액션을 취하지 않고 서버와 주고받는 것 없이 고정되어있는 글들을 보는 것만 하는 것은 정적 사이트라고 보시면 됩니다. 
이런 정적 사이트를 생성해주는 Jekyll을 사용하기 위해서 위에서 언급해준 것과 같이 Ruby를 설치해줘야합니다.
다음 글에서는 Ruby설치방법과 MacOS에서의 원활한 Ruby설치를 위한 프로그램을 알아보겠습니다.
