# Optional class
- 어떤 타입의 객체를 포장해주는 래퍼 클래스이며, null이 올 수 있는 값을 감싼다.
- 참조하더라도 `NullPointerException` 에러가 발생하지 않게 도와준다.
  - ```java
    List<Integer> numbers = new ArrayList<>();
    ...
    numbers.sort(); // null일 시 NPE가 발생
    ```
    
## Optional 객체 생성

### 값이 비어있는 경우
- `Optional.empty()`
- Optional은 빈 값이 올 수 있기 때문에 빈 객체는 `Optional.empty()` 를 사용하여 생성 가능하다.
```java
Optional<Integer> number = Optional.empty();
```

### 값이 null이 아닌 경우
- `Optional.of()`
- 어떤 값이 절대 null이 아닌 경우에는 `Optional.of(값)` 이렇게 생성 가능하다.
- 만약 null을 저장하려고 하면 `NullPointerException` 이 발생한다!
```java
Optional<Integer> number = Optional.of(123);
```

### 값이 null일 수 있는 경우
- `Optional.ofNullable()`
- null이 허용될 수 있는 경우 `Optional.ofNullable(값)` 이렇게 생성한다.
```java
Optional<Integer> number = Optional.ofNullable(null);
```

### 값이 있는지 없는지 체크
- `.isPresent()`
- boolean 타입이며 Optional 객체가 값을 가지고 있다면 true, 없다면 false를 리턴한다.
- `isPresent()` 를 사용하여 `!= null` 과 같은 조건식을 없앨 수 있다.
```java
Optional<String> name = getName();

if (name.isPresent()) {
    System.out.println("존재 하다.");    
}
```

- `.ifPresent()`
- Optional 객체가 값을 가지고 있으면 실행 값이 넘어감.
```java
boardRepository.findById(id).ifPresent(board -> { System.out.println("존재 하다."); })
```

### get()
- Optional 객체에 저장된 값에 접근한다.
- null 이라면 `NoSuchElementException` 예외 발생

```java
Optional<String> str = Optional.ofNullable("hello");

System.out.println(str.get());
```

### orElse()
- Optional 객체의 값이 null 이라면 아규먼트로 전달된 함수를 실행시킨다.
```java
Optional<String> nullString = Optional.ofNullable(null);

String str = nullString.orElse("없따.");
```

### orElseGet()
- Optional 객체가 null 이라면 아규먼트로 전달된 함수의 리턴 값을 리턴한다.
```java
Optional<String> nullString = Optional.ofNullable(null);

String str = nullString.orElseGet(() -> "없따.");
```

### orElseThrow()
- Optional 객체가 null 이라면 아규먼트로 전달된 예외를 발생시킴
```java
Optional<String> nullString = Optional.ofNullable(null);

String str = nullString.orElseThrow(NullPointerException::new);
```

