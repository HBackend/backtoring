## Optional class

### Optional class란?

null이 올 수 있는 값을 감싸주어 NPE를 방지할 수 있도록 도와주는 Wrapper 클래스  
이러한 옵셔널 클래스를 통해 사용할 수 있는 다양한 메서드 또한 제공한다

값을 감싸고 푸는 동작을 실행하는 과정에서 시스템 성능의 저하를 방지하기 위해서는 NPE가 발생할 가능성이 매우 높은 경우에만 사용하는것이 좋다

---

#### 값이 Null인 경우

Optional.empty()

- 값이 비어있는 Optional 객체를 반환
- 참조해도 NPE가 발생 안함

```java
Optional<String> optional = Optional.empty();
```

#### 값이 Null이 아닌 경우

Optional.of()

- 명시된 값을 가지는(null이 아닌) Optional 객체를 반환
- null값이 저장되면 NPE 발생

```java
Optional.of();
```

#### 값이 Null일수도, 아닐수도 있는 경우

Optional.ofNullbale()

- 경우에 따라 null값을 담은 객체를, 또는 명시된 값을 가지는 Optional 객체를 반환

```java
Optional.ofNullable();
```

---

#### 저장된 값의 null 여부 판별

isPresent()

- boolean 타입
- 저장된 값이 존재하면 true를, 값이 존재하지 않으면 false를 반환

```java
if (memberID.isPresent()) {

}
```

#### Optional class 의 값 가져오기

Optional.get()

- 객체에 저장된 값에 접근하여 값을 가져오는 메소드

```java
System.out.println(memberID.get());
```

#### 객체에 저장된 값이 null일때 대체 값 지정

`orElse(인수)`

- 저장된 값이 존재하지 않으면 인수로 전달된 값을 반환

`orElseGet()`

- 저장된 값이 존재하지 않으면 인자로 전달된 식의 결과를 반환

`orElseThrow()`

- 저장된 값이 존재하지 않으면 예외를 발생시킴
