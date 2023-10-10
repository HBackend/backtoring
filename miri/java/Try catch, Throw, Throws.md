## Try catch, Throw, Throws

Try catch, Throw, Throws는 Java에서 예외관련 처리를 할때 사용되는 키워드들이다

### Try catch

try 블록의 코드를 수행하는중, 해당 코드에서 예외가 발생한다면 catch문으로 즉시 넘어간다  
catch문에서 예외를 처리한 이후 finaily문을 선택적으로 추가하여 실행한다

```java
try {
    // 예외가 발생할 수 있는 코드
} catch (예외타입 예외변수) {
    // 예외를 처리하는 코드
} finally {
    // 무조건 실행되는 코드
}

```

### try-with-resouces 문

> try-catch-finaliy문에서 필요한 자원을 닫아주는 작업을 자동으로 제공한다

```java
try (리소스 선언) {
    // 리소스를 사용하는 코드
} catch (예외 타입 예외 변수) {
    // 예외 처리 코드
}
```

### Thorw

어떠한 조건이 충족되지 않았을 때 이에 대한 처리를 예외처리로 할 수 있도록 자체적으로 예외를 발생시키는 것

```java
if () {
    throw new SomeException("error");
}

```

### Thorws

메서드 선언부에 해당 키워드를 사용하여, 해당 메서드의 실행에서 발생한 예외를 메서드를 호출한 부분으로 던져주어 처리하게 하는 것  
throws 뒤에 해당 메서드에서 발생할 수 있는 예외 종류들을 나열함

```java
public void Method() throws ExceptionType, ExceptionType2 {

}
```

---

세 키워드를 사용한 예외처리의 예시

```java
public class ExceptionTest {
    // 예외 클래스 정의
    public static class ExceptionEx1 extends Exception {
        public ExceptionEx1(String message) {
            super(message);
        }
    }

    public static void ExceptionTestMethod(매개변수) throws ExceptionEx1 {
        if () {
            throw new ExceptionEx1("에러메세지");
        }
    }

    public static void main(String[] args) {
        try {
            ExceptionTestMethod(인자);
        } catch (ExceptionEx1 e) {
            // 예외 처리 로직

        }
    }
}

```
