---
title: "피츠의 법칙"
date: 2021-12-19T17:46:38+09:00
tags: ["ux","Fitts'Law"]
categories: ["uxui"]
series: [""]
chapter: [""]
author: [""]
ShowReadingTime: true
ShowBreadCrumbs: false
ShowPostNavLinks: true
ShowCodeCopyButtons: true
ShowCreativeCommons: true
showToc: true
TocOpen: false
comments: true
disableShare: false
searchHidden: false
cover:
  hidden: true
  image: ""
  alt: ""

draft: false
---

## 🔎피츠의 법칙
 
<br>

> 대상에 도달하는 시간은 대상까지의 거리와 대상의 크기와 함수 관계에 있다.

- 터치 대상의 크기는 사용자가 정확하게 선택할 수 있을 정도로 충분히 커야한다.
- 터치 대상 사이에 충분한 거리를 확보해야 한다.
- 터치 대상은 인터페이스상에서 쉽게 도달할 수 있는 영역에 배치해야 한다.

### 💛 피츠의 법칙 적용 사례

#### 💚 폼 텍스트 레이블 (form text label)
> 폼 텍스트 레이블은 피츠의 법칙을 보여주는 흔한 예다. 디자이너와 개발자가 텍스트 레이블 요소와 입력을 연결해두면 레이블을 탭하거나 클릭해도 입력이 선택된다.

- 입력 면적이 넓어져서 정확하게 터치하지 않아도 입력이 가능하게 만들어준다.
- 모바일의 경우는 터치 면적이 좁아서 폼 텍스트 레이블을 활용한다면 더욱 더 좋은 것 같다.

##### 💙 내가 실무에서 적용했던 것!
나는 한 프로젝트에서 아웃게임을 담당해서 구현한 적이 있다. 이때에 UI prefab 제작과 배치까지 해야했다. 그 당시 폼 텍스트 레이블이라는 것은 몰랐지만 버튼을 제작할 때 버튼의 뒷배경, 아이콘, 텍스트를 모두 포함하도록 raycast영역을 정해주었다.(크기를 확장)

#### 💚 그 외...
- 각 정보들을 입력해야하는 상황일 때(ed. 인터넷에서 물건을 구매시 개인 정보를 입력할 경우) 마지막 입력 폼 바로 하단에 제출하기 버튼을 두는 것.(대상에 도달하는 시간을 줄여줌)
- 한글, word같은 프로그램을 사용할 때 텍스트에 관한 것들 또는 자주 사용되는 것들을 모아두는 것. (대상에 도달하는 시간을 줄여줌)
![예시이미지](/images/studying22.png)
- 모바일 화면에 항상 앱들이 한 줄에 5개 미만으로 되어있는 것(보통 핸드폰 및 세로 기준). (대상을 잘못 터치하지않게 간격 조절을 한 것)

<br>

## ✏️ 마무리 하며
피츠의 법칙은 당연하다고 느껴진다. 하지만 당연하다고 느껴지는 것들을 우리는 가끔 소홀히 할 때가 많은 것 같다. 다들 내가 누르려고 했던 것이 아닌데 대상과의 거리가 너무 좁아서 잘못 누른 경험이 분명 있을 것이다. 당연한 것이지만 그것을 지키지 못한 부분이 있었던 것..! 우리는 당연한 것일지라도 잊지말고 명심하도록 하자!!!