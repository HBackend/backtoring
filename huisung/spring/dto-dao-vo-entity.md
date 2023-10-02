# DTO DAO VO Entity

## DTO (Data Transfer Object)

- 계층간 데이터 교환을 위해 사용하는 객체이다.
- DB에서 가져온 데이터를 다른 계층에서 사용하기 적합한 형식으로 변환하여 전송하는데 사용한다!
- response / request 에서 사용할 수 있다.

```java
@Getter
@Setter
public class AddUserRequest {
    private String email;
    private String password;
}
```

## DAO (Data Access Object)

- Database에 접근하여 CRUD를 수행한다.
- Service와 DB를 연결한다.
- Repository package가 DAO이다.

* repository와 dao는 비슷한 개념이다.
    - repository는 Entity 객체를 보관하고 관리하는 저장소, dao는 데이터에 접근하도록 DB접근 관련 로직을 모아둔 객체이다.

> UserDao 인터페이스
```java
public interface UserDao {
void save(User user);
List<User> findAll();
void update(User user);
void delete(int id);
}
```

```java
@Respository
public class UserDaoJdbc implements UserDao {

    @Override
    public void save(User user) {
        ...
    }

    @Override
    public List<User> findAll() {
        ...
    }

    @Override
    public void update(User user) {
        ...
    }

    @Override
    public void delete(int id) {
        ...
    }
}
```

## VO (Value Object)

- Read-Only 속성을 지닌 값 오브젝트이다.
- DTO는 인스턴스 개념이고, VO는 리터럴 값 개념이다.
- 두 객체의 모든 필드 값들이 동일하면 두 객체는 같다.
    - 완전히 값 자체 표현 용도로만 사용하는 목적이기 때문이다.

```java
public class Address {
    private String street;
    private String city;
    private String state;
    private String postalCode;

    public Address(String street, String city, String state, String postalCode) {
        this.street = street;
        this.city = city;
        this.state = state;
        this.postalCode = postalCode;
    }

    // getter 메서드

    // 기타 메서드
}
```

## Entity

- 실제 DB 테이블과 매핑되는 클래스이며 Entity를 기준으로 테이블이 생성된다.
- 데이터를 전달하는 클래스로 사용하면 안된다.
- Entity는 비즈니스 로직을 포함할 수 있다.

```java
@Entity
@Getter
@NoArgsConstructor(access = AccessLevel.PROTECTED)
public class Article {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id", updatable = false)
    private Long id;

    @Column(name = "title", nullable = false)
    private String title;

    @Column(name = "content", nullable = false)
    private String content;

    public void update(String title, String content) {
        this.title = title;
        this.content = content;
    }
}
```

## +) record

- 불변 데이터를 표현하는데 사용한다.
- 클래스이므로 interface 구현, extends 가능하다.
- constructor / getter 메서드를 컴파일러가 자동생성 해준다.

```java
public record ReadBoardsResponse(Long id, String title, String createBy) {
}
```
