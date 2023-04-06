## RESTful API

API(Application Programming Interface)는 일종의 소프트웨어 인터페이스이며 애플리캐이션 서로 간에 연결하여 통신할 수 있는 방법을 정의하는 기능의 집합이다. 
RESTful api 는 REST(Representational State Transfer) 디자인 원칙을 준수한 API이다.

 
### REST
자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미한다.

**즉, HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원(URI)에 대한 CRUD Operation을 적용하는 것을 의미한다.**

+) CRUD Operation 은 대부분의 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리 기능인 Create(생성), Read(읽기), Update(수정), Delete(삭제)를 묶어서 일컫는 말이다.

- 자원(Resource) : HTTP URI (Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다.)
- 자원에 대한 행위(Verb) : HTTP Method 
- 자원에 대한 행위의 내용 (Representations) : REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타내어 질 수 있다.

### REST API 설계 기본 규칙
1. Uniform Interface(일관된 인터페이스)
URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다. 즉, 특정 언어나 기술에 종속되지 않는다.
 
2. Stateless(무상태성)
- 서버는 각각의 요청을 별개의 것으로 인식하고 처리해야하며, 이전 요청이 다음 요청에 연관되어서는 안된다. 즉 REST API는 서버측에서 클라이언트의 상태를 관리하지 않는다. 
- 서비스의 자유도가 높으며, 서버에서 불필요한 정보를 관리하지 않으므로 구현이 단순하다.

3. Cacheable(캐시 가능)
- Rest API는 결국 HTTP라는 기존의 웹표준을 그대로 사용하기 때문에, 웹의 기존 인프라를 그대로 활용할 수 있다.


4. Client-Server Architecture (서버-클라이언트 구조)
- 클라이언트는 유저와 관련된 처리를, 서버는 REST API를 제공함으로써 각각의 역활이 확실하게 구분되고 일괄적인 인터페이스로 분리되어 작동할 수 있게 한다. 
- 서로 간 의존성이 줄어든다.

5. Self-Descriptiveness(자체 표현)
JSON을 이용한 메시지 포멧을 이용하여 직관적으로 이해할 수 있고 REST API 메시지만으로 그 요청이 어떤 행위를 하는지 알 수 있다.

6. Layered System(계층 구조)
클라이언트와 서버가 분리되어 있기 때문에 중간에 프록시 서버, 암호화 계층 등 중간매체를 사용할 수 있어 자유도가 높다


### URI 설계 원칙
- URI는 명사를 사용한다.
- 슬래시로 계층 관계를 표현한다.
- URI의 마지막에는 슬래시를 붙이지 않는다.
- URI는 소문자로만 구성한다.
- 가독성이 떨어지는 경우 하이픈을 사용한다.


+) URL은 Uniform Resource Locator로 인터넷 상 자원의 위치( 어떤 파일의 위치)를 의미한다. 반면에 URI는 Uniform Resource Identifier로 인터넷 상의 자원을 식별하기 위한 문자열의 구성으로, URI는 URL을 포함하게 된다. 그러므로 URI가 보다 포괄적인 범위라고 할 수 있다.


## Web Server 과 WAS

### Web Server
HTTP를 통해 웹 브라우저에서 요청하는 HTML ,css, 이미지 등 정적인 데이터을 전송해주는 서비스 프로그램을 말한다. 대표적으로 NGIX, APACHE가 있다.

### WAS (Web Application Server)
웹 서버의 기능을 포함(HTTP 요청을 받을 수 있다.) 하고 DB 접속과 애플리케이션 로직 처리를 요구하는 동적인 컨텐츠를 제공하기 위해 만들어진 소프트웨터 프레임 워크이다. (미들웨어)
대표적으로 톰캣, Undertow, Jetty 가 있다.

**WAS의 역할 = Web Server + Web Container**

+) Container란 JSP, Servlet을 실행시킬 수 있는 소프트웨어를 말한다. 즉 WAS는 JSP, Servlet 구동 환경을 제공한다.
+) 미들웨어 : 운영 체제와 응용 소프트웨어의 중간에서 제공받는 서비스 이외에 추가적으로 이용할 수 있는 서비스를 제공하는 컴퓨터 소프트웨어이다.
+) 정적 컨텐츠는 요청 인자 값에 (상태) 상관없이 동일한 컨텐츠를 의미한다. 동적 컨텐츠는 요청 인자에 따라 바뀔수 있는 컨텐츠이다.

