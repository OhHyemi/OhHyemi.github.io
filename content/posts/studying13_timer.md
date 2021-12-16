---
title: "타이머를 이용해 스킬아이콘을 만들어보자!"
date: 2021-12-06T15:58:16+09:00
tags: ["unity","coroutine","timer", "spellIcon"]
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

🍑 타이머
```csharp
public class Timer : MonoBehaviour
{
    private Coroutine curTimer;
    
    public void StartTimer(int time, Action<float> onValueChanged)
    {
        //진행되던 타이머가 있다면 멈추고 새로 시작
        if (curTimer != null)
        {
            StopCoroutine(curTimer);
        }
        curTimer = StartCoroutine(CoStartTimer(time, onValueChanged));
    }
    //타이머를 진행할 시간, 시간이 바뀔때마다 어떠한 행동을할건지
    IEnumerator CoStartTimer(int time, Action<float> onValueChanged)
    {
        float timer = 0;
        while (true)
        {
            //타이머가 지정된 시간을 넘기면 break!
            if (timer >= time)
            {
                break;
            }
            //시간을 더해주자!
            timer += Time.deltaTime;
            yield return null;
            //남은 시간을 보내주기
            onValueChanged(time - timer);
        }
        //타이머가 끝나면 코루틴을 null
        curTimer = null;
    }
}
```

💚 `deltaTime` 사용 이유!

>지난 프레임이 완료되는 데 까지 걸린 시간을 나타내며, 단위는 초를 사용합니다.(읽기전용)
사용자의 프레임 률(frame rate)을 독립적으로 적용하기 위해서 사용합니다.

즉! 사용자의 각자 프레임률이 다르기 때문에 프레임 카운트로 타이머를 만든다면 각 사용자의 타이머는 시간이 모두 다르다.
하지만 deltaTime을 쓴다면, 같은 결과값을 얻을 수 있다!

<br>

여기서, 매 프레임마다 실행되는 update와 달리 coroutine을 사용했는데 내용이 적용이 될까? 라는 의문이 들 수 있다. 
yield return null 을 사용함으로 update바로 다음에 실행이 되도록 하였다! 즉, update에서 사용하는 것과 동일하게 사용이 가능하다.

![실행순서](/images/studying13_0.PNG)


🍑 스킬아이콘
```csharp
public class SpellIcon : MonoBehaviour
{
    //연출에 사용할 커브!
    [SerializeField] private AnimationCurve ease;
    //스킬 아이콘 이미지
    private Image img_icon;
    //쿨타임이 돌 때 이미지(딤드)
    private Image img_cooltime;
    //쿨타임을 표시해 줄 텍스트
    private Text txt_timer;
    //타이머를 가지고 있자!
    private Timer timer;
    //임시 쿨타임 적용
    private int cooltime = 5;

    private void Awake()
    {
        foreach (var img in GetComponentsInChildren<Image>())
        {
            if (img.name == "Image_Spell")
            {
                img_icon = img;
            }
            else if (img.name == "Image_CoolTime")
            {
                img_cooltime = img;
            }
        }
        
        var btn = img_icon.gameObject.AddComponent<Button>();
        btn.onClick.AddListener(OnClickSpell);

        timer = GetComponent<Timer>();
        txt_timer = GetComponentInChildren<Text>();
    }
    
    //바깥에서 불러줘야해!
    //useAble : 바로 사용이 가능한지?
    public void Initialize(Sprite sprite, int cooltime, bool useAble = true)
    {
        img_icon.sprite = sprite;
        this.cooltime = cooltime;
        //바로사용이 불가능하다면 쿨타임을 실행!
        OnTimeChanged(useAble ? cooltime : 0);
    }
    
    void UseSpell()
    {
        img_cooltime.raycastTarget = true;
        timer.StartTimer(cooltime, OnTimeChanged);
    }
    void OnClickSpell()
    {
        //어디론가 보내서 스킬을 발동되도록 해야겠지 ?
        Debug.Log("아 스킬 발동ㅋ");
        ClickAnimation();//연출!
        UseSpell();
    }

    void ClickAnimation()
    {
        //클릭시 커졌다가 다시 돌아오는 핑퐁형태의 연출을 추가!
        transform.Scale(Vector3.one, Vector3.one * 1.1f, 0.1f).SetEase(ease,true).Play();
    }
    //타임이 변경될 때 마다 업데이트를 시켜줌
    void OnTimeChanged(float time)
    {
        UpdateCooltimeImage(time);
        UpdateTimerText(time);
    }
    void UpdateCooltimeImage(float time)
    {
        if (time <= 0)
        {
            //쿨타임이 끝났으니 아이콘을 누를 수 있도록 해당 이미지를 raycastTarget을 꺼줌.
            img_cooltime.raycastTarget = false;
        }
        if (cooltime > 0)
        {
            img_cooltime.fillAmount = time / cooltime;
        }
        else
        {
            img_cooltime.fillAmount = 0;
        }
    }
    void UpdateTimerText(float time)
    {
        txt_timer.text = time <= 0 ? string.Empty :  txt_timer.text = Math.Ceiling(time).ToString();
    }
}
```

![결과](/images/studying13_1.PNG)

스킬 아이콘을 초기화해주고 정보를 넣어주는 것은 원래 해당 클래스 바깥에서 관리를 해주어야 할 것이다.
이 스킬 아이콘들의 상태를 관리하고 이벤트들을 실제로 사용하는 곳으로 전달하는 역할의 매니저 클래스가 필요하다. 다음에 이 클래스를 관리하는 클래스도 추가해보겠다.
<br>

이 클래스는 실 데이터(스킬의 데미지, 타겟, 효과 등...)를 다루거나 그 데이터를 기반으로 행위를 하는 것보다 사용자의 눈에 보여지는 부분만 처리하기 위해 존재한다.(`UI적 부분만`)