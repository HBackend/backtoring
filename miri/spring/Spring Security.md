## Spring Security

```
Spring 기반 에플리케이션의 `인증`, `권한`, `인가` 등을 담당하는 Spring 프레임워크
```

spring 프로젝트에서 회원 로그인/로그아웃과 같은 기능을  
보다 편리하게 개발할 수 있도록 spring에서 제공하는 하위 프레임워크

- 보안과 관련된 체계적인 로직들을 프레임워크에서 제공
- 개발자가 하나하나 직접 보안 관련 로직을 작성하지 않아도 됨

```
spring security에서는 Principal과 그에 따른 Credential를 주체로 하여 인증을 진행하고, 인가 절차를 통해 권한을 확인함
-> 시스템에서 사용자를 식별하고 해당 사용자에 대한 권한을 확인 및 부여할 수 있도록 하는 과정
```

### Spring Security 핵심 용어

#### (1)Principal

보호된 Resource에 접근하는 유저

#### (2)Credential

Resource에 접근하는 유저의 비밀번호

#### (3)Authentication(인증)

해당 사용자가 본인인지 확인하는 절차

#### (4)Authorization(인가)

인증된 사용자가 요청한 자원에 접근 가능한지 결정하는 절차

#### (5)권한

인증된 주체가 애플리케이션의 리소스를 이용할 수 있는지를 결정하는 요소

#### (6)SecurityContext

현재 사용자의 인증 정보를 저장하는 곳

#### Spring Security에서는 `AuthenticationFilter`, `AuthenticationManager`, `AuthenticationProvider` 3가지 요소를 거치는 과정을 통해 인증 절차를 처리한다

### AuthenticationFilter

- 클라이언트에서 온 인증 요청을 Spring Security에게 전달하는 역할
- 인증이 완료된 이후 _Authentication_ 객체를 SecurityContext에 저장하는 역할

### AuthenticationManager

- 여러 개의 AuthenticationProvider를 관리하며, 인증을 수행시키는 주체

### AuthenticationProvider

- AuthenticationProvider는 특정한 인증 유형을 처리하고 사용자를 인증하는 역할
- 인증용 객체의 정보를 바탕으로 다양한 데이터 소스를 처리할 수 있는 여러 인증방식들중 적합한 것(들)이 선택됨
- 인증에 성공했을 경우, 남은 AuthenticationProvider를 통한 인증 과정은 더 이상 실행하지 않음

---

### Spring Security 전체 동작 원리

