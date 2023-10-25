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