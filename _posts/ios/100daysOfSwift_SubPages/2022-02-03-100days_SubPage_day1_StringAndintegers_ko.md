---
title: (100days Of Swfit) Day1 String and Integers 번역
author: Kyungsup Go (Sup)
date: 2022-02-03 02:01:00 +0900
categories: [IOS, 100days Of Swfit - Subpages]

tags: [ios, (100days Of Swfit) String and Integers]
toc: True
comments: true
---

100days_SubPage_day1_StringAndintegers_ko

<iframe width="700" height="400" src="https://www.youtube.com/embed/ZU3JDkjvn3w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


https://suppppppp.github.io/posts/100days_SubPage_day1_StringAndintegers_ko/

Swift는 모든 변수가 하나의 명확한 타입을 가져야만하는 typs-safe 언어로 알려져있습니다.
Xcode가 우리를 위해 만들어준 <span style ="color : #e6196b">**Str**</span> 변수는 "Hellow, playground" 철자를 가진 문자열을 보유하고 있으므로 Swift는 <span style ="color : #e6196b">**String**</span> 타입을 할당합니다. 

반면에, 만약 우리가 누군가의 나이를 저장하길 원한다면 우리는 변수를 이렇게도 만들 수  있습니다. :
```swift
var age = 38
```

이 변수는 숫자를 가지는데 Swift는 <span style ="color : #e6196b">**Int**</span> 타입을 할당합니다 - "integer"를 줄인겁니다.


만약 당신이 큰 숫자를 넣는다면, Swift는 천단위 구분자로 "_"를 사용할 수 있습니다. - 이것은 숫자를 바꾸지 않지만 더 쉽게 읽을 수 있습니다.(가독성측면)<br>
예를 들어:
```swift
var population = 8_000_000
```
(이렇게 입력했을 때 아래 비교사진을 보면 변수 할당시 _를 사용했지만 실제 할당되는건 8000000으로 둘이 같습니다.)

![int참고](/assets/img/ios/100daysOfSwift_SubPages/day1/int_compare.png)

Strings와 intergers는 다른 타입이고 서로 섞어 쓸 수 없습니다. 그래서  <span style ="color : #e6196b">**str**</span> 을 "Goodbye"로 바꾸는 것은 안전하지만 38로 바꿀수는 없습니다. 왜냐하면 <span style ="color : #e6196b">**Int**</span> 는 <span style ="color : #e6196b">**String**</span> 이 아니기 때문입니다.<br>

---
---

__코드로 부연설명__

```swift
var str = "Hello, playground" //에서
 str = "Goodbye" //로 바꾸는 것은 같은 str이라서 안전하지만

str = 38 //로 바꾸는 것은 String에서 -> Integer 타입으로 바꾸는 것이기 때문에 불가능하다.
```

## 돌아가기

[⬅️Day 1 돌아가기](https://suppppppp.github.io/posts/100days_MainPage_day1_ko/)<br>
[🏠Main page 돌아가기](https://suppppppp.github.io/posts/100days_MainPage_ko/)

