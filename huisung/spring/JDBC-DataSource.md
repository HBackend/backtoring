# JDBC, DataSource

## JDBC
- DB에 쉽게 접근할 수 있도록 도와주는 자바의 API이다.
- JDBC를 사용하면 종속적이지 않은 DB연동을 구현할 수 있다.
> ex. mysql을 쓰다가 postgres로 쉽게 변경이 가능하다.
- JDBC는 데이터베이스에 대한 연결, 쿼리 실행, 결과 처리 등을 처리하기 위한 인터페이스와 클래스를 제공한다.

* Spring JDBC는 JDBC를 더 쉽고 효율적이게 사용할 수 있도록 도와준다.ㅌㄴ

**JdbcTemplate** 같은 객체를 사용하면 JDBC 작업을 간편하게 수행할 수 있게 도와준다.

```java
@Repository
public class UserJdbcRepository {

    private final JdbcTemplate jdbcTemplate;

    public UserJdbcRepository(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }
    
    ...

    public void saveUserName(String name, Integer age) {
        String sql = "INSERT INTO user (name, age) VALUES (? ,?)";
        jdbcTemplate.update(sql, name, age);
    }

    public void updateUserName(String name, long userId) {
        String sql = "UPDATE user SET name = ? WHERE id = ?";
        jdbcTemplate.update(sql, name, userId);
    }
}
```

- 이렇게 쿼리문을 작성한다. 데이터를 넣을 곳은 `?`로 작성한다. 
- 주입받은 jdbcTemplate의 update 메서드로 쿼리문과 `?` 부분이 넣을 데이터를 아규먼트로 전달한다.

* jdbcTemplate.update는 insert, update, delete 쿼리에 사용할 수 있다.
* jdbcTemplate.query으로는 select 쿼리에 사용할 수 있다.
  - ```jdbcTemplate.query(sql, RowMapper 구현 익명클래스)```

## DataSource

- 데이터베이스와의 연결을 관리하는 객체로 데이터베이스와 관련된 연결 정보를 포함하여 디비의 빠른 연결을 제공한다.
