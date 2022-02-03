---
title: (100days Of Swfit) Day1 Variables 번역
author: Kyungsup Go (Sup)
date: 2022-02-02 01:01:00 +0900
categories: [IOS, 100days Of Swfit - Subpages]

tags: [ios, (100days Of Swfit) Day 1_Var]
toc: True
comments: true
---

<iframe width="700" height="400" src="https://www.youtube.com/embed/kohIy64THOo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


(아래 글은 영상에 대한 자막이므로 리스닝이 힘드실 경우 아래를 보시면 됩니다.)<br>

Xcode를 실행할 때 무엇을 하고 싶은지 물어보는데 ~~“Get Started with a Playground”~~를 선택해주면 됩니다.<br>
(영상의 버전은 9.2버전으로 현재 Xcode버전과는 동떨어져 있어서 13.2버전기준으로 추가 설명과 사진을 넣어놓겠습니다.)
<details>
<summary> Xcode설치 및 13.2버전 playground열기 </summary>
<div markdown="1">

100days에서처럼 App stroe에서 Xcode를 설치하는 것이 아니라 공식 홈페이지에서 다운방법은 예전 제 글을 [참고](https://suppppppp.github.io/posts/Mac_M1_-Xcode_install(Not_in_App-Store!!)_ko/)해주세요.

# Playground 여는 방법
![open](/assets/img/ios/100daysOfSwift_SubPages/day1/open.png)
</div>
</details>
-- 이것은 Swift 코드를 입력하고 즉각적으로 결과를 볼 수 있는 Sandbox입니다.<br>

기본 값(default)은 ios용 비어있는 playground로 next를 클릭해서  만들고 당신의 desktop에 저장하세요.<br>


이 동영상에서 프로그램 데이터를 저장할 수 있는 변수(Variable)를 소개하겠습니다.
이것들은 변수(Variable)라고 불립니다. 왜냐하면 변수들은 다양하기 때문입니다. -- 당신은 변수 값들을 자유롭게 바꿀 수 있습니다.


Playgrounds는 변수를 만드는 코드 명령줄과 함께 시작합니다.:
```swift
var str = "Hello, playground"
```

그러면 `str`이라는 변수(variable)이 만들어지고 *"Hello, Palyground"*라는 값이 지정됩니다.<br>
playground 오른쪽에 있는 결과 출력창(ouput area)에 *“Hello, playground”*를 볼 수 있습니다 - 이것은 값(value)이 설정된 것을 보여주는 Xcode입니다.


왜냐하면 `str`은 우리가 변하게 할 수 있는 변수입니다.
```swift
str = "Goodbye"
```

2번째에서는 `var`가 필요없는데 변수(**var**)가 이미 만들어졌기 때문입니다. - 그냥 바꾸기만 하면됩니다.