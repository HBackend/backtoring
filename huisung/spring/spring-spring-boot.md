## 스프링과 스프링 부트 개념의 차이

## 스프링 프레임워크란
- 자바 애플리케이션 개발을 지원하는 오픈소스 프레임워크이다.
- 스프링의 주요 특징에는 아래와 같은 것이 있다.
  - IOC(Inversion of Control) 제어의 역전
  - DI(Dependency Injection) 의존성 주입
  - AOP(Aspect Object Programming) 관점 지향 프로그래밍
  - PSA(Portable Service Abstraction) 서비스 추상화

### 스프링의 단점
- 복합한 설정
  - 스프링의 기능을 사용하기 위해선 많은 설정과 구성이 필요하다.
  - 컨텍스트 설정, 빈 정의, 다양한 컴포넌트 구성을 위해 많은 설정 코드를 작성해야하고 이는 초기 설정의 어려움을 가져온다.
- 의존성 관리 문제
  - 스프링에선 여러 의존성과 버전 관리가 복잡했다.
  - 의존성 주입(DI)을 구현하기 위해 XML 설정파일에 수 많은 빈을 등록해야 했었다.
- WAS 서버 구성 
  - 스프링을 구동하려면 별도로 WAS를 설치하고 설정하여 서버에 수동으로 배포해야하는 번거로움이 있었다.
  > WAS(Web Application Server): 간단한 웹 애플리케이션을 실행하기 위한 장치
  

## 스프링 부트 프레임워크
- 스프링은 장점이 많지만 그만큼 매우 복잡하다는 단점이 있다. 이런 단점을 보완하고자 스프링 부트가 개발되었다
- 스프링 부트는 스프링을 더 쉽고 빠르게 이용할 수 있도록 만들어주는 도구이다. 의존성 세트라고 불리는 스타터를 이용하여 간편하게 의존성을 관리할 수 있다.

### 스프링 부트의 특징
- 구성의 차이
  - 스프링은 개발에 필요한 환경을 수동으로 구성하고 정의했던 반면에   
  스프링 부트는 스프링 코어와 스프링 MVC의 모든 기능을 자동으로 로드하므로 수동으로 구성할 필요가 없다.

- 내장 WAS
  - 스프링은 일반적으로 톰캣과 같은 WAS에서 구동된다.
  - 스프링 부트는 WAS를 자체적으로 가지고 있으며 jar 파일만 있다면 별도의 WAS설정 없이 애플리케이션을 배포할 수 있다.