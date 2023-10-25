# Spring URL HandlerMapping

- 핸들러 매핑은 HTTP 요청의 정보를 이용하여 알맞는 컨트롤러를 찾아주는 기능을 수행한다.
- 디스패처 서블릿이 등록된 핸들러 매핑 전략들에게 `HttpServletRequest`를 전달하면서 매핑되는 객체를 찾는다.

### `DispatcherServlet`
- 요청이 오면 해당 요청을 제일 먼저 받고 알맞은 컨트롤러를 찾아 정해주는 역할을 한다. 
- 스프링 MVC의 중앙 서블릿이며 애플리케이션으로 오는 모든 요청을 핸들링하고 공통된 작업을 처리해준다.
- 디스패처 서블릿을 **프론트 컨트롤러** 라고도 한다

> 디스패처 서블릿 요청 처리 과정 : 요청을 처리할 컨트롤러를 찾음 -> (없다면) 정적 자원을 탐색   

> 서블릿 : 클라이언트의 요청을 처리하고, 그 결과를 반환하는 기술
## BeanNameUrlHandlerMapping
- 빈의 이름에 들어있는 URL을 요청의 URL과 비교하여 일치하는 빈을 찾아주는 역할을 한다.
- 가장 직관적이고 쉬운 핸들러 매핑 전략.
- 컨트롤러가 많아질수록 URL정보가 복잡해지므로 규모가 큰 애플리케이션에선 잘 사용하지 않음

## ControllerBeanNameHandlerMapping
- 위의 방식과 비슷하지만 빈 이름앞에 `/`를 붙혀 URL 매핑을 진행하므로 빈 이름을 URL 형태로 짓지 않아도 되는 장점이 있다.

## ControllerClassNameHandlerMapping
- 빈의 클래스 이름으로 URL 매핑을 진행한다.
- 클래스 이름이 Controller 로 끝난다면 Controller 를 뺀 나머지 이름을 URL 매핑 해준다.

## SimpleUrlHandlerMapping
- URL과 컨트롤러 매핑 정보를 한 곳에 모아놓는 전략이다.

## RequestMappingHandlerMapping
- `@RequestMapping` 이라는 어노테이션을 이용하여 매핑을 진행한다.
- 클래스에 적용하는것 뿐 아니라 메서드 단위에서도 매핑이 가능하고 다양한 정보도 매핑할 수 있어서 현재 가장 많이 사용된다.