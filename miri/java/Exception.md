## Exception, RuntimeException, Error

Java에서는 프로그램의 실행을 기점으로, 실행 전 컴파일 시점에 발생하는 Exception과 프로그램이 실행되는 도중 발생하는 RuntimeException 2가지로 구분한다

> 예외처리 클래스에는 **최상위 예외클래스**인 `Throwable` 클래스를 상속받는 `Exception`, `Error` 두가지의 주요 서브클래스로 이루어져있고  
> 각각 다양한 예외와 오류를 나타내는 클래스들이 하위에 정의되어있다

또한, 프로그램이 실행되는 도중 발생될 수 있는 런타임에러를 RuntimeException과 Error로 구분한다

> 컴파일 타임 (Compile Time) 이란
>
> - 소스코드가 컴파일러에 의해 기계어로 변환되는 과정
> - 해당 과정에서 컴파일 오류(Exception)를 잡아낸다

> 런타임 (Run Time) 이란
>
> - 컴파일 이후 프로그램이 실제로 실행되는 과정
> - 이때 발생하는 오류를 런타임 오류(RuntimeException)라고 한다

### 예외 처리란?

프로그램 실행중 RuntimeException이 발생할 것을 대비하여 이를 미리 제어하고 처리하도록 만드는 것

### Exception

프로그램의 실행 전 컴파일러를 통해 처리할 수 있거나, 프로그래머가 직접 예측하여 예외처리를 통해 막을 수 있는 처리가능한 오류

**CheckedException, UncheckedException이란?**

> `CheckedException` 컴파일 타임에 체크되는 예외, 컴파일러가 코드를 컴파일하는 과정에서 잡아내는 오류

> `UncheckedException` 런타임에 발생하는 예외, 컴파일타임에 별도로 체크되지 않는 오류

CheckedException 예시

- `IOException`

UncheckedException 예시

- `NullPointerException`

### Error

시스템 자체에서 발생하여 대부분의 경우 애플리케이션에서 복구할 수 없는 수준의 오류

Error 예시

- `StackOverflowError`
- `OutOfMemoryError`

  > 메모리 영역이 프로그램 실행에 있어서 부족할 때
  > **_OutOfMemoryError_**가 발생하는데,이를 방지하기 위해서는 **불필요한 객체 생성을 최소화**하고, **로직을 수정**하는등 메모리 사용을 최적화하여 해결할 수 있다
