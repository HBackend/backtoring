# 추상 클래스와 인터페이스

## 추상 클래스
- 하나 이상의 추상 메서드를 포함하는 클래스를 추상 클래스라고 한다.
- 이러한 추상 클래스는 OOP에서 중요한 요소인 다형성을 가지는 메서드의 집합을 정의할 수 있게 해주는 레전드이다.
  -  다형성이란, 객체지향 4원칙중 하나로 여러가지 상태를 가질 수 있는 능력이다.
  - 오버라이딩으로 예를 들면 부모클래스에서 상속받은 메서드를 자식클래스에서 오버라이딩 하면서 함수명은 같지만 자식이 재정의해서 다른 기능을 수행하게 재정의 할 수 있다. 
- 추상 클래스를 그 자체로 인스턴스화 할 수 없다.

### 추상 메서드
- 자식 클래스에서 반드시 오버라이딩 해야하는 메서드이다.
- 추상 메서드는 선언부만 존재하며 구현부는 없다.

```java
abstract void goodFunction();
```
> ex.
```java
abstract class Animal {
    public abstract void hi();
}

abstract class Cat extends Animal {
    @Override
    public void hi() {
        System.out.println('야옹');
    }
}
```

## 인터페이스
- 클래스를 작성할 때 기본이 되는 틀을 제공한다.

### 인터페이스 선언
- 인터페이스의 모든 필드와 메서드는 public static final(필드) 이다. (생략해도됨)
```java
public interface Animal {
    public int MAX_AGE = 100;
    
    public void hello();
    public void run();
}
```
> 컴파일 시 아래와 같이 자동변환
```java
// 필드는 public static final로 변환
public static final int MAX_AGE = 100;
// 메서드는 public abstract로 변환
public abstract void hello(); 
public abstract void run();
```

### 인터페이스 구현
- 인터페이스를 사용할때 인터페이스를 구현하는 클래스에서 `implements` 키워드를 사용한다.
- 인터페이스가 가지고 있는 메서드를 하나라도 구현하지 않으면 해당 클래스는 추상클래스가 됨(인스턴스화 X)

```java
public class Cat implements Animal {
    @Override
    public void hello() {
        System.out.println("애옹");
    }

    @Override
    public void run() {
        System.out.println("🐈");
    }
}
```

### Default Method

- default 키워드를 사용하여 인터페이스 내부에서도 로직이 포함된 메서드를 선언할 수 있다.
- 인터페이스의 구현체를 만들고 사용하는 중에 인터페이스에 추가해야할 메서드가 생겼을때 기존의 구현체들의 코드를 변경하지 않고 기능을 확장시킬 수 있다.
```java
public interface Animal {
    public int MAX_AGE = 100;
    public void hello();
    public void run();
    
    default void water() {
        System.out.println("");
    }
}
```

### Static Method

- 인터페이스에 정적 메서드를 선언할 수 있다.

```java
public interface Animal {
    public int MAX_AGE = 100;
    public void hello();
    public void run();
    
    static void food() {
        System.out.println("🍗");
    }
}

...

Animal.food();
```

> 호출시 `인터페이스명`.`메서드명` 형식으로 호출해야함