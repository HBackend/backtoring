### Getter, Setter

Getter, Setter 란?

```
접근제어자 private 으로 설정된 필드에 대해,
직접적으로 접근하는것을 막고 메서드를 통해 접근할 수 있도록 하는 것
```

Getter (접근자)

- 필드의 값을 반환해준다
- 매개변수가 없다

```java
public String getName() {
        return name;
    }
```

Setter (수정자)

- 필드의 값을 수정해준다
- 리턴타입이 없다

```java
public void Name(String name) {
        this.name = name;
    }
```

---

### Constructor

Constructor (생성자) 란?

```
인스턴스가 생성될 때 반드시 호출이 되고, 가장 먼저 실행되어 인스턴스의 초기화를 담당하는 메서드
```

- 생성자 이름은 클래스 이름과 같다
- 초기화 시 매개변수로 받는 값에 따라 여러 생성자가 생길 수 있다

```java
public Book(String title, String author) {
        this.title = title;
        this.author = author;
    }
// 기본생성자
public Book() {

}
```

---

## Builder

### 빌더 패턴이란

```
생성자 또는 수정자를 사용하여 객체의 속성에 값을 넣어주는 과정에서 일어나는 문제를 해결해주기 위해 사용하는 패턴
```

사용 예시

```java
public static void main(String[] args) {
    Person parkmiri = new Person.Builder()
        .name("박미리")
        .age(101)
        .birthday(070722)
        .build();
}
```

> 빌더의 구현은 롬복의 `@Builder` 어노테이션을 달아 사용할 수 있다 ~~진짜롬복없었으면어떡하지~~

#### 생성자(Constructor) 의 문제

- 객체의 필드가 많아질수록 여러 생성자가 필요하다
- 생성자 파라미터 갯수가 많아질수록 불편하다
  > 순서를 혼동하기 쉽다  
  > 가독성이 낮아지고, 유지보수에 불편함이 생긴다

#### 수정자(Setter) 의 문제

- 객체 속성의 수정가능성을 계속 열어두기 때문에 객체불변성을 보장할 수 없어진다
- 값을 변경하는 의도롤 파악하기 어렵다

**_하지만 빌더 패턴을 사용한다면_**

- 객체의 속성을 각각 단계별로 설정할 수 있기 때문에 생성 과정이 명확해진다
- 객체의 불변성을 보장할 수 있다
- 필요한 속성만을 설정할 수 있기때문에 여러 생성자를 만들 필요가 없다

따라서, 생성자와 수정자의 사용을 지양하며 대신 사용할 수 있는 해결책이다
