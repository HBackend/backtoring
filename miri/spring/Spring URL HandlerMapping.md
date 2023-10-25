## Spring URL Handler Mapping

#### Spring URL Handler Mapping 이란?

Spring MVC 패턴에서 클라이언트의 request를 받았을 때  
요청받은 url를 기반으로 **해당 요청을 어떤 Controller의 어떤 메소드에서 처리할 것인지를 결정**하는 것

> 즉, 요청을 받았을 때 그 요청을 처리하기에 적절한 handdler를 찾는 역할

Spring MVC 패턴에는 다음과 같은 Handler Mapping 전략들이 있다

### BeanNameUrlHandlerMapping

기본적으로 사용되는 핸들러 맵핑 전략

- 빈의 이름이 URL 패턴으로 사용

### SimpleUrlHandlerMapping

- 설정 파일(Java Config 등)에서 URL 패턴과 빈 이름을 직접 매핑하여 지정

### ControllerClassNameHandlerMapping

- Controller의 클래스 이름을 기반으로 URL 패턴을 생성

### RequestMappingHandlerMapping

가장 많이 사용되는 핸들러 맵핑 전략

- @RequestMapping 어노테이션이 붙은 메소드나 클래스를 찾아 URL 패턴과 매핑
