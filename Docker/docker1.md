# 도커를 사용하는 이유?

- 결론적으로 어떠한 프로그램을 다운 받는 과정을 굉장히 간단하게 만들기 위해서입니다.
<hr/>

### 도커 없이 프로그램 받을때 원래 프로그램을 다운받고 실행하는 순서
1. installer 다운
2. installer 실행
3. 프로그램 설치 완료

- 갖고 있는 서버, 패키지 버전, 운영체제 등에 따라 프로그램을 설치하는 과정중에 많은 에러들이 발생하게 됩니다.
- 그것만이 아니라 설치 과정이 다소 복잡합니다...

<hr/>
 
### 도커 없이 Redis 받는 과정
 
```java
 $ wget http://download.redis.io/releases/redis-6.0.4.tar.gz
 $ tar xzf redis-6.0.5.tar.gz
 $ cd redis-6.0.5
 $ make
```

<hr/>

### 도커 사용 Redis 받는 과정

```java
docker run -it redis
```
 

