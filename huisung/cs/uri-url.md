# URI, URL, URN

## URI (Uniform Resource Identifier)
- 통합 자원 식별자이다. 인터넷에 있는 자원이 어디에 있는지 자원 자체를 식별하는 문자열이다.
- URI 의 하위 개념으로 URL, URN 이 있다.

```java
URL
 | -> Name -> URN
 | -> Location -> URL
```

## URL (Uniform Resource Locator)
- 네트워크 상에서 특정 자원의 위치를 구체적으로 서술하는 문자열이다.
- 애플리케이션에게 특정 자원에 접근하는 방법과 위치를 알려주는 수단이다.
- URL의 예시이다. ```https://github.com/HBackend/backtoring``` 해당 URL을 브라우저 주소창에 입력하면 연결된 자원을 불러올 수 있다.  

### URL의 구조

> ex
`https://github.com:443/HBackend/?id=100&pages=10#pullrequestreview-1651867139`

**스카마**   
- `https`
- URL의 첫 부분은 브라우저가 자원을 요청하는 데 사용해야하는 통신규약을 나타낸다. (HTTPS 프로토콜을 사용한다는 의미)

**도메인**
- `github.com`
- 도메인은 IP 주소를 갖는 서버를 사용자가 쉽게 기억하고 찾을 수 있도록 만든 서비스 이다.

**포트**
- `:443`
- 서버의 어떤 포트에 접속할지 결정한다. `:` 뒤에 나온다. 웹 서버가 HTTP 프로토콜의 표준포트를 시용할 경우 일반적으로 생략된다.

**Path**
- `/HBackend`
- 자원의 경로를 가리키며, `/` 뒤에 나온다.

**Parameter**
- `?id=100&pages=10`
- 파라미터는 쿼리 스트링이라고도 부르며, `key = value` 형식이다.
- `?` 뒤에 나열되며 `&` 기호로 구분된다.

**Anchor(Fragment)**
- `#pullrequestreview-1651867139`
- 프래그먼트, 해시태그라고도 부르며 특정 요소를 지시한다.
- 해시태그로 원하는 요소의 id를 연결하면 스크롤 이동 없이 바로 해당 위치로 이동한다.

>예를 들어 다음과 같은 홈페이지 링크가 있을 때   
`https://www.github.com/index.html?page=2&id=100&search=abc`
- URL은 index.html의 위치를 표시한 `https://www.github.com/index.html` 까지 이다.
- 하지만 원하는 리소스에 도착 하려면 `?page=2&id=100&search=abc` 라는 식별자가 필요하다.
- `https://www.github.com/index.html?page=2&id=100&search=abc` -> URI
- `https://www.github.com/index.html` -> URL

## URN (Uniform Resource Name)
- 리소스의 위치와 상관없이 유일하게 해당 리소스를 식별하는 이름 역할을 한다.
- URN 은 아직 널리 채택되어 사용되지는 않는다.