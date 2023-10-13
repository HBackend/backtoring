## Object Oriented Programming 객체지향

객체지향의 4원칙
`추상화`, `캡슐화`, `상속`,`다형성`

프로그래밍에서 객체지향의 패러다임이란?

```
필요한 데이터와 기능을 추상화시켜 필드와 메서드를 가진 객체를 만들고
그 객체들을 통해 로직을 구성하는 프로그래밍 방법
```

- 단순 순차적으로 실행되는 절차지향 프로그래밍과 대조되는 개념

- 클래스 단위의 객체는 각각 다른 상태값을 갖고, 그 값에 따라 다르게 행동한다

- 객체지향 설계에 디자인패턴을 적용하면 더욱 쉽고 효율적인 설계를 할 수 있다
  > `디자인 패턴`이란?  
  >  객체 지향 프로그래밍 설계를 최적화 할 수 있도록 사용되는 패턴

내가 생각하는 객체지향이란

개발을 하는데에 있어서 필요한 요소들을 객체 단위로 묶고, 그들의 구조의 **상호작용**을 통해 실행하는 프로그래밍 방법

#### 객체지향에서 `책임`,`역할`,`협력` 이란?

객체지향 설계의 품질을 결정하는 요소

**책임**

> 객체가 특정한 요청에 대하여 적절한 응답을 해야하는 책임을 갖는 것을 말한다  
> 객체가 다른 객체에 책임을 가지도록 요청하는것을 메세지 전송이라고 한다

**역할**

> 객체가 가지는 책임들의 집합을 말한다  
> 하나의 협력 안에 여러 객체가 참여할 수 있도록 역할을 추상화 할 수 있다

**협력**

> 객체들의 요청과 응답을 통해 형성되는 관계를 말한다

객체를 설계하는데에 있어서
객체간의 결합도가 높거나, 특정 상황에 국한되도록 설계하거나, 객체들끼리 서로 긴밀하게 연결되어있다면  
객체들이 협력하는데에 어려움이 발생하기때문에 시스템의 품질을 저하시키고 유지보수를 어렵게 한다

---

#### 추상화 Abstraction

메서드, 클래스 등의 내용을 구현하지 않고 선언만 하여 여러 클래스에서 공통된 속성과 기능을 한곳으로 묶어두는 것

```java
public abstract class AbstractionClass {
    public abstract int Abstraction();
}
```

#### 캡슐화 encapsulation

기능과 속성을 정의한 클래스에 접근제어자를 사용하여 외부에서의 불필요한 접근을 막는 것 (정보은닉)

> 한 클래스에 특정 기능을 구현하는 기능과 속성을 묶어두어 코드를 재사용 할 수 있게 한다

```java
public class EncapsulationClass {
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

#### 상속 inheritance

서브클래스가 슈퍼클래스를 물려받아 재정의하고, 확장하여 사용할 수 있게하는 것

> 확장과 재사용에 유용하다

```java
class Huiseong {
    public void PrintAge() {
        System.out.println("저는 1000살입니다");
    }
}
class Miri extends Huiseong {
    @Override
    public void PrintAge() {
        System.out.println("저는 7살 베이비 입니다");
    }
}

public class Test {
    public static void main(String[] args) {
        Miri m = new Miri();
        m.PrintAge();
    }
}
```

#### 다형성 polymorphism

다양한 객체들이 공통된 특성을 가지는 상위 클래스나 인터페이스를 통해 표현되는 것
한가지 타입의 참조변수로 여러 타입의 객체에 접근할 수 있게 하는것

> 오버라이딩, 오버로딩으로 다형성을 구현한다

```java
class Hope {
    void print() {
        System.out.println("저는 신입니다");
    }

}
class Huiseong extends Hope{
    @Override
    void print() {
        System.out.println("저는 신 희성입니다");
    }
}
class Miri extends Hope {
    @Override
    void print() {
        System.out.println("저는 진짜신희성 입니다");
    }
}

public class Test {
    public static void main(String[] args) {
        Hope h1 = new Miri();
        Hope h2 = new Huiseong();
        h1.print();
        h2.print();

    }
}
```
