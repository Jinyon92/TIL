# 세션(Session)란 무엇인가?

- 클라이언트 별로 서버에 저장되는 정보입니다.

__1. 이용방법__
- 웹 클라이언트가 서버측에 요청을 보내게 되면 서버는 클라이언트를 식별하는 session id를 생성합니다.
- 서버는 session id를 이용해서 key와 value를 이용한 저장소인 HttpSession을 생성합니다.
- 서버는 session id를 저장하고 있는 쿠키를 생성하여 클라이언트에 전송합니다.
- 클라이언트는 서버측에 요청을 보낼때 session id를 가지고 있는 쿠키를 전송합니다.
- 서버는 쿠키에 있는 session id를 이용해서 그 전 요청에서 생성한 HttpSession을 찾고 사용합니다.

__2. 세션 생성 및 얻기__
```java
HttpSession session = request.getSession();
HttpSession session = request.getSession(true);
```
- request의 getSession()메소드는 서버에 생성된 세션이 있다면 세션을 반환하고 없다면 새롭게 세션을 생성하여 반환합니다.
- 새롭게 생성된 세션인지는 HttpSession이 가지고 있는 isNew()메소드를 통해 알 수 있습니다.
```java
HttpSession session = request.getSession(false);
```
- request의 getSession()메소드에 파라미터로 false를 전달하면, 이미 생성된 세션이 있다면 반환하고 없으면 null을 반환합니다.

__3. 세션의 값 저장__
```java
setAttribute(String name, Object value);
session.setAttribute(이름, 값);
```
- name과 value의 쌍으로 객체 Object를 저장하는 메소드입니다.
- 세션이 유지되는 동안 저장할 자료를 저장합니다.

__4. 세션의 값 조회__
- 세션에 저장된 자료는 다시 getAttribute(String name) 메소드를 이용해 조회합니다.
- 반환 값은 Object 유형이므로 저장된 객체로 자료유형 변환이 필요합니다.
- 메소드 setAttribute()에 이용한 name인 “id”를 알고 있다면 바로 다음과 같이 바로 조회합니다.
```java
String value = (String) session.getAttribute("id");
```

__5. 세션의 값 삭제__
+ removeAttribute(String name) 메소드
  - name값에 해당하는 세션 정보를 삭제합니다.
+ invalidate() 메소드
  - 모든 세션 정보를 삭제합니다.

__6. javax.servlet.http.HttpSession__
+ 세션은 클라이언트가 서버에 접속하는 순간 생성
  - 특별히 지정하지 않으면 세션의 유지 시간은 기본 값으로 30분 설정합니다.
  - 세션의 유지 시간이란 서버에 접속한 후 서버에 요청을 하지 않는 최대 시간입니다.
  - 30분 이상 서버에 전혀 반응을 보이지 않으면 세션이 자동으로 끊어집니다.
  - 이 세션 유지 시간은 web.xml파일에서 설정 가능합니다.
```java
<session-config>
  <session-timeout>30</session-timeout>
</session-config>
```
