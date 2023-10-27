## @RequestBody, @ResponseBody

#### @RequestBody

클라이언트로부터 전송받은 요청의 본문(body) 부분을 자바 객체로 변환하거나 바인딩 할 때 사용되는 어노테이션

- JSON, XML과 같은 형식의 데이터를 요청으로 받아 Java 객체로 변환하기 위해 사용
- @RequestBody를 사용하여 받은 데이터는 Spring의 HttpMessageConverter를 사용하여 객체로 변환된다 (데이터 -> 객체)

```java
@RestController
public class UserController {

    @PostMapping("/user")
    public User createUser(@RequestBody User user) {

        return userService.createUser(user);
    }
}
```

> requset에서 받은 데이터를 자바 User 타입의 user 객체로 HttpMessageConverter에 의해 변환후 사용

위처럼 HTTP 요청 본문의 내용을 Java 객체로 변환할 때, 객체의 역직렬화를 통해 객체를 생성한다

#### Json 데이터 -> Java 객체 변환 과정

1. **기본 생성자를 통한 객체 생성**  
   jackson과 같은 (역직렬화) 라이브러리가 기본생성자 호출을 통해 객체의 초기 인스턴스를 생성한다  
   이때 생성된 인스턴스는 기본생성자를 통해 생성되었기때문에 필드들은 모두 기본값을 갖는다

2. **필드 값 대입**  
   JSON의 키-값 쌍을 읽어나가면서, 해당 키에 해당하는 Java 객체의 필드에 값을 대입한다  
   이 과정에서 리플렉션을 통해 객체의 private 필드에도 값을 직접 넣을 수 있다

3. 객체 완성

> 하지만 기본생성자가 없더라도 모든 생성자를 초기화가 불가능한 것은 아니다

추가적으로, @RequsetBody에는 `required`라는 속성을 선택적으로 부여할 수 있는데

```java
public User createUser(@RequestBody(required = false) User user) {
    ...
}
```

와 같이 코드를 작성한경우에는  
요청의 body에 데이터가 포함되지 않은 경우를 허용하며, 데이터를 null값으로 대신하여 메서드를 사용할 수 있다

---

#### @ResponseBody

컨트롤러의 메소드에서 반환하는 자바 객체를 응답 본문(body)으로 전송하기 위한 어노테이션

- 메소드의 반환값을 HttpMessageConverter를 사용하여 응답 본문으로 변환
- 주로 MappingJackson2HttpMessageConverter에 의해 JSON 형식으로 변환하여 응답

```java
public class UserController {

    @GetMapping("/users/{id}")
    @ResponseBody
    public User getUser(@PathVariable Long id) {
        // 사용자 조회 로직
        return user;
    }
}
```

> response에 user객체를 담아 반환하는데, 이때 HttpMessageConverter에 의해 Json 형식으로 변환

일반적으로 @Controller 어노테이션이 붙은 클래스에서 return을 할 때, view의 이름으로 반환을 받기때문에  
메서드의 반환 데이터를 HTTP 응답의 본문으로 하고자 할 때 해당 어노테이션을 사용한다

> 반면, @RestController를 사용하면 내부적으로 @Controller와 @ResponseBody를 포함하고 있기때문에 해당 어노테이션을 따로 작성해주지 않아도 메소드의 반환값을 HTTP 응답의 본문으로 사용되게 한다

> 따라서 @RestController와 @ResponseBody는 중복으로 작성할 필요가 없게된다

@RequestBody와 @ResponseBody는 Spring에서 HTTP **요청 및 응답 본문과 자바 객체 사이의 변환을 쉽게** 해주고,  
이를 사용하면 RESTful API 구현 시 **_데이터를 쉽게 처리_**할 수 있다
