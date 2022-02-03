---
title: (100days Of Swfit) Main page 번역
author: Kyungsup Go (Sup)
date: 2022-02-01 01:01:00 +0900
categories: [IOS, 100days Of Swfit - Days N]

tags: [ios, 100days Of Swfit]
toc: True
comments: true
---

IOS를 공부하기로 마음먹으면서 자료조사를 해보았고 여러 자료들을 추천하는 글들을 보았습니다.<br>
그 중 유투브나 여러 자료들을 보았지만 ios에 완전히 처음인 저는 체계적인 공부방식이 필요했고 다양한 자료들 중 <br>몇 가지를 찾았습니다. 

이 100days of Swift는 그 중 1가지로 기초부터 체계적으로 하루에 1개씩 공부하게 만들어졌으며 개념과 퀴즈가 같이 있고 무료라는 점이 좋았습니다. 물론 영어는 힘이 들지만 어차피 개발을 공부하는 사람은 영어와 뗄 수가 없으므로 이번 기회에 굳어졌던 영어공부도 하는 겸해서 진행해보려 했습니다.

개인이 만든 사이트이기 때문에 부족한 내용과 보충 설명이 필요한 내용은 swift공식문서와 병행하면서 같이 보았습니다. 

단순히 공부를 하는 것보다 직접 번역을 하는 것이 제게 더 좋을 것 같아 번역을 하며 공부를 할 목적으로 글을 작성하게 되었습니다. 좋지 않은 영어실력으로 인해 오역될 수 있으므로 잘못된 점을 발견할 경우 가감없이 말씀해주시면 수정하도록 하겠습니다. 
그럼 시작하도록 하겠습니다.

---
---

# [Main Page](https://www.hackingwithswift.com/100)

<iframe width="560" height="315" src="https://www.youtube.com/embed/RB5nWzdl-b8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# How it works

100 Days of Swift에 오신 것을 환영합니다.<br>
여기는 Hacking with Swift에 대한 제 작업들에서 가져온 동영상, 튜토리얼, 테스트등의 무료 모음집이고 여러분이 swift를 배울 수 있게 설계되었습니다.<br>
실제 iOS 앱을 빌드하는 방법을 배우고 싶지만 목표를 달성하는 데 도움이 될 수 있는 좋은 무료 코스를 찾는 데 어려움을 겪는 초보자를 대상으로 합니다. <br>
만약 당신이라면 환영합니다. - 당신의 진짜 모습<sup id="a1">[1](#f1)</sup>을 IOS세계를 보여줄 준비가 되어있기를 바랍니다.


## Rules

만약 이 과정을 성공적으로 완주하길 원한다면 딱 2가지만 지키세요
1. 매일 1시간씩 Swift 튜토리얼을 보거나 읽고 아니면 Swift 코드를 작성하세요
2. 당신이 선택한 Social media(facebook, twitter 등)에 당신에 진행상황을 포스팅하세요. 사람들에게 얘기하세요!

저는 따라가는 데 필요한 모든 자료를 제공할테니, 당신이 할일은 배울 준비된 상태로 나타나기만 하면 됩니다.

## Tips



Swift를 배우려고 시도했다가 실패하는 많은 사람들을 자주 만나왔습니다. 만약 당신이 여기에 해당한다면 이미 잘못된 시작을 몇 번 했을 가능성이 큽니다.

이번은 아닙니다. 이번 기회에 당신은 진짜 Swift에 대해 배울 것이고, 100일동안 당신이 자랑스러워 할 수 있는 몇 종류의 full app들을 만들어 볼 것입니다. 

당신은 이미 100days의 2가지 규칙을 읽었지만 이 코스의 기회를 최대한 활용하기 위해서 몇 가지 팁을 드릴게요 :

1. **마라톤이에요 단거리가 아닙니다.** <br>빨리 배워야한다는 생각으로 돌진하지 마세요. <sup id="a2">[2](#f2)</sup> 왜냐하면 이건 길을 잃게 될 큰 요인입니다.<br>자신만의 시간을 가지고 공부하세요
2. **"Shiny object syndrome"<sup id="a3">[3](#f3)</sup>의 희생양이 되지 마세요** <br>저도 압니다. 다른 코스에서 50$을 쓰는 유혹은 큽니다. 하지만 당신을 책을 사면 아무것도 배우지 못합니다.<br>당신의 성공적인 최고의 기회는 이곳에 나와있는 100days와 함께하며 실제로 이루는 것입니다. 
3. **고독한 늑대가 되지 마세요** <br>당신은 혼자서 배우는 게 아닙니다 - 많은 사람들처럼 돕기 위해 제가 여기 있습니다.<br>만약 질문이 있다면, [tweet me at @twostraws](https://twitter.com/twostraws)하세요. 최선을 다해서 도와드릴게요!
4. **Consolidation days<sup id="a4">[4](#f4)</sup>을 사용하세요** <br>100일동안 간격을 두고 당신에게 무엇을 배웠는지 정말로 몰입 할 수 있는 복습할 시간을 주세요.<br>당신이 확실히 알지 못하는 날로 돌아가거나, 놓친 숙제를 마치거나, 자유롭게 코딩할 때 이 시간들을 사용하세요.
5. 당신이 쉽게 참조할 수 있도록 북마크 해놓아야하는 [common Swift terms](https://www.hackingwithswift.com/glossary)용어 목록입니다.
6. [Download my Unwrap app from the App Store.](https://apps.apple.com/app/id1440611372)iPhone and iPad에서 동작하며, 이 코스의 처음 12일과 많은 보너스 활동이 포함되어 있습니다. 앱 내의 구매 없이 무료입니다.

# The Course

<h2 data-toc-skip>Days 1-12: Introduction to Swift</h2>

처음 12일동안 swift를 가볍게 배우는 내용을 제공합니다.<br>
당신은 매일 1분짜리 동영상을 선택해서 보고 각 동영상에 대한 짧은 퀴즈를 풀어볼 것입니다.<br>

제가 공부를 하나씩 할때마다 day가 추가 될 예정입니다.

- Day 1 - 변수, 간단한 데이터 타입, string interpolation(문자열 보간법)




---
---

# 각주 

><b id="f1"><sup>1</sup></b> Show me what you got처럼 너의 실력/진짜 모습을 보여줘라~의 의미[↩](#a1)<br>
<b id="f2"><sup>2</sup></b> Charge ahead : 돌진하다[↩](#a2)<br>
<b id="f3"><sup>3</sup></b> Shiny object syndrome : 지나치게 많은 아이디어나 최신 유행을 따르다가 그 어느 것도 제대로 완성하지 못하고 시간과 돈을 낭비하는 현상[↩](#a3)<br>
<b id="f4"><sup>4</sup></b> 사전적의미로는 통합 날짜이지만 문맥상 의미로는 정확히 100일이 아니라 사이사이에 복습할 시간을 넣어준 전체 days를 의미하는 것 같습니다.[↩](#a4)<br>


