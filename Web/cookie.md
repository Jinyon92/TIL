# 쿠키(Cookie)란 무엇인가?

- 클라이언트 단에 저장되는 작은 정보의 단위입니다.
- 클라이언트에서 생성하고 저장될 수 있고, 서버 단에서 전송한 쿠키가 클라이언트에 저장될 수 있습니다.

### 쿠키(Cookie)특징
- 사용자 컴퓨터에 저장
- 저장된 정보를 다른 사람 또는 시스템이 볼 수 있는 단점
- 유효시간이 지나면 사라짐

__1. 이용방법__
- 서버에서 클라이언트의 브라우저로 전송되어 사용자의 컴퓨터에 저장합니다.
- 저장된 쿠키는 다시 해당하는 웹 페이지에 접속할 때, 브라우저에서 서버로 쿠키를 전송합니다.
- 쿠키는 이름(name)과 값(value) 쌍으로 정보를 저장합니다.
- 이름-값 쌍 외에도 도메인(Domain), 경로(Path), 유효기간(Max-Age, Expires), 보안(Secure), HttpOnly 속성을 저장할 수 있습니다.

__2. 쿠키는 그 수와 크기에 제한__
- 브라우저별로 제한 값을 다르게 가져가고 있습니다. 
- 참고 : http://browsercookielimits.squawky.net/

__3. javax.servlet.http.Cookie__
- 서버에서 쿠키 생성, Response의 addCookie메소드를 이용해 클라이언트에게 전송
- 쿠키는 (이름, 값)의 쌍 정보를 입력하여 생성합니다.
- 쿠키의 이름은 일반적으로 알파벳과 숫자, 언더바로 구성합니다. 정확한 정의를 알고 싶다면 RFC 6265(https://tools.ietf.org/html/rfc6265) 문서 [4.1.1 Syntax] 항목을 참조하세요.
```java
Cookie cookie = new Cookie(이름, 값);
response.addCookie(cookie);
```

__4. 클라이언트에게 쿠키 삭제 요청__
- 쿠키를 삭제하는 명령은 없고, maxAge가 0인 같은 이름의 쿠키를 전송합니다.
```java
Cookie cookie = new Cookie("이름", null);
cookie.setMaxAge(0);
response.addCookie(cookie);
```

__5. 쿠키의 유효기간 설정__
+ 메소드 setMaxAge()
  - 인자는 유효기간을 나타내는 초 단위의 정수형
  - 만일 유효기간을 0으로 지정하면 쿠키의 삭제
  - 음수를 지정하면 브라우저가 종료될 때 쿠키가 삭제
+ 유효기간을 10분으로 지정하려면
  - cookie.setMaxAge(10*60); //초 단위 : 10분
  - 1주일 지정하려면 (7*24*60*60)로 설정합니다.

![cookie-image](../static/web/cookie-image.png)

__6. Spring MVC에서의 Cookie 사용__
+ @CookieValue 애노테이션 사용
  - 컨트롤러 메소드의 파라미터에서 CookieValue애노테이션을 사용함으로써 원하는 쿠키정보를 파라미터 변수에 담아 사용할 수 있습니다.
+ 컨트롤러메소드(@CookieValue(value="쿠키이름", required=false, defaultValue="기본값") String 변수명)
