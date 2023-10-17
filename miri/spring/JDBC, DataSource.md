## JDBC란?

자바 언어를 통해 데이터베이스와 연결하고, 데이터베이스 내의 데이터와 상호 작용하기 위한 자바의 API

JDBC가 SQL 쿼리를 직접 작성하여 데이터베이스와의 연동을 처리해주기 때문에, 개발자는 이를 쉽게 사용하여 개발의 효율을 높일 수 있다

#### JDBC 드라이버

특정 데이터베이스환경에 접근할 수 있도록 JDBC 인터페이스를 구현해둔 라이브러리를 말한다  
개발자들은 제공되는 JDBC 드라이버를 통해 JDBC를 활용한 개발을 할 수 있다

> 이때 `DriverManager`는 애플리케이션 코드에서 제공된 코드(문자열)와 같은 정보들을 기반으로 적절한 드라이버를 선택하고,  
> 드라이버들과의 연결을 수행하며 관리한다

---

## DataSource란?

**데이터베이스에 연결을 해주고 관리해주는 추상화된 객체**

데이터베이스와 관계된 연결정보를 담아 애플리케이션에 빠르게 연결을 제공한다

### **_커넥션풀링_**

DataSource는 주로 `커넥션 풀링`을 위한 작동을 제공한다

커넥션풀이란?  
데이터베이스와 연결되는 객체를 미리 저장해두는 `pool`이라는 공간

#### 커넥션풀링이란?

> 데이터베이스와 연결된 객체들을 미리 연결해두어 `pool`에 저장해두었다가
> 요청이 와 커넥션이 필요한 경우에 그것을 빌려주고 사용을 마친후 다시 `pool`에 저장하는 방식으로 동작하게 하는 것

**미리** 생성된 연결을 재사용하므로, 연결 및 연결종료에 따른 오버헤드를 줄일 수 있고
데이터베이스에 접근할때 성능을 향상시킨다

> SpringBoot에서는 커넥션 풀 관리를 위해 HikariCP를 사용하고, 이를 통해 커넥션풀링의 성능을 최적화할 수 있다

---

Connection, Statement, ResultSet 란?

> JDBC의 동작과 관련된 클래스(인터페이스)들로, 해당 클래스들을 이용해 sql문으로 DB에 접근하는 로직을 짤 수 있다  
> 하지만 sql문을 코드에 직접 작성하는경우 초래되는 보안적인 문제, 유지보수성의 저하 등으로 최근에는 잘 사용되지 않는다

`Connection` DB와 연결성을 갖는 클래스  
`Statement` SQL문을 실행하는 클래스  
`ResultSet` 조회된 결과를 갖는 클래스