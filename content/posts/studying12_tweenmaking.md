---
title: "Tween 만들기 프로젝트 근황"
date: 2021-12-06T15:34:11+09:00
tags: ["Tween", "Project", "AnimationCurve", "unity"]
categories: ["unity"]
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
  image: "/logo/logo-unity-01.png"
  alt: "unity"

draft: false
---
애니메이션 커브에 대해서 조금 더 알 수 있었던 핑퐁 기능 만들기였다.


🍑 핑퐁 기능 추가!!!!
```csharp
public static Tween SetEase(this Tween tween, AnimationCurve ease, bool pingpong = false)
//ping pong: 다시 돌아오는 형태의 애니메이션
{
    if (!tween.IsPlaying) //트윈이 플레이 중이지 않을 때 수정!
    {
        if (pingpong)//핑퐁을 한다면
        {
            Keyframe[] keyframes = new Keyframe[ease.length];
            //애니메이션 커브의 키 프레임만큼 키프레임 배열 생성
            for (int i = 0; i < ease.length; i++)
            {
                //일대일 매칭을 해서
                keyframes[i] = ease.keys[i];
                //정해진 기간내에 from으로 와야함. 
                //반절은 to로 반절은 from로 가야하기때문에 2로 나누어 줌!
                keyframes[i].time = keyframes[i].time / 2;
            }
            //새로운 커브를 생성해 이전 ease와 교체
            ease = new AnimationCurve(keyframes);
            //핑퐁으로 모드를 변경!
            ease.postWrapMode = WrapMode.PingPong;
        }
        tween.Ease = ease;
    }
    else
    {
        Debug.Log("tween is playing");
    }
    return tween;
}
```

💚 `ease.Evaluate(time / duration)` 를 통해서 총 애니메이션 기간에 대한 현재 애니메이션 타임의 값을 ease에서 얻을 수 있다. 이 값을 대상이 Transform(position, scale, rotate)이든지 MaskAbleGraphic(color, alpha), CanvasGroup(alpha)이든지 간에 값을 정해줄 수 있다.

<br>

나중에 애니메이션커브만 따로 포스팅을 해보겠다!