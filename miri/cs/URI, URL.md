## URI

### URI(통합자원식별자) 란?

```
인터넷에 존재하는 자원(각종 정보) 들의 이름이나 위치를 표시하는 식별자
```

- Uniform Resource Identifier

- 자원의 위치나 이름 등을 나타내기 위해 사용되는 문자열 구조

- URI의 하위개념인 URL과 URN 두 가지를 포함하는 개념이다

### URL 이란?

- Uniform Resource Locator

- 자원의 위치를 나타내는 웹 주소

- 인터넷 상의 자원이 위치하는 위치, 그리고 그 자원에 접근하기 위해 사용하는 방법등에 대한 정보를 표현한다

- `scheme://host:port/path?query#fragment`
  의 구조를 가진다

  > 기본적으로 위의 구조를 따르지만, 필요에 따라 생략되는 표현들도 있다
  >
  > - 기본 포트번호 (http 80, https 443)
  > - http또는 https (웹브라우저에서 자동으로 추가하는 경우)
  > - Path, Query, Fragment (웹 페이지에 따라 필요하지 않은 경우)

### URN 이란?

- Uniform Resource Name

- URI의 또다른 하나의 형태로, 자원의 위치나 접근 방법에 상관없이 리소스를 식별하는 이름을 나타낸다

- 시간이 지나도 변하지 않는 안정적인 리소스 식별자이지만, 현재는 많이 사용되지 않는다

---

**URI는 URL URN을 포함하는 개념이고, 현재 URN보다는 URL을 더 자주 사용한다**
