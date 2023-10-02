# 레퍼 클래스, 오토래핑, 언래핑

## 래퍼 클래스
- 기본 타입의 데이터를 객체로 다루기 위해 기본 자료형 8개를 포장해서 클래스화 한 것이다.
- 제네릭, 자료구조, 매개변수 등 기본 자료형이 아닌 래퍼런스 타입을 필요로 하는 경우가 많고 유용한 메서드들을 가지고 있어 다양하게 활용 가능하다.
  - `원시 타입` : 정수, 실수, 등의 실제 데이터의 값을 저장하는 타입 `ex. int, float ..`
  - `참조(래퍼런스) 타입` : 객체를 참조하는 메모리 주소 값을 저장하는 타입 `ex. Integer, Float, Object ..`
- null 값을 표현할 수 있다.
  - 이렇게 null 값을 표현할 수 있어 값이 없는 상태를 명확이 표현할 수 있다.
  - ```java
    int num1 = null; // error
    Integer num2 = null;
    ```

| 기본 자료형  | Wrapper class |   
|---------|--------|
| int     | Integer |
| boolean | Boolean|
| char    | Character |
| float   | Float |
| double | Double |
| long | Long |

```java
Integer num = new Integer(100);
```

### 래핑, 언패링
- **래핑**은 기본 자료형의 데이터를 래퍼 클래스의 객체로 만드는 과정
- **언래핑**은 래퍼 클래스의 데이터를 기본 자료형으로 얻어내는 과정

### 래핑 방법
- new 연산자를 사용하여 생성
```java
public static void main(String[]args) {
        int i = 100;   
        Interger wi = new Integer(i);
}
```
- wrapper class의 valueOf() 메서드를 사용하여 생성
```java
public static void main(String[]args) {
        int i = 100;   
        Interger wi = Integer.valueOf(i);
}
```
> int -> Integer (래핑)

### 언래핑 방법
- wrapper class의 메서드를 사용하여 생성
  - `기본자료형Value()`
```java
public static void main(String[]args){
    int i = 100;
    Integer wi = new Integer(i); // 래핑
    int ii.w1.intValue(); // 언래핑
}
```

### 오토래핑, 오토언래핑
- JDK 1.5 부터 오토래핑, 오토언래핑을 지원한다.
- 위의 래핑, 언래핑하는 방법을 사용하지 않고도 간단히 변환이 가능하다. (컴파일러가 자동으로 변환해줌)
- 방밥은 오토래핑은 래퍼 클래스에 기본 자료형 데이터를, 오토 언래핑은 기본 자료형에 래퍼 객체를 대입하면 된다.
```java
public static void main(String[]args){
    int i = 100;
    Integer wi = i; // 오토 박싱
    int ii = w1; // 오토 언박싱
}
```