### WAS + Web Server
WAS가 동정, 정정 데이터 모두를 처리할 수 있는데 Web Server가 필요한 이유? -> 확장성, 안전성

- 책임을 분리하여 WAS의 서버 부하 방지
- 물리적으로 분리하여 보안 방지
  - SSL 암호화 처리에 앞단에 위치한 웹서버를 사용하여 중요한 정보가 담긴 DB, 로직까지 전파 공격이 전패 되지 못하게 한다.
- 여러 개의 서버를 사용하는 대용량 웹 애플리케이션의 경우 웹 서버와 WAS를 분리하여 무중단 운영을 위한 장애 극복에 쉽게 대응할 수 있다.
  - Load Balancing
  - fail over, fail back, Health check
- 다른 종류의 WAS로 서비스 가능
  - 예를 들어 하나의 서버에서 PHP와 JAVA를 함께 사용할 수 있다.

즉, 클라이언트의 동적인 요청(Request)을 웹 서버가 WAS에 보내고, WAS가 처리한 결과를 웹서버가 클라이언트에게 전달(응답, Response)한다. 웹 서버와 WAS는 소켓을 통해 통신한다.

### Servlet
클라이언트의 동적 요청을 처리하고, 그 결과를 반환하는 자바로 구현되어진 웹 어플리케이션 컴포넌트 또는 기술이다.
WebContainer는 웹 서버로부터 요청이 들어오면 스레드를 생성하고 서블릿 인터페이스를 통해 서블릿 구현체를 실행시킨다.  서블릿은 싱글톤으로 구현되어 있어 메모리를 공유하고 스레드마다 local 변수를 갖는다.


## CORS(Cross-Origin Resource Sharing) : 교차 출처 자원 공유

### Origin

SOP(Same Origin Policy) : 다른 출처의 리소스를 사용하는 것에 제한하는 보안 방식

프로토콜+호스트+포트 가 동일하면 서로 같은 출처라 한다.

### 등장 배경
예전에 웹사이트를 만들때는 대부분 하나의 서버에서 브라우저의 모든 요청을 처리했지만 점점 웹 서비스가 커지면서 브라우저가 다른 출처(Origin)의 자원을 요청할 일이 많아졌다. (예를 들어 지도 API를 사용하여 지도 기능을 추가하는 경우) 하지만 SOP와 반대로 아무런 제약도 존재하지 않는다면 보안상 매우 취약하다. 그래서 다른 출처의 리소스가 필요한 경우,  SOP를 우회하기 위한 방법으로 CORS 가 사용되었다.

즉, CORS란 추가 HTTP 헤더를 사용하여 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근 할 수 있는 권한을 부여하도록 브라우저에 알려주는 정책이다.

### 동작 방식
- Preflight Request
Request 의  Origin과 Response의 Access-Control-Allow-Origin이 동일한지 브라우저가 판단한다.
Options 메서드로 예비 요청을 보내고 본 요청을 보낸다. 예비요청에는 Origin 정보 뿐만 아니라 본 요청에 대한 헤더, http 메서드 등의 정보들도 포함한다. Origin이 동일하면 본요청을 보내고 아니면 에러를 발생시킨다. 예비요청의 응답 status code는 200 이다.

- Simple Request
예비 요청이 없이 본 요청에서 origin 검사를 한다. 요청 메소드는 GET, HEAD, POST 만 사용 가능하고 Content-type에서 Json을 사용하지 못하고 헤더에는 JWT를 포함할 수 없기 때문에 잘 사용되지 않는다.

+) Preflight 가 필요한 이유는 cors 에러를 확인하기 전에 DB와 같은 작업 하는 것을 방지 하기 위해

- Credentialed Request (인증 정보 포함 요청)
인증 관련 헤더를 포함할 때 사용하는 요청

기본적으로 브라우저가 제공하는 비동기 리소스 요청 API인 XMLHttpRequest 객체나 fetch API는 별도의 옵션 없이 브라우저의 쿠키 정보나 인증과 관련된 헤더를 함부로 요청에 담지 않는다. 이때 요청에 인증과 관련된 정보를 담을 수 있게 해주는 옵션이 바로 credentials 옵션이다.

옵션
same-origin (기본값) : 같은 출처 간 요청에만 인증 정보를 담는다.
include : 모든 요청에 인증 정보를 담는다.
omit : 모든 요청에 인증 정보를 담지 않는다.

Access-Control-Allow-Origin : * 은 안된다. 정확한 url 명시
Access-Control-Allow-Credentials : true 롤 설정 필수

