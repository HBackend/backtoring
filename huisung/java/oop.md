# 객체 지향

### 객체지향 프로그래밍
> Object Oriented Programming (객체지향 프로그래밍)
- 절자적이 아닌 객체가 중심이 되어 이들의 상호작용으로 프로그램이 진행되는 방식이다.
- 객체는 하나의 역할을 수행하는 필드와 메서드의 집합이다.
> ex. 사물 / 추상적인 개념

### 내가 생각하는 객체지향이란?
- 프로그램을 객체라는 단위로 나누고 이러한 객체들 간의 상호작용을 중심으로 소프트웨어를 개발하고 설계하는 방법이다!

## 객체지향 4원칙
- 객체지향 4원칙에는 **추상화** / **캡슐화** / **상속** / **다형성** 이 있다.

### 추상화
- > 추상 : 사물이나 표상을 어떤 성질이나 공통점과 본질에 착안하여 그 것을 추출하여 파악하는 것   
  >  -> 불필요한 것을 제거하고 가장 본질적이고 공통적인 부분만 추출하여 표현하는 것 -> 중요한 부분이 강조됨
- 객체의 공통적인 속성과 기능을 분리해서 재조합 하는 것.

```java
class Computer {
    public void display() { ... };
    public void typing() { ... };
}

// display() / typing() / commandKeyClick()
class Mac extends Computer {
    public void commandKeyClick() { ... };
}

// display() / typing() / windowKeyClick()
class Lg extends Computer {
    public void windowKeyClick() { ... };
}
```

### 캡슐화
- 각 객체의 데이터를 필요한 부분만 공개하고 나머지 부분은 외부에 노출하지 않게 하는 방식이다.
- 객체의 무결성을 위해 객체의 필드를 private로 설정하고 해당 값을 메서드를 통해 접근할 수 있게 하여 값의 오염을 막을 수 있고 값 변경의 목적을 명확히 할 수 있다.

```java
class HBackEnd {
    private String name;
    private Integer assignedCount;

    public String getName() {
        return name;
    }

    public Integer getAssignedCount() {
        return assignedCount;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    public void setAssignedCount(Integer count) {
        this.assignedCount = count;
    }
}
```

### 상속
- 클래스가 다른 클래스의 필드와 메서드를 물려받는 기능이다.
- `extends` 키워드로 상속이 가능하며, 필드를 물려준 클래스를 부모 클래스, 물려받은 클래스는 자식 클래스라고 부른다.
- 상속을 통해 코드의 재사용성을 높힐 수 있고 유지보수가 편해진다.

```java
class Person {
    String name;
    Integer age;
    
    ... (메서드 들)
}

// 각각 자식 클래스를 Person의 필드와 메서드들를 물려받음.
class Student extends Person {
    Integer schoolNumber;
    Integer examScore;
}

class Developer extends Person {
    String baekjoonRank;
    Integer balance;
}
```

### 다형성
- 하나의 객체가 여러 가지 다른 형태를 가질 수 있는 것을 말한다.
- 인터페이스, 추상클래스, 상속 등으로 다형성을 구현할 수 있다. (오버로딩, 오버라이딩)
- 부모나 자식 클래스의 타입 참조 변수로 클래스를 생성하여도 자식 클래스에서 오버라이딩한 메서드가 호출된다.
  - 형변환 신경 안써도 됨

```java
class Person {
    public void walking() {
        System.out.println("뚜벅뚜벅");
    }
}

class Developer extends Person {
    @Override
    public void walking() {
        System.out.println("저벅저벅");
    }
}
```