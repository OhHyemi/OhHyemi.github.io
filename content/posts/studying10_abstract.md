---
title: "abstract class: 추상클래스"
date: 2021-12-02T23:13:57+09:00
tags: ["csharp","abstract","class"]
categories: ["csharp"]
---
오늘은 추상 클래스에 대해 알아보쟈!

## {{< color color="#FFD400" text="abstract class(추상클래스)" >}}가 뭐야? 🧐

인터페이스가 `Can Do`를 알려주는 역할이라면 추상클래스는 `분류(category)`를 알려주는 클래스다.  

<br>

💚 예시 (내가 이해한 방식) 
<br>

인터페이스에서 이야기했던 예시를 이어가자면, 앵무새와 참새, 펭귄 그리고 슈가 글라이더는 각자 객체를 가질 수 있다. 하지만 앵무새,참새 그리고 펭귄을 포함하는 `조류`, 슈가 글라이더를 포함하는 `포유류`라는 것은 객체가 없는, 추상적인 `분류(category)`의 개념이다. 
<br>
추상클래스 안에 추상메소드는 인터페이스와 같은 역할이라고 생각하면된다. 
<br>
즉, "이러한 분류(추상클래스)에 속하는 객체들은 이러한(추상메소드)것에 반드시 반응해야한다." 라는 계약이 생긴다.
<br>

🍑 위의 내용을 추가로 코드를 수정해보자
```csharp
public abstract class Animal//동물이라는 카테고리를 표현
{
    private bool isAlive = true;//추상클래스는 필드를 가질 수 있다.

    public abstract void Eat();//추상메소드: 자식클래스에서 모두 구현을 해주어야함!

    public virtual void Die()//일반 메소드: 추상클래스는 일반 메소드 또한 가질 수 있다.
    {
        isAlive = false;
    }
}

public abstract class Birds : Animal//동물이라는 카테고리 속 조류라는 카테고리
{
    protected Birds(Beak beak)
    {
        this.beak = beak;
    }
    public Beak beak { get; private set; }
}

public class Sparrow : Birds, IFly//조류에 속하는 참새 객체 
{
    public Sparrow(Beak beak) : base(beak)
    {
    }
    public void Fly()
    {
        Console.WriteLine("포로록~ 참새 난다~");
    }
    public override void Eat()
    {
        Console.WriteLine("참새 쌀알 먹는다. 콕콕!");
    }
}

public class Parrot : Birds, IFly//조류에 속하는 앵무새 객체
{
    public Parrot(Beak beak) : base(beak)
    {
    }
    public void Fly()
    {
       Console.WriteLine("푸드덕~ 앵무새 난다~");
    }
    public override void Eat()
    {
        Console.WriteLine("츄릅~ 앵무새 메뚜기 먹는다!");
    }
}
```

## {{< color color="#FFD400" text="abstract class(추상클래스)" >}}의 특징은?  🧐

- 클래스 안에 추상메소드가 하나라도 존재한다면, 그 클래스는 반드시 추상클래스여야한다.
- 추상클래스: `abstract class ["클래스 이름"]`, 추상메소드: `abstract ["반환타입"] ["메소드 이름"]( ["파라미터"] )`로 표현한다.
- 추상메소드는 내부가 구현되지않은 상태여야한다. (이전에 포스팅했던 인터페이스가 추상메소드만으로만 이루어진 것)
- 접근한정자를 정해주지않으면 `private` 디폴트 값이다.
- `필드와 일반메소드 모두 가지고 있을 수 있다.`(인터페이스와 가장 큰 차이점 중 하나)
- 다른 일반 클래스와 마찮가지로 `다중상속이 불가능`하다.
- 인터페이스와 마찮가지로 인스턴스가 불가능하다. 

<br>

** 다음 포스팅은 일반 클래스와 상속에 대해서 다루겠다!