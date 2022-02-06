---
title: (100days Of Swfit) Day1 Str&Int - Option 번역
author: Kyungsup Go (Sup)
date: 2022-02-03 02:02:00 +0900
categories: [IOS, 100days Of Swfit - Subpages]

tags: [ios, (100days Of Swfit) Day 1 , Option - Why is Swift a type-safe language?]
toc: True
comments: true
---

# Why is Swift a type-safe language?
Xcode 13.2버전으로 업데이트됨


Swift는 Strings와 integers로서 변수를 만들게 해주지만 다른 많은 데이터의 타입들도 있습니다. <br>
당신이 변수를 만들 때 Swift는 당신이 할당한 데이터가 어떤 종류인지에 따라서 어떤 타입의 변수인지 알 수 있고, 그 때 변수는 항상 한가지의 특정한 타입을 가질 것입니다.

예를 들면,아래는 42와 동일한 <span style ="color : #e6196b">**meaningOfLife**</span> 라는 변수가 생성됩니다. :
```swift
var meaningOfLife = 42
```

왜냐하면 <span style ="color : #e6196b">**meaningOfLife**</span> 의 초기값으로 우리는 42를 할당했기 때문에 Swift는 Type을 integer로 할당할 것입니다.<br>
이것은 우리가 필요할 때마다 값을 자주 바꿀 수 있는 변수이지만, type을 바꿀 수는 없습니다. :<br>이것의 type은 항상 Integer일 것입니다.

이것은 App을 만들 때 매우 유용합니다. 왜냐하면 Swift는 우리의 데이터에 실수하지 않도록 확실히 할 것이기 때문입니다.<br>예를 들어 우리는 이렇게 쓸수 없습니다.:
```swift
meaningOfLife = "Forty two"
```
비록 우리가 명백한 실수를 하는 것은 거의 없지만, 당신은 이 type safety(타입 안정성)가 Swift로 코드를 작성하는 날마다 도움을 주는 것을 알게 될 것입니다.

셍긱해보세요 : 변수를 하나 만들고 그 변수에 명백하게 실패할 타입을 변화시키려고 합니다.<br>(잘못된 변환을 하려고 한다고 가정)<br>
하지만 당신의 프로그램이 크기가 커지고 복잡성이 증가함에 따라, 매번 당신의 머리안에 변수들의 타입을 외우고 있는 것이 불가능하게 됩니다. 그래서 대신에 Swift로 효과적으로 변환시키고 있습니다.  

# 돌아가기 

[⬅️Day 1 돌아가기](https://suppppppp.github.io/posts/100days_MainPage_day1_ko/)<br>
[🏠Main page 돌아가기](https://suppppppp.github.io/posts/100days_MainPage_ko/)
