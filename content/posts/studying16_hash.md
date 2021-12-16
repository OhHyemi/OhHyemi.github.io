---
title: "HashTable: 해시테이블"
date: 2021-12-15T21:14:39+09:00
tags: ["csharp", "dictionary", "hash", "hashtable"]
categories: ["csharp"]
author: [""]
ShowReadingTime: true
ShowBreadCrumbs: false
ShowPostNavLinks: true
ShowCodeCopyButtons: true
ShowCreativeCommons: true
showToc: true
TocOpen: true
comments: true
disableShare: false
searchHidden: false
cover:
  hidden: true
  image: "/logo/logo-csharp.png"
  alt: "csharp"

draft: false
---

## {{< color color="#FFD400" text="해시" >}}가 뭐야? 🧐

> `해시(Hash)는` 키 값을 `해시 함수(Hash function)`으로 해싱하여 해시테이블의 특정 위치로 직접 엑세스하도록 만든 방식이다.

## {{< color color="#FFD400" text="해시테이블" >}}이 뭐야? 🧐

![해시테이블](/images/studying16_0.PNG)

> 해시 테이블은 연관배열 구조를 이용하여 키(key)에 결과 값(value)을 저장하는 자료구조이다.
>> 연관배열 구조(associative array)란, 키(key) 1개와 값(value) 1개가 1:1로 연관되어 있는 자료구조이다. 따라서 키(key)를 이용하여 값(value)을 도출할 수 있다.

<br>

**key 와 value는 일대일 매핑으로 같은 value값을 가질 순 있어도, 같은 key값은 가지지 못한다.** 

###  1. 해시테이블(HashTable) 클래스

- `Non-generic` 클래스.
- `key`와 `value`를 가지고 있음 -> 둘다 `object` 타입으로 받음 -> boxing/unboxing이 일어난다.
- `Double Hashing` 방식을 사용


#### 💚 `Double Hashing` 이란? 


 해시충돌이 일어날 경우 한 번 더 다른 해시함수를 거쳐 새로운 해시코드를 생성하여 해시충돌을 막는 방법.


#### 💚 `해시충돌` 이란? 

서로 다른 키값을 가졌지만 해싱 후 가진 해시코드가 같은 경우.

<br>

ex) 만약 해시함수의 알고리즘이 문자열의 길이를 반환한다고 가정하였을 경우, cake와 taco는 4라는 해시코드를 가지게 된다. key는 서로 다르지만 해시코드가 이처럼 같은 경우를 해시충돌이라고 한다.

###  2. 딕셔너리(Dictionary) 클래스

- `Generic` 클래스.
- `key`와 `value`를 가지고 있음 -> Generic으로 타입을 지정  -> `boxing/unboxing 일어나지 않음!`
- `Chaining` 방식을 사용

#### 💚 `Chaining` 이란? 

 linked list로 해당값을 기존값에 연결시키는 방법이다.

 ![체이닝](/images/studying16_1.PNG)

 