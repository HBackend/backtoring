# Spring IoC, DI, Bean, Application Context	

## Spring DI
> Dependency Injection

- DI는 스프링이 지원하는 의존 관계 주입 기능이다.
- 객체를 직접 생성(new 키워드)하는 것이 아니라 외부(IOC컨테이너)에서 생성한 후 주입 시켜주는 방법이다.
- DI로 모듈간의 결합도를 낮출 수 있다.
- 주입 방법으로는 필드주입, 생성자 주입, setter 주입이 있다.

```java
public class Person() {
    @Autowired
    private Student s;
}
```

- 스프링에선 이렇게 주입당하는 객체를 빈이라고 부르며, 빈 객체를 등록하면 스프링 컨테이너에서 빈의 생성부터 소멸까지의 과정을 모두 관리한다.

## Spring Bean
- 스프링 컨테이너가 관리하는 객체를 빈 이라고 한다.

### 스프링 빈 라이프사이클
1. 스프링 IoC 컨테이너 생성
   - 가장 처음에는 컨테이너가 생성되는 과정이 일어난다.
2. 스프링 빈 생성
   - 스프링에서 컴포넌트 스캔으로 Bean들을 스프링 컨테이너안에 등록시킨다.
3. 의존관계 주입
   - IoC 컨테이너에서 클래스의 의존관계를 보고 의존성을 주입해준다.
4. 초기화 콜백 실행
   - 콜백 메서드 : 특정 이벤트가 실행되고 실행되는 메서드
   - 인터페이스, 설정 정보에 추가, @PostConstrucy, @PreDestroy 로 빈 생명주기 콜백을 관리한다.
   - ```java
     public class ExampleBean {
     @PostConstruct
         public void init()  {
             // 초기화 콜백
         }
    
     @PreDestroy
         public void close() t {
             // 소멸 전 콜백
         }
     }
     ```
5. 사용
6. 소멸 전 콜백 실행
7. 종료

### 빈 스코프
- 빈이 관리되는 범위이다.

#### Singleton
- 스프링 애플리케이션이 구동 될때 한번에 ApplicationContext에서 모두 생성하여 하나의 클래스는 하나의 빈만 가진다.
- 기본적으로 빈을 등록하면 싱글톤 패턴으로 관리해준다.
- 가장 넓은 범위를 가진 스코프이다.

#### Request
- HTTP 요청이 들어오고 나갈때 유지되는 범위이다.
- 각각의 요청마다 빈 인스턴스가 생성되고 관리된다.


#### Prototype
- 매번 새로운 빈을 정의해서 사용한다.
- 스프링 컨테이너가 생성과, 의존관계 주입, 초기화 (콜백 실행) 까지만 관여하고 이후의 과정은 관여하지 않는다.

> 스코프 등록 방법
```java
@Scope("singleton")
@Component
public class ILoveBean {}
```

### 빈 등록 방법

`@Configuration`

- 클래스에 붙이는 어노테이션
- @Bean을 사용할 때 함께 사용해 주어야 한다.

`@Bean`

- 메소드에 붙이는 어노테이션
- 메소드에서 반환되는 객체를 스프링 빈에 등록한다.

`@Service / @Repository`

- 개발자가 직접만든 클래스를 빈으로 등록할 때 사용

`@Configuration / @Bean`

- 외부 라이브러리, 프레임워크에서 만든 클래스를 등록할 때 주로 사용한다.

`@Component`

- 주어진 클래스를 컴포넌트로 간주한다.
- 이 클래스들은 스프링 서버가 뜰 때 자동으로 감지된다. 스프링 빈이 됨
- 컨트롤러 서비스 리포지토리가 모두 아니고 개발자가 직접 작성한 클래스를 스프링 빈으로 등록할 때 사용하기도 한다.

## Spring IoC
> Inversion of Control

- 제어의 역전이라는 의미로 객체의 호출 작업을 개발자가 아니라, 스프링에서 결정하는 것이다 (제어권이 바뀌어진다).
- 객체의 생성부터 생명주기에 대한 모든 제어의 권한이 바뀌었다는 것이다.

```java
public interface BookRepository {
    void saveBook();
}
```
- 예시로 이렇게 BookRepository 인터페이스가 있다.

```java
@Service
public class BookService {

    private final BookRepository bookRepository;

    public BookService(BookRepository bookRepository) {
        this.bookRepository = bookRepository;
    }

    public void saveBook() {
        bookRepository.saveBook();
    }
}
```
- 이렇게 bookRepository 를 DI 한다.

```java
@Repository
public class BookMemoryRepository implements BookRepository {

    @Override
    public void saveBook() {
        System.out.println("BookMemoryRepository");
    }

}
```

```java
@Primary
@Repository
public class BookMysqlRepository implements BookRepository {
    @Override
    public void saveBook() {
        System.out.println("BookMysqlRepository");
    }
}
```

- 이렇게 두개의 구현체가 있으면, 컨테이너가 BookMysqlRepository 또는 BookMysqlRepository 를 선택하여 BookService에 만들어 준다.


## ApplicationContext

- BeanFactory 는 스프링 컨테이너의 최상위 인터페이스 이며 스프링 빈을 관리하고 조회하는 역할을 수행한다. ApplicationContext는 BeanFactory의 하위 인터페이스로 여러 기능이 추가 되어있는 인터페이스 이다.
- BeanFactory를 직접 사용하는 경우는 거의 없고 ApplicationContext를 사용하기 때문에 ApplicationContext를 스프링 컨테이너라 한다.