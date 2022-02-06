---
title: (100days Of Swfit) Day1 Why does Swift have variables? 번역
author: Kyungsup Go (Sup)
date: 2022-02-03 01:02:00 +0900
categories: [IOS, 100days Of Swfit - Subpages]

tags: [ios, (100days Of Swfit) Day 1 Opt Why does Swift have variables?]
toc: True
comments: true
---

# Why does Swift have variables?

(Swift는 왜 변수variable을 가질까?)<br>
Xcode 13.2버전으로 업데이트 됨

변수들은 우리의 프로그램의 임시적인 정보를 저장할 수 있게 해주며 거의 모든 Swsift프로그램의 핵심부분을 구성합니다.<br>
궁극적으로, 당신의 프로그램은 어떻게든 데이터를 변화시킬 것입니다. :<br>
아마 사용자에게 todo list 기능을 입력하게 한 후 그것들의 check를 꺼버릴 수도 있고,
자본주의 너구리를 무인도에서 배회하게 할 수 도 있고(동물의 숲이란 게임을 비유한 것입니다.),
장치의 시간을 읽고 시계에 표시할 수도 있습니다.<br>
어쨌든,당신은 어떤 종류의 데이터를 가져와서 어떻게든 변환해서 사용자에게 보여주는 것입니다.
<br>

물론, "어떤방식으로든 변환해서"는 진정한 마법이 일어나는 부분인데, 왜냐하면 그 부분이 당신의 기발한 app idea가 일어나는 부분이기 때문입니다.
하지만 메모리에 데이터를 저장하는 프로세스는--(사용자가 입력한 내용이나,인터넷으로부터 다운받은 무언가를 보관하는 것)--변수가 필요한 내용입니다.

당신이 `var`를 사용해서 변수를 만들면, `var`를 다시 사용할 필요없이 원하는 만큼 바꿀 수 있습니다.<br>
예를 들면:
```swift
var favoriteShow = "Orange is the New Black"
favoriteShow = "The Good Place"
favoriteShow = "Doctor Who"
```
만약 `var`를 읽을 때 "새로운 변수만들기"로서 `var`를 읽는 것이 도움이 된다면 그렇게 읽어보세요.<br>
그래서 위의 첫번째  라인은 "***favoriteShow***라는 새로운 변수 만들고 *Orange is the New Black*이라는 값을 넣어주기"로서 읽을 수 있습니다.
line 2과 line 3은 `var`를 가지지 않고 새로운 변수를 만들기보다 존재하는 값을 최신화합니다.<br>


이제 상상해보세요. 당신은 3개의 모든 line에 `var`를 가졌습니다.(`var` ***favoriteShow*** 를 각 line에 사용했다고 가정합니다.)<br>말이 되지 않을 것입니다, 왜냐하면 첫번째 시도 후에는 명백하게 새로운 변수가 아니므로 "`favoriteShow`라는 새로운 변수 만들기 "를 3번 말하는 것은 말이 안되기 때문입니다.
Swift는 당신이 변수에대해 다른 이름을 고를때까지 코드가 실행되되지 않도록 error로 표시할 겁니다.


이건 짜증나는 행동일지도 모르지만 절 믿으세요 : 이건 매우 유용합니다! Swift는 다음처럼 당신한테 명백하게 하길 원합니다: 기존에 존재하는 변수에 대해 수정하려고 합니까? (만약 그렇다면 2번째와 그 후에`var`제거), 또는 새로운 변수를 생성하려고 합니까? (여기서는 변수를 다른 이름으로 )

마지막 1가지 : 비록 대부분의 변수가 Swift프로그램의 핵심을 구성할지라도, 당신은 때떄로 변수들을 가장 피해야한다는 것을 배울 것입니다. 자세한 내용은 나중에 더 하겠습니다. 
<br><br>

[⬅️Day 1 돌아가기](https://suppppppp.github.io/posts/100days_MainPage_day1_ko/)<br>
[🏠Main page 돌아가기](https://suppppppp.github.io/posts/100days_MainPage_ko/)