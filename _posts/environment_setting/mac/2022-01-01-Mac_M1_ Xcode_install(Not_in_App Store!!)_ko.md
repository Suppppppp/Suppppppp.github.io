---
title: Mac M1 Xcode 설치(App Store 말고!!)
author: Kyungsup Go (Sup)
date: 2021-01-01 00:00:00 +0900
categories: [Environment setting, Mac M1]

tags: [Mac,MacOS,M1,M1 pro,Apple silicon,Xcode]
toc: True
comments: true
---


window에서 넘어온 mac으로 넘어온 가장 큰 이유는 ios개발을 위해서는 mac을 사용해야하는 것이었기 때문에 ios개발에 필요한 Apple macOS 전용 IDE인 Xcode를 설치해보도록 하겠습니다.
<br>사실 App store에 검색만하면 Xcode가 있는데 왜 굳이 이런글을 쓸까 싶을 수도 있는데 xcode 설치로 구글링을 조금만 해보면 알 수 있습니다. 아래는 Xcode 설치를 검색해본 것인데 App store를 통해 설치를 하는 것이 얼마나많은 장애(?)가 있는지 선배개발자님들의 고생이 보입니다. 


![Untitled](/assets/img/environment_setting/mac/Mac_M1_Xcode_install/Untitled_0.png){: width="500" height="300"}<br>


그래서 여러 글을 탐독한 결과 App store가 아닌 Apple developer사이트에서 직접다운받는 것이 제일 좋다고 하여 그 방법으로 진행해보겠습니다.<br>[여기](https://developer.apple.com/develop/)  로 들어가서 Develop -> Downloads를 클릭해줍니다.(저는 이미 들어가서 화면이 살짝 다를 수 있으나 홈페이지 상단에 Develop을 누르면 같은 화면으로 나타납니다)


![Untitled](/assets/img/environment_setting/mac/Mac_M1_Xcode_install/Untitled_1.png){: width="400" height="200"}




그럼 아래와 같이 현재 날짜 기준 2021/12/12 최신버전 Xcode 13.2 RC 다운로드가 나오게 됩니다.

![Untitled](/assets/img/environment_setting/mac/Mac_M1_Xcode_install/Untitled_2.png)

해당버전으로 다운받아 진행해도 무리는 없습니다  (Xcode 13버전의 경우 Big Sur 11.3 이상의 버전에만 동작합니다. 버전이 11.이하의 os 일 경우 업데이트하고 진행하주시는 게 좋습니다.) 

<details>
<summary> Tip 13.2RC 의 의미가 궁금하신 분들만 보세요</summary>
<div markdown="1">

The term "Release Candidate" (RC) replaces "GM seed" and indicates this version is near final. 라는 의미를 간단히 설명하자면 RC(Release Candidate) 직역하면 출시후보(최종 릴리즈)버전입니다. 정식 출시전 마지막 베타버전을 보통 RC라고 칭합니다. 이 단계에서 버그가 발견되지 않을 경우 바로 출시를 준비합니다.
GM은 Golden Master의 약자로 최종판 이라고 이해하면 됩니다.  
아래는 소프트웨어의 배포주기 입니다. 따라서 위의 13.2RC버전은 딱히 버그가 발견되지않으면 그대로 GM으로 대체 되고 추후 정식배포판이 될 확률 이 높습니다.

![Untitled](/assets/img/environment_setting/mac/Mac_M1_Xcode_install/Untitled_3.png){: width="500" height="300"}*출처 : [소프트웨어 배포 생명주기](https://ko.wikipedia.org/wiki/%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4_%EB%B0%B0%ED%8F%AC_%EC%83%9D%EB%AA%85_%EC%A3%BC%EA%B8%B0)&nbsp;/[GM의 의미](https://koorei.tistory.com/71)*
</div>
</details>


만약 Beta버전들에 지독한 경험이 있어서 stable 버전을 원한다면 위의 창에서 More버튼을 눌러줍니다.


![Untitled](/assets/img/environment_setting/mac/Mac_M1_Xcode_install/Untitled_4.png)


그럼 Apple에서 다운받을 수 있는 여러가지가 나오는데 여기에 Xcode를 입력해 검색해주고 마음에 드는 Stable버전을 다운받아 줍니다.


![Untitled](/assets/img/environment_setting/mac/Mac_M1_Xcode_install/Untitled_5.png)

저는 13.2RC 버전으로 다운로드를 진행했습니다.
용량이 10GB이기 때문에 15~20분 정도 소요되었습니다.
xip은 Extract in Place의 약자라고 합니다 zip형식의 파일과 비슷하다고 하니 토막상식으로 알려드립니다.
파일을 눌러 압축을 풀어줍니다.

![Untitled](/assets/img/environment_setting/mac/Mac_M1_Xcode_install/Untitled_6.png)
![Untitled](/assets/img/environment_setting/mac/Mac_M1_Xcode_install/Untitled_13.png)<br>


정상적으로 압축이 풀렸으면 xcode를 실행해줍니다

![Untitled](/assets/img/environment_setting/mac/Mac_M1_Xcode_install/Untitled_7.png)

![Untitled](/assets/img/environment_setting/mac/Mac_M1_Xcode_install/Untitled_8.png)
![Untitled](/assets/img/environment_setting/mac/Mac_M1_Xcode_install/Untitled_9.png)
![Untitled](/assets/img/environment_setting/mac/Mac_M1_Xcode_install/Untitled_10.png)
![Untitled](/assets/img/environment_setting/mac/Mac_M1_Xcode_install/Untitled_11.png)

Xcode가 정상적으로 설치되었습니다.

![Untitled](/assets/img/environment_setting/mac/Mac_M1_Xcode_install/Untitled_12.png)
