# URI, URL

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


>예를 들어 다음과 같은 홈페이지 링크가 있을 때   
`https://www.github.com/index.html?page=2&id=100&search=abc`
- URL은 index.html의 위치를 표시한 `https://www.github.com/index.html` 까지 이다.
- 하지만 원하는 리소스에 도착 하려면 `?page=2&id=100&search=abc` 라는 식별자가 필요하다.
- `https://www.github.com/index.html?page=2&id=100&search=abc` -> URI
- `https://www.github.com/index.html` -> URL

## URN (Uniform Resource Name)
- 리소스의 위치와 상관없이 유일하게 해당 리소스를 식별하는 이름 역할을 한다.
- URN 은 아직 널리 채택되어 사용되지는 않는다.