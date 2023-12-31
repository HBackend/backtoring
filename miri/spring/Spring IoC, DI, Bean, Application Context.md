### Spring IoC, DI, Bean, ApplicationContext

> Spring 프레임워크에서 애플리케이션의 객체 관리와 관련된 핵심적인 개념

### Spring IoC 란?

Inversion of Control, 즉 제어의 역전이란 프로그램의 실행방식에 있어서 흐름을 제어하는 주체를 외부에 두어 관리시키는 것

**이러한 IoC 기술을 Spring이라는 프레임워크에 적용**하여 개발자가 직접 객체를 생성, 초기화, 연결 및 관리하는 대신에 프레임워크가 그 역할을 하게 하고,  
이를 통해 유연성이 높은 코드를 작성할 수 있게 한다

> 이때 알 수 있는 프레임워크와 라이브러리와의 차이점은 "제어의 흐름"에 있는데  
>  라이브러리는 개발자가 필요에 의해 선택적으로 가져와서 사용하고 제어하는 반면, IoC를 적용한 프레임워크는 프레임워크의 내부에서(개발자가 아닌 외부 컨테이너를 뜻함) 전체적인 실행 흐름을 제어하며 개발자는 프레임워크에 따라 특정 부분에만 코드를 작성하게 된다

> 다시 말해, 라이브러리는 개발자가 코드에 직접 사용하지만, 프레임워크에서는 개발자의 코드가 **프레임워크에 의해 사용된다**는 차이가 있다고 할 수 있다

Spring에서는 `ApplicationContext`라는 IoC 컨테이너의 기능을 확장시킨 인터페이스를 제공하며  
이를 통해 `Bean`의 생성 및 관리, 의존성주입(`DI`)등을 관리한다

### ApplicationContext 란?

Spring 애플리케이션의 **핵심적인 런타임 환경을 제공**하는 중심적인 역할을 하는 프레임워크의 핵심 인터페이스

Spring IoC 컨테이너인 빈 팩토리(Bean Factory)를 확장하여 빈 생성및 관리 외의 기능들을 사용할 수 있게 한다

### DI 란?

Dependency Injection, 객체간의 의존성을 개발자가 직접 명시하거나 초기화하는 대신, 컨테이너에 의한 의존성주입 방식을 말한다

`생성자 주입`, `필드 주입`, `Setter 주입` 등의 방식으로 구현될 수 있는데
Spring에서는 **_생성자주입 방식_**을 가장 권장한다

```java
@Service
public class Service {

    private final Repository repository;

    @Autowired
    public Service(Repository repository) {
        this.repository = repository;
    }
}
```

> 생성자를 통해 의존 관계를 주입하는 방법이다

- 빈 생성시 필수적으로 1회 호출되고, 이후에 더이상 변경되는일이 없기 때문에 안정성을 보장할 수 있어 권장된다

- 생성자가 1개만 있는 경우 `@Autowired` 어노테이션이 생략 가능하다

### Bean 이란?

스프링 컨테이너(즉 ApplicationContext) 에 의해 생성, 관리되는 인스턴스화 된 객체  
주로 `@Component`, `@Service`, `@Repository`, `@Controller`와 같은 어노테이션을 통한 컴포넌트 스캔 방식으로 주로 빈이 생성되지만
xml 설정파일에서 직접 클래스를 빈으로 등록하고 의존성을 주입하는 방식, 또는 Java Config 파일에서 Java 코드로 빈 설정을 직접 하는 방법도 있다

그리고 이렇게 생성된 빈은 필요한경우 **컨테이너에 의해 의존성 주입**을 받는다

> 인스턴스화 된 객체를 말하지만, new 연산자등을 통해 생성된 객체 등 스프링 애플리케이션에서 생성되는 모든 객체가 빈인것은 아니다

#### Bean의 라이프사이클

`스프링 IoC 컨테이너 생성` → `스프링 빈 생성` → `의존관계 주입` → `초기화 콜백 메소드 호출` → `사용` → `소멸 전 콜백 메소드 호출` → `종료`

이 과정에서 빈들은 Bean Scope에 의해 관리되며, 각 scope에 따라 IoC 컨테이너가 관리하는 빈의 생명 주기와 범위가 다르다

`싱글톤 스코프` 디폴트 타입  
빈의 생성부터 종료까지 컨테이너가 관리하는 가장 넓은 범위의 스코프

`프로토타입 스코프`  
컨테이너가 빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않는 짧은 범위의 스코프

`request 스코프`  
http 요청을 받았을때부터 응답을 반환할때 까지 컨테이너가 관리하는 스코프

#### 콜백 메소드란?

Bean 생성시 초기화를 필요로 하는 경우나, Bean의 소멸 전 리소스 제거 등의 작업을 위해 호출되는 메서드이다

#### 빈 스코프에서 생길수 있는 문제?

생성 시점에 한번만 초기화되는 싱글톤 스코프 빈 안에, 매번 새로 생성되어 초기화되는 프로토타입 스코프 빈을 혼용하여 함께 사용할 경우 의도치 않게 동작하는 문제가 생길 수 있다

> 싱글톤 빈은 생성 시점에 한번만 초기화되기 때문에, 그 안의 프로토타입 빈도 한 번만 생성되고 매번 새로 생성되지 않게된다

이러한 문제점을 해결하기 위해서는 싱글톤 빈에서 `@Lookup` 어노테이션을 통해 **프로토타입 빈을 매번 새로 호출해서 사용**하는 방법이 있다

추상메서드를 선언한 싱글톤 빈 메서드에서 해당 어노테이션을 사용하면, 메서드 호출시 매번 새로운 프로토타입의 빈을 반환한다  
따라서 이 방법을 통해 두 스코프의 동시 사용시 생기는 문제점을 해결할 수 있어진다
