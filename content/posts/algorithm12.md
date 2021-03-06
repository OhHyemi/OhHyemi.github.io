---
title: "AlgorithmStudy_백준 4673"
date: 2021-11-22T21:13:41+09:00
tags: ["csharp", "알고리즘", " 백준"]
categories: ["algorithm"]
---

# 알고리즘 공부 {{< color color="#FFD400" text="백준 4673" >}} 🧐
#### 셀프 넘버

## 👉문제
셀프 넘버는 1949년 인도 수학자 D.R. Kaprekar가 이름 붙였다. 양의 정수 n에 대해서 d(n)을 n과 n의 각 자리수를 더하는 함수라고 정의하자. 예를 들어, d(75) = 75+7+5 = 87이다.

양의 정수 n이 주어졌을 때, 이 수를 시작해서 n, d(n), d(d(n)), d(d(d(n))), ...과 같은 무한 수열을 만들 수 있다. 

예를 들어, 33으로 시작한다면 다음 수는 33 + 3 + 3 = 39이고, 그 다음 수는 39 + 3 + 9 = 51, 다음 수는 51 + 5 + 1 = 57이다. 이런식으로 다음과 같은 수열을 만들 수 있다.

33, 39, 51, 57, 69, 84, 96, 111, 114, 120, 123, 129, 141, ...

n을 d(n)의 생성자라고 한다. 위의 수열에서 33은 39의 생성자이고, 39는 51의 생성자, 51은 57의 생성자이다. 생성자가 한 개보다 많은 경우도 있다. 예를 들어, 101은 생성자가 2개(91과 100) 있다. 

생성자가 없는 숫자를 셀프 넘버라고 한다. 100보다 작은 셀프 넘버는 총 13개가 있다. 1, 3, 5, 7, 9, 20, 31, 42, 53, 64, 75, 86, 97

10,000보다 작거나 같은 셀프 넘버를 한 줄에 하나씩 출력하는 프로그램을 작성하시오.

<br>

## 👉입력  
입력은 없다.


<br>

## 👉출력
10,000보다 작거나 같은 셀프 넘버를 한 줄에 하나씩 증가하는 순서로 출력한다.

<br>

🍑풀이
```csharp
using System;
using System.Linq;

namespace Algorithm12
{
    class Baekjoon4673
    {
        static void Main(string[] args)
        {
            var arr = new bool[10000]; //생성자가 있는 지 없는 지 체크해주는 배열!

            for (int i = 0; i < arr.Length; i++)
            {
                var n = i + 1; //실제 체크해야 하는 수는 인덱스 보다 1 더 큼.
                
                if (arr[i] == false) //만약 생성자가 없다면
                {
                    Console.WriteLine(n);//출력
                }

                var list = n.ToString().ToArray();//수를 array 로 변환
                foreach (var num in list)
                {
                    n += num - '0';//수에 각 자리 수를 더함
                }
                
                if (n - 1 < arr.Length)//만약 인덱스가 arr의 길이보다 작을 경우에는
                {
                    arr[n - 1] = true;//생성자가 있다고 true 로 변경하기
                }
            }
        }
    }
}
```

<br>

[문제풀러가기](https://www.acmicpc.net/problem/4673)