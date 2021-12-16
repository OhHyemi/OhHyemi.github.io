---
title: "inheritance: 상속"
date: 2021-12-06T00:25:53+09:00
tags: ["inheritance","csharp", "상속"]
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

draft: false
---

## {{< color color="#FFD400" text="상속" >}}이 뭐야? 🧐

상속은 `확장`의 개념이다. 추상클래스, 일반클래스 모두 상속을 통해 특정 객체의 개념을 확장시킬 수 있다.(인터페이스의 경우 기능확장이라는 말이 좀 더 어울리는 것 같다.) 인터페이스와 추상클래스는 이전 포스트에서 다루었으니 일반클래스를 예시로 들겠다.


<br>

💚 예시
<br>

오크라는 객체가 있다고 하자. 이 오크라는 객체는 마법사 오크가 될수도, 전사 오크, 궁수 오크 등이 될 수 있다. 이런 오크들을 구현할 때 상속을 사용한다. 직업이 있는 오크 모두 하나의 오크라는 객체를 상속받을 수 있는 것이다. 일반클래스의 상속은 추상클래스나 인터페이스를 상속받는 것과 다르게 부모클래스도 인스턴스할 수 있다. 즉, 아무렂 직업이 없는 일반 오크(부모클래스)도 존재할 수 있고, 이 오크를 기반으로 다양한 직업을 가진 오크(자식클래스)도 존재할 수 있다. 

<br>

🍑 위의 내용을 바탕으로 코드를 만들어 보자!
<br>

🍑 일반클래스, 추상클래스, 인터페이스 모두 활용해보자!

```csharp
public abstract class Monster //몬스터라는 분류!
{
    private int maxHp;
    private int maxMp;
    private int hp;
    private int mp;
    private bool isAbleSkill;
    public bool IsAbleSkill
    {
        get => mp > 0;
        private set => isAbleSkill = value;
    }
    private bool IsAlive=> hp > 0;
    public int Hp
    {
        get => hp;
        set
        {
            var _hp = hp + value;
            if (_hp > maxHp)
            {
                hp = maxHp;
            }
            else if (_hp <= 0)
            {
                Die();
            }
            else
            {
                hp = _hp;
            }
        }
    }
    public int Mp
    {
        get => mp;
        set
        {
            var _mp = mp + value;
            if (_mp > maxMp)
            {
                mp = maxMp;
            }
            else if (_mp <= 0)
            {
                mp = 0;
            }
            else
            {
                mp = _mp;
            }
        }
    }
    protected Monster(int maxHp, int maxMp)//abstract 클래스의 생성자는 항상 protected로!
    {
        this.maxHp = maxHp;
        this.maxMp = maxMp;
        hp = maxHp;
        mp = maxMp;
    }
    public abstract void UseSkill();
    public abstract void Die();
    public void SetEnableUseSkill(bool able)
    {
        isAbleSkill = able;
    }
}
public class Orc : Monster
{
    public override void UseSkill()
    {
        if (IsAbleSkill)
        {
            Skill();
        }
    }
    public Orc(int maxHp, int maxMp) : base(maxHp,maxMp)
    {
    }
    protected virtual void Skill()
    {
        Console.WriteLine("일반오크 스킬 발동!");
    }
    public override void Die()
    {
        Console.WriteLine("오크 죽음!");
    }
}
public class WizardOrc : Orc, IFly
{
    public WizardOrc(int maxHp, int maxMp) : base(maxHp,maxMp)
    {
    }
    protected override void Skill() //부모의 함수를 오버라이딩 하여 자신에게 알맞은 함수를 실행함
    {
        Console.WriteLine("마법사 오크 스킬 발동!");
    }
    public void Fly()
    {
        Console.WriteLine("휘익~ 마법사 오크 난다!");
    }
}
public class KnightOrc : Orc
{
    public KnightOrc(int maxHp, int maxMp) : base(maxHp,maxMp)
    {
    }
    protected override void Skill()
    {
        Console.WriteLine("전사오크 스킬 발동!");
    }
}
public class ArcherOrc : Orc
{
    public ArcherOrc(int maxHp, int maxMp) : base(maxHp,maxMp)
    {
    }
    protected override void Skill()
    {
        Console.WriteLine("궁수오크 스킬 발동!");
    }
}
```

<br>

## {{< color color="#FFD400" text="상속" >}}의 특징은? 🧐
- 자식클래스가 부모클래스의 필드와 메소드를 모두 가지고 있다.
- 부모클래스에서 private으로 선언되어있는 요소들은 자식클래스라도 접근이 불가능하다.(가지고는 있음!)
- 부모클래스에서 `protected`로 선언되어있는 요소는 `자식클래스만 접근`이 가능하다.
- 부모클래스이 메소드를 `virtual/override` 를 통해 자식클래스에서 `재정의` 할 수 있다.
- interface를 제외한 모든 상속은 `다중상속이 불가능`하다.