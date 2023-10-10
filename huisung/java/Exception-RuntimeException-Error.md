# Exception, RuntimeException, Error

## Exception vs Error
### Error (에러)
- 컴퓨터 프로그램의 오작동, 고장 등으로 인해 응용프로그램 실행에 오류가 발생하는 것
- 실행 불능이 됨
### Exception (예외)
- 잘못된 조작, 개발자의 실수로 인해 발생하는 프로그램의 오류
- 예외가 발생하면 프로그램이 바로 종료된다 (에러와 동일).
- 예외 처리를 하여 프로그램을 종료하지 않고 실행 상태를 유지할 수 있다.

## 예외의 종류
- 자바에서는 예외를 클래스로 관리한다. (java.lang.Exception)

### 일반 예외
- 컴파일 과정에서 발견되는 예외이다.
- Exception을 상속받는다.
> IOException 같은 예외이다.

### 런타임 예외
- 컴파일 과정에서 예외 처리 코드를 검사하지 않는 예외이다.
- RuntimeException과 Exception을 상속받는다.
> NullPointerException 같은 예외이다.
> try-catch 문을 사용하여 예외 처리 가능

![](https://img1.daumcdn.net/thumb/R1280x0/?fname=http://t1.daumcdn.net/brunch/service/user/xTa/image/EV_9X_vwDtwXTsoqr6cviQLUTAg.png)

## Throwable class
- Throwable 클래스는 자바의 오류, 예외의 슈퍼 클래스이다.

### checked exception
- 반드시 예외 처리를 해야하는 예외이다.
- 컴파일 단계에서 확인된다.

### unchecked exception
- 예외 처리가 강제되지 않는다.
- 런타임 단계에서 확인된다.
