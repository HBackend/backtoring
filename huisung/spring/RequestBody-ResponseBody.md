# RequestBody, ResponseBody

- 서버와 클라이언트가 요청과 응답을 할 때 요청의 본문 (RequestBody)에 데이터를 담아서 요청을 하고, 응답의 본문(ResponseBody)에 데이터를 담아서 응답을 준다.
- 스프링에서 해당 요청과 응답의 requestBody와 responseBody의 데이터를 바인딩할 때 사용하는 어노테이션은 `@RequestBody` `@ResponseBody` 가 있다.

## `@RequestBody`
-  해당 어노테이션은 서버에 온 http 요청의 body의 json을 자바 객체로 매핑 시켜준다.

```java
@PostMapping
public ResponseEntity<MsgResponseDto> saveMember(@RequestBody @Valid SaveMemberRequest request) {
        ...
    return ResponseEntity.ok(new MsgResponseDto("맴버 생성 완료.", HttpStatus.CREATED.value()));
}
```
- 이렇게 json으로 들어오는 데이터를 자바 객체로 받을 수 있다.

```json
{
  "name" : "khm",
  "age" : 18
}
```
```java
// SaveMemberRequest
@Getter
public class SaveMemberRequest {
    private String name;
    private Integer age;
}
```

- 위의 json 데이터가 해당 객체와 매핑된다.


## `@ResponseBody`
- @RequesyBody와 반대로 자바 객체를 json 데이터 형태로 변환하여 http body에 담는 어노테이션이다.
```java
@Controller
public class MemberController {

@GetMapping
@ResponseBody
public MemberDto getMember() {
        ...
    return member;
}

...
```
- 이렇게 사용하면 자바 객체를 응답 http body 데이터 형식으로 변환된다.


### HTTP 메시지 컨버터
- HTTP 요청 또는 응답의 바디의 JSON 데이터를 객체로 변환하거나, 객체를 HTTP 요청 또는 응답의 바디의 JSON으로 변환하는 기능을 제공한다.
- JSON 데이터를 HTTP 메시지 바디에서 직접 읽거나 쓰는 경우 HTTP 메시지 컨버터를 사용할 수 있다.
- HttpMessageConverter 인터페이스에 read(), write() 등 메시지를 읽고 쓸 수 있는 기능 같은 메서드들이 선언되어있다.

### ArgumentResolver
- ArgumentResolver 를 호출하여 다양한 파라미터를 생성하여 컨트롤러에게 넘겨준다.

> ArgumentResolver 를 사용하여 `@RequestParam` 어노테이션을 처리하는 예시이다.
```java
@GetMapping("/user")
public void getUser(@RequestParam("id") int userId) {
        ...
}
```

### @RestController / ResponseEntity

### @RestController
- @RestController 를 컨트롤러 클래스에 작성하면 자동으로 모든 핸들러에 `@ResponseBody` 어노테이션이 적용되어 생략이 가능하다.


```java
@RestController
public class MemberController {

@GetMapping
// @ResponseBody
public MemberDto getMember() {
        ...
    return member;
}

...
```

### @RequestBody의 dto 객체는 기본 생성자와 getter가 필요하다
- `ObjectMapper` 는 getter/setter 로 dto의 필드를 가져온다.
- 값을 초기화 해줄때는 reflection을 사용해서 필드에 값을 넣어준다.
    > reflection : 구체적인 클래스 타입을 몰라도 해당 클래스의 메서드, 필드에 접근할 수 있게 해주는 자바 API


### @ResponseBody 가 작성된 데이터에 기본 생성자가 필요하다.
- RestController에서 @ResquestBody를 바인딩 하기 위해 ObjectMapper를 사용하는데 기본 생성자로 해당 dto를 생성하기 때문이다! 

#### ObjectMapper
- JSON to 객체(역직렬화), 객체 to JSON(직렬화) 하기 위헤 사용하는 Jackson 라이브러리의 클래스이다.

### ResponseEntity
- 반환값에 상태코드와 데이터 주고 싶을 때 사용한다.

```java
@GetMapping
public ResponseEntity<Member> getMember() {
        ...
    return ResponseEntity.ok(member);
}
```

`ResponseEntity.ok( 데이터 )`
`ResponseEntity.created( 데이터 )`   
등 http 상태코드와 데이터를 함께 보낼 수 있다.   

추가로 RequestEntity는 응답 헤더, body 양식을 맞추어 반환해주므로 @ResponseBody를 붙히지 않아도 잘 작동한다.

**ResponseEntity를 사용하지 않고 응답 상태코드를 지정하는 방법**

```java
@GetMapping("/user")
void user(HttpServletResponse response) {
    ...
    response.setStatus(HttpServletResponse.SC_OK);
}
```

- `HttpServletResponse` 를 메서드의 파라미터로 받아와서 직접 응답의 상태코드를 지정할 수 있다.

> `@ResponseStatus` 어노테이션을 사용하여 응답의 상태코드를 지정할 수도 있다.
```java
@GetMapping("/user")
@ResponseStatus(HttpStatus.OK)
void user( ... ) {
  ...
}
```