![spring security](https://cdn.discordapp.com/attachments/1083644292117045341/1186015044518035496/2023-12-18_3.40.13.png?ex=6591b595&is=657f4095&hm=f3a24c6dcbae9e89d2aabc6b9cb69bf56c3f39ae10ddf03281516427b17ec442&)

> 이미지의 번호와 아래 설명의 번호는 무관

1. 사용자가 username, password등의 로그인 정보를 HTTP body로 전달과 함께 인증을 요청

2. `AuthenticationFilter`가 요청을 가로채고, 가로챈 정보를 통해 인증용 객체인 **_UsernamePasswordAuthenticationToken_**를 생성

3. `AuthenticationManager`의 구현체인 **ProviderManager**에게 생성한 **_UsernamePasswordAuthenticationToken(인증용 객체)_** 객체를 전달

4. **ProviderManager**는 전달받은 인증용 객체를 바탕으로 등록된 여러 `AuthenticationManager`들 중 적절한 것(들)을 선택

5. 선택된 `AuthenticationProvider`가 실행이 되면 전달받은 인증용 객체를 **UserDetailsService**에 넘겨줌

6. **UserDetailsService** 에서는 넘겨받은 인증용 객체의 principal을 통해 DB에서 찾은 Credential등을 포함한 사용자 정보인 **_UserDetails_** 객체를 만들음

7. 생성된 **_UserDetails_** 객체와 넘겨받은 **_인증용 객체_**의 정보를 비교

   > 이때, database에서 가져온 UserDetails의 Credential정보는 암호화가 되어있는 상태  
   > 따라서 인증용 객체의 Credential 정보와 비교를 할 때에는 PasswordEncoder를 사용하여 안전하게 둘을 비교하는 과정을 거침

8. 인증이 완료되면 권한 등의 사용자 정보를 담은 **_Authentication_** 객체를 반환

9. `AuthenticationFilter`는 SecurityContextHolder를 통해 반환받은 **_Authentication_** 객체를 SecurityContext에 저장

### UserDetailsService 구현

```java
@Service
@RequiredArgsConstructor
public class UserDetailsServiceImpl implements UserDetailsService {

    private final UserRepository userRepository;

    // 사용자명을 이용하여 UserRepository에서 사용자 정보를 조회하고 비교하는 메서드 실행
    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = userRepository.findByUsername(username)
                .orElseThrow(() -> new UsernameNotFoundException(ErrorType.NOT_FOUND_USER.getMessage())); // 사용자명과 일치하는 정보가 DB에 없으면 예외처리

        // UserDetailsImpl 클래스를 이용하여 Spring Security에서 사용할 UserDetails 객체 생성
        return new UserDetailsImpl(user, user.getUsername()); // 사용자 정보를 UserDetails로 반환
    }
}

```

### UserDetails 구현

```java
public class UserDetailsImpl implements UserDetails {
    // 사용자의 인증과 권한 부여를 위한 정보를 포함하는 객체

    private final User user; // 실제 사용자 정보를 담은 User(entity) 객체
    private final String username; // 사용자명 (Principal)

    public UserDetailsImpl(User user, String username) {
        this.user = user;
        this.username = username;
    }

    public User getUser() {
        return user;
    }

    // 권한 정보를 Spring Security가 사용하는 GrantedAuthority 형태로 변환하여 반환하는 메서드

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        UserRoleEnum role = user.getRole(); // 사용자의 권한을 나타내는 Enum 값 가져오기
        String authority = role.getAuthority(); // Enum 값을 문자열로 변환하여 권한 문자열 생성

        SimpleGrantedAuthority simpleGrantedAuthority = new SimpleGrantedAuthority(authority);
        Collection<GrantedAuthority> authorities = new ArrayList<>();
        authorities.add(simpleGrantedAuthority);

        return authorities; // GrantedAuthority 형태로 추상화된 사용자 권한 반환
    }

    @Override
    public String getPassword() {
        return user.getPassword(); // 사용자의 비밀번호 반환
    }

    @Override
    public String getUsername() {
        return this.username; // 사용자명 반환
    }

    // 사용자 계정의 유효기간 만료X, 잠김X, 자격증명의 유효기간 만료X, 활성상태를 항상 true로 반환
    @Override
    public boolean isAccountNonExpired() {
        return true;
    }

    @Override
    public boolean isAccountNonLocked() {
        return true;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        return true;
    }

    @Override
    public boolean isEnabled() {
        return true;
    }
}
```

---

### JWT와 접목

Spring Security의 인증 및 권한 부여를 효과적으로 구현하기 위한 방법 중 하나로, JWT를 함께 접목하여 이용하는 방법

#### JWT란?

JSON 방식으로 정보를 전달하는 토큰

- 웹서비스의 로그인 인증 시스템에서 주로 사용된다
- 암호화된 문자열의 형태이다

#### JWT의 특징

- stateful 해야한다는 세션의 단점을 보완할 수 있다
- 별도의 세션 저장소를 강제하지 않기때문에 stateless하여 확장성이 뛰어나다
- signature를 통해 보안성을 갖추고있다

#### JWT의 구조

`Header 헤더`
토큰의 타입과 사용하는 암호화 알고리즘 정보가 들어있다

`Payload 페이로드`
실제로 전달할 내용이(예: 사용자 ID) 들어있다

- key-value (json) 형태로 저장된다
- 사용자, 토큰에 대한 property를 저장한다

`Signature 서명`
헤더와 페이로드를 디코딩 한 값을 합친 다음, 개인 키를 사용하여 암호화 되어있다.  
-> 이를 통해(your-256-bit-secret, 서버가 가지고있는 개인 키)JWT가 변조되지 않았는지 확인할 수 있다

#### Signature을 복호화 하여 사용자 인증을 하는 과정

클라이언트에서 서버로 요청을 보내고, jwt 토큰을 동시에 전달한다
서버의 개인 키를 사용해 signature을 복호화 하게 된다. 이때 signature를 복호화 하여 알 수 있는 헤더와 페이로드의 값이 jwt의 헤더와 페이로드의 값과 일치한다면 인증을 허용한다
서버의 개인키로만 암호화 할 수 있으므로, 따라서 다른 클라이언트에선 복호화가 불가능하다  
**_-> 보안성을 갖춤_**

#### 간단한 구현 방법

- Spring Security와 JWT를 통한 인증, 권한 확인을 위한 필터, 구성을 추가로 사용하여 웹 애플리케이션의 보안을 구성
- JWT를 생성하고 검증하기 위한 유틸리티 클래스나 서비스를 구현
  > ex) JwtTokenProvider

#### 동작 원리

1. 사용자가 로그인할 때, JWT 토큰을 생성하고 클라이언트에게 전달
   > 로그인(인증) 성공 시, JwtTokenProvider를 사용하여 토큰을 생성하고 http response에 추가
2. 클라이언트는 인증이 필요한 요청을 할 때마다 발급받은 JWT 토큰을 http request 헤더에 포함시켜 전송
   > ex) Authorization: Bearer [토큰]
3. 서버는 클라이언트로부터 받은 JWT 토큰을 검증하고, 유효하다면 해당 토큰에서 사용자 정보를 추출하여 Spring Security의 Authentication 객체로 생성하여 사용

**_JWT의 만료 시간과 access token, refresh token을 적절히 설정하여 보안을 강화시키는 것이 중요_**

---

### OAuth와의 접목

OAuth를 Spring Security에 접목하는 것
즉, 외부 서비스에서 제공하는 사용자 인증을 어플리케이션에 효과적으로 통합할 수 있게 하는 방법

#### 동작 원리

1. 사용자의 로그인 요청을 받은 서버는 OAuth provider에게 사용자 로그인 요청

2. OAuth provider는 사용자를 로그인 페이지로 리다이렉션하고, 직접 로그인하는 과정을 거친 후 인가 코드(Authorization Code)를 발급하고, 이를 서버에 전달
3. Authorization Code를 받은 서버는, 이를 통해 OAuth provider에게 Access Token을 요청

4. 서버는 발급받은 Access Token을 사용하여 사용자 정보를 요청하고, OAuth provider의 검증 이후 사용자의 정보를 받음

5. 발급받은 사용자 정보를 기반으로 서버에서 UserDetails 객체를 생성한 후 Authentication객체를 생성하여 SecurityContext에 저장
   (spring security의 동작원리를 따름)

위와 같은 과정을 통해 Spring Security는 사용자의 권한 및 인증 상태를 확인하여 리소스에 대한 접근을 관리함

**_OAuth 인증을 통해 사용자의 정보를 반환받아 UserDetails 객체를 생성하는 과정이 가장 큰 차이이자 특징_**
