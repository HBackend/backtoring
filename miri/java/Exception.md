## Exception, RuntimeException, Error

Java에서는 프로그램의 실행을 기점으로, 실행 전 컴파일 시점에 발생하는 Exception과 프로그램이 실행되는 도중 발생하는 RuntimeException 2가지로 구분한다  
또한, 프로그램이 실행되는 도중 발생될 수 있는 런타임에러를 RuntimeException과 Error로 구분한다

### 예외 처리란?

프로그램 실행중 RuntimeException이 발생할 것을 대비하여 이를 미리 제어하고 처리하도록 만드는 것

### Exception

프로그램의 실행 전 컴파일러를 통해 처리할 수 있거나, 프로그래머가 직접 예측하여 예외처리를 통해 막을 수 있는 처리가능한 오류

> Exception 예시

- `IOException`
  > RuntimeException 예시
- `NullPointerException`

### Error

시스템 자체에서 발생하여 대부분의 경우 애플리케이션에서 복구할 수 없는 수준의 오류

> Error 예시

- `OutOfMemoryError`
- `StackOverflowError`
