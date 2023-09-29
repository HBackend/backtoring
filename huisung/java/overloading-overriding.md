# 오버로딩, 오버라이딩

## 오버로딩
- 매개변수의 유형과 개수를 다르게 하여 같은 이름의 메서드를 여러개 가지게 하는 것

```java
class Cal {
    public int plus(int i, int j) {
        return i + j;
    }
    
    public int plus(int i, int j, int k) {
        return i + j + k;
    }
    
    public int plus(int i, int j, int k, int l) {
        return i + j + k + l;
    }
}
```
```java
Cal c = new Cal();

c.plus(1,2); // 3
c.plus(1,2,3); // 6
c.plus(1,2,3,4); // 10
```
- 메소드의 인자에 어떤 값이 쓰이느냐에 따라서 각기 다른 메소드가 호출됨

## 오버라이딩
-  부모가 가지고 있는 메서드와 똑같은 모양의 메서드를 자식이 가지고 있는 것(부모의 메서드 재정의)이다.
- 즉 부모의 메서드를 상속받아 재정의(다형성)한다.
  - 상속 -> 부모 클래스의 필드와 메서드를 자식 클래스에서 사용할 수 있는 것
  - 다형성 -> 같은 이름의 부모의 메서드를 자식 클래스에서 재정의하여 기능을 확장하거나 수정하는 것

```java
class Animal {
    public void hello() {
        System.out.println("동물이에오");
    }
}

class Cat extends Animal {
    @Override
    public void hello() {
        System.out.println("고양이에오");
    }
}

...

Cat c = new Cat();
c.hello(); // "고양이에오"
```
- 오버라이딩하면 자식클래스에서 재정의된 메서드가 호출된다.

> super 키워드를 통해 부모의 메서드를 호출할 수 있다.
```java
class Cat extends Animal {
    super.hello();
}
```

## 결합도(Coupling)와 응집도(Cohesion)

### 결합도
- 결합도는 다른 모듈간의 의존도를 말한다.
> ex. 연관된 두 개의 클래스가 있다고 예를 들었을 때 한 클래스가 변경 되었다면 다른 클래스도 변경 되어야 한다.   
> 이렇게 된다면 규모가 큰 프로젝트에서는 규모가 커질수록 그만큼 변경해야할 부분이 많아진다.

### 응집도
- 모듈 내부의 기능적인 집중도를 말한다.

개별 모듈은 독립적으로 자신에게 주어진 기능만 수행해야하고 (높은 응집도)   
다른 모듈에 의존성이 높아선 안된다. (낮은 결합도)
- 결합도는 낮추고, 응집도는 높여야 유지보수하기 쉽고 좋은 코드가 된다.


### 상속을 통해 결합도를 낮추기 위함 설계
- 결합도를 낮추기 위한 방법중 하나는 다형성이다.
  - 상속이나 메서드 재정의를 통해 이루어진다.

> ex. 추상 클래스를 사용한 예시
```java
abstract class Fish {
    abstract void breath();
    abstract void swim();
}

class cod implements Fish {
    @Override
    void swim() {
    }
    
    @Override
    void breath() {
    }
}

class Carp implements Fish {
    @Override
    void swim() {
    }

    @Override
    void breath() {
    }
}
```