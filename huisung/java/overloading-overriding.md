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
-  부모가 가지고 있는 메소드와 똑같은 모양의 메소드를 자식이 가지고 있는 것(부모의 메서드 재정의)이다.

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