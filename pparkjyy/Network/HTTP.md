# HTTP

<br>

## HTTP (Hyper Text Transfer Protocol)

- 인터넷에서 데이터를 주고받을 수 있도록 하는 프로토콜
    - HTML, text, json, xml 등의 데이터를 주고 받음
- **비연결성**(Connectionless) 프로토콜임
    - 클라이언트가 요청을 서버에 보내고 서버가 적절한 응답을 클라이언트에 보내면 바로 연결이 끊어진다.
- **무상태**(Stateless) +  프로토콜임
    - 연결을 끊는 순간 클라이언트와 서버의 통신은 끝나며 상태 정보를 유지하지 않는다.
- TCP/IP 기반, 80포트

<br>

## HTTP 메시지 구조

![image](https://user-images.githubusercontent.com/92436863/229435216-07c3af4f-f7f9-482c-b1b0-f15f849a02c4.png)


### Start Line 
```
GET /search HTTP/1.1
```
- 요청 HTTP는 아래와 같이 세 부분으로 나누어짐
    1. `HTTP Method`
    2. `Request target`
    3. `HTTP version`

```
HTTP/1.1 404 Not Found
```
- 응답 HTTP는 아래와 같이 세 부분으로 나누어짐
    1. `HTTP version`
    2. `Status Code`
    3. `Status Text`

### Headers

- request에 대한 추가 정보를 담고 있는 부분
- key - value 형태로 저장됨
- 세 부분으로 나뉜다(general headers, request headers, entity headers)
    - `Host` : 요청하려는 서버 호스트 이름과 포트번호
    - `User-agent` : 클라이언트 프로그램 정보. 이 정보를 통해 서버는 클라이언트 프로그램(브라우저)에 맞는 최적의 데이터를 보내줄 수 있다.
    - `Referer` : 바로 직전에 머물렀던 웹 링크 주소
    - `Accept` : 클라이언트가 처리 가능한 미디어 타입 종류 나열
    - `If-Modified-Since` : 여기에 쓰여진 시간 이후로 변경된 리소스 취득. 페이지가 수정되었으면 최신 페이지로 교체한다.
    - `Authorization` : 인증 토큰을 서버로 보낼 때 쓰이는 Header
    - `Origin` : 서버로 Post 요청을 보낼 때 요청이 어느 주소에 시작되었는지 나타내는 값. 이 값으로 요청을 보낸 주소와 받는 주소가 다르면 CORS(Cross-Origin Resource Sharing) 에러가 발생한다.
    - `Cookie` : 쿠키 값이 key-value로 표현된다.

### Body

- http의 실제 데이터 정보
- GET 요청과 같은 경우 생략 가능

<br>


## HTTP Method

- http 요청의 목적이나 종류를 나타내는 수단임
- 총 9개의 메소드가 존재한다
    - 5개의 주요메소드와 4개의 기타 메소드
- 일부 메소드는 **안정성**(Safe)를 가진다
    - 데이터를 아예 변경하지 않을 때
- 일부 메소드는 **멱등성**(Idempotent)을 가진다
    - 여러번 요청한 결과와 한번 요청한 결과의 데이터 상태가 같을 때
- 일부 메소드는 **캐시가능** 특징을 가진다.
    - GET과 HEAD 메소드에서 자주 캐싱이 사용됨

![image](https://user-images.githubusercontent.com/71180414/150720932-5f2a71ae-1d31-4f3a-9518-42dfc0037240.png)

### POST

- 데이터 생성 (Create)

### PUT

- 데이터를 교체 및 생성 (덮어씌우기)
- POST와 차이점
    - 여러번 요청했을 때 POST는 데이터를 계속 생성하지만, PUT은 한번 생성 후 계속 교체함
    - 즉 PUT은 멱등성을 가진다.

### GET

- 데이터 조회 (Read)

### PATCH

- 데이터 수정 (Update)
- 데이터를 부분 수정할 때 사용됨
- PUT과 차이점
    - PUT은 문서 자체의 교체만을 허용하며, 일부만 전달할 경우 전달한 필드외 모드 null이나 초기값으로 처리된다

### DELETE

- 데이터 삭제 (Delete)

### HEAD

- GET과 유사한 방식이지만 응답메시지에 헤더 정보만 보냄
- 웹 서버의 다운 여부 점검이나 웹 서버 정보(버전 등)등을 얻기 위해 사용됨

### TRACE

- 요청이 서버에 도달했을 때 어떻게 보이게 되는지 알려줌
- 디버깅용으로 사용됨

### OPTIONS

- 서버에게 여러 종류의 지원 범위를 물어봄
    - 특정 리소스에 대한 지원되는 메소드 정보
- 응답메시지 헤더에 Allow 필드를 포함하여 응답

### CONNECT

- 요청된 리소스와 양방향 통신을 시작

<br>

## Status Code

### 1xx (Informational)

- 요청을 받고 처리중인 상태
- 거의 사용하지 않음

### 2xx (Successful)

- 요청이 정상 처리된 상태
- `200` OK : 요청 처리 성공
- `201` Created : 요청 성공해서 새로운 리소스가 생성됨
- `202` Accepted : 요청이 접수되었으나 처리가 완료되지 않았음
- `204` No Content : 서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음

### 3xx (Redirection)

- 리다이렉션을 수행해야하는 상태
- location 헤더가 있다면 해당 location 위치로 이동하도록 만듬

### 4xx (Client Error)

- 클라이언트 오류
- `400` Bad Request : 클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음
- `401` Unauthorized : 클라이언트가 해당 리소스에 대한 인증이 필요함
- `403` Forbidden : 서버가 요청을 이해했지만 승인을 거부함
- `404` Not Found : 요청 리소스를 찾을 수 없음
- `405` Method Not Allowed : 요청 메소드가 금지되었음

### 5xx (Server Error)
 
- 서버 오류
- `500` Internal Server Error : 서버 문제로 오류 발생, 애매하면 500 오류
- `502` Bad Gateway : 게이트웨이에서 문제 발생 (nginx에서 자주 보임)
- `503` Service Unavailable : 서비스 이용 불가상태 (유지보수를 위한 중단 or 과부하)

<br>

