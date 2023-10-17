# JDBC, DataSource

## JDBC
- DB에 쉽게 접근할 수 있도록 도와주는 자바의 API이다.
- JDBC는 데이터베이스에 대한 연결, 쿼리 실행, 결과 처리 등을 처리하기 위한 인터페이스와 클래스를 제공한다.
- Spring JDBC는 JDBC를 더 쉽고 효율적이게 사용할 수 있도록 도와준다.


**서버가 데이터베이스와 통신할 때 아래와 같은 과정이 진행된다.**
1. 커넥션 연결
    - TCP, IP를 통해 연결
2. SQL 전달
    - 연결된 커넥션으로 서버에 SQL 쿼리 전달
3. 결과 응답
    - 서버는 쿼리를 실행하고 서버에 전달

* JDBC를 사용하면 종속적이지 않은 DB연동을 구현할 수 있다.
> ex. mysql을 쓰다가 postgres로 쉽게 변경이 가능하다.

- 개발자는 JDBC Interface만 의존하여 코드를 작성하면 된다,
 JDBC Interface의 구현체는 각 DB별로 가지고 있다. (드라이버)
- DB 라이브러리를 추가하면 JDBC Driver Manager가 드라이버를 찾아 연결해준다.

### JDBC Drivcer Manager
- JDBC DriverManager는 url을 분석하여 드라이버 목록을 자동으로 인식하고 관리한다.
- 이 드라이버들에게 순서대로 데이터베이스 접속 정보를 전달해 커넥션을 획득할 수 있는지 확인한다.

```java
Connection connection = DriverManager.getConnection(url, db_username, db_password);
```

```java
public class DatabaseConnection {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/testdb"; 
        String username = "root"; 
        String password = "12345"; 

        try {
            Class.forName("com.mysql.jdbc.Driver");
            Connection connection = DriverManager.getConnection(url, username, password);

            if (connection != null) {
                System.out.println("데이터베이스 연결 성공!");
                // 작업 수행
                connection.close();
            } else {
                System.out.println("데이터베이스 연결 실패!");
            }
    }
}
```

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

### JDBC Driver
- 자바 애플리케이션과 데이터베이스를 연결하도록 하는 자바 API이다.
- 일반적으로 데이터베이스와의 연결을 설정하고 데이터를 쿼리하는데 사용한다.
- 각각의 DBMS는 자신에게 알맞는 JDBC Driver를 제공한다.

### JDBC 실행과정
1. JDBC 드라이버 로드
2. Connection 객체 생성
3. Statement 객체 생성
4. Query 실행
5. Result 객체로부터 데이터 추출
6. Result 객체 close
7. Statement 객체 close
8. Connection 객체 close

#### Connection : DB 연결 객체
#### Statement : SQL 실행 객체
#### ResultSet : select 쿼리의 결과를 가지는 객체


### DataSource
- 데이터베이스 연결을 관리하는 객체로, JDBC에서 데이터베이스와의 연결을 설정하고 관리하기 위해 사용된다.
- 연결을 설정하기 위해서는 DB URL, 사용자 이름, 비밀번호 같은 정보가 필요하다.
이러한 정보를 하드코딩하는 것은 보안에 취약하기 때문에 DataSource를 사용한다.

```yml
datasource:
  url: jdbc:mysql://localhost:3306/test-db
  username: root
  password: 0000
  driver-class-name: com.mysql.cj.jdbc.Driver
```

- 커넥션 풀링을 관리할 수 있어 애플리케이션 성능을 향상 시킬 수 있다.
-  커넥션 풀링은 데이터베이스 연결을 미리 만들어두고 필요할 때 재사용함으로써 더 빠르게 연결할 수 있다.

### Connection pool
- 커넥션 풀은 일정량의 Connection객체를 미리 만들어서 pool에 저장한다.
- 요청이 오면 Connection 객체를 빌려주고 해당 객체가 반납하면 다시 pool에 저장하는 프로그래밍 기법이다.

> **HikariCP**는 스프링 2.0 부터 기본 데이터 소로 채택하고 있으며, JDBC 풀 라이브러리중 하나이다.    
> 디비 커넥션 관리를 편리하게 도와준다!