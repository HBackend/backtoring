# try-catch, throw, throws

### 예외 처리 방법
1. try-catch
2. throws
3. throw

## try-catch
```java
try {
    // 예외가 생길 가능성이 있는 코드
} catch (예외 클래스 error) {
    // 예외 처리 코드
}
```
- try - catch 구문의 형태

```java
public static void main(String[]args){
    try {
        System.out.println(10 / 0);
    } catch (Exception error) {
        System.out.println(error);
    }
}
```
- 이렇게 예외를 잡을 수 있다.

### try-catch-finally
- finally 절을 추가할 수 있다.
- 예외가 발생했든 안했든 finally 절의 구문이 실행된다.

```java
public static void main(String[]args){
    try {
        
    } catch (Exception error) {
        
    } finally {
        
    }
}
```

### try-with-resource
- `try-catch`의 변형 문법이다. `try-with-resource` 는 자원을 할당하는 부분을 명시하면 try 블록이 끝날 때 자동으로 할당한 자원을 해제해준디.

```java
try (자원을 할당하는 부분) {
    ...
}
```

> 예시
```java
public class Main {
    public static void main(String[] args) {
        String str;
        try (
            Scanner scanner = new Scanner();
        ) { str = scanner.next(); }
        finally {
            System.out.println(str);
        }
    }
}
```


## throws
- 자신을 호출하는 메서드에 예외처리를 떠넘기는 것이다.

```java
public static void main(String[]args){
    int a = 10, b = 0;
    
    try {
        test(a, b);
    } catch (ArithmeticException error) {
        System.out.println(error);
    }
}

public static test(int a, int b) throws ArithmeticException { // 산술 에러
    System.out.println(a / b);
}
```
- test 메서드 뒤에 `throws ArithmeticException` 이 부분은 해당 예외가 발생하면 이 메서드를 호출한 곳 (즉 main) 에서 예외처리를 해야한다는 뜻이다!
- 예외처리를 넘겨받은 메서드에선 반드시 try-catch 구문으로 감싸서 예외처리를 해야한다

## throw
- 직접 예외를 발생시키고 싶을 때 쓰는 것이다.
- `RuntimeException` 예외를 처리할 때 쓰는 방식이다.

```java
throw new IllegalArgument("잘못된 인자 값");
```