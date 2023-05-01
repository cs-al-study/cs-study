# Servlet

<br>

## Servlet 이란

웹 서버 내부에서 클라이언트 요구에 맞춰 동적으로 반응하는 페이지인 처리를 위해 동작하는 자바 프로그램

- servlet 컨테이너에 의해 실행되고 관리된다.

## Servlet 특징

- 클라이언트의 Request에 대해 동적으로 작동
- HTML을 사용하여 response
- Java 스레드를 이용해 동작
- MVC 패턴에서의 컨트롤러로 이용
- servlet 인터페이스 구현을 위해 generic servlet, http servlet를 상속받아 구현
- UDP 보다 느림

## Apache Tomcat
Tomcat은 WEB/WAS 기능을 가진 전 세계적으로 가장 많이 사용되는 오픈 소스 웹 컨테이너

## WEB , WAS 차이
- WEB
    - 사용자가 요청하면 해당 페이지를 넘겨주는 정적인 방식

    - 필요한 페이지마다 자파스크립트 등으로 복잡한 로직을 구성해서 모든 페이지를 구성해놔야 한다는 단점

- WAS
    - 사용자의 복잡한 로직을 처리하기 위해 요청 내용(request)을 받아 짜여진 로직대로 잘 처리한 뒤 웹페이지를 만들어 사용자에게 응답(response) 해주는 방식

    - 사용자는 웹서버가 주는 페이지만 받아서 실행하므로 내부의 로직을 알 수 없게 되어 보안이 강화

클라이언트WEB에 요청 -> WEB에서 연산이 필요없는 정적 페이지(이미지.. 등)는 자신이 처리하고 연산이 필요한건 WAS에 요청 -> WAS가 연산 결과 WEB에 반환 -> WEB에 클라이언트에 결과 응답

## Servlet filter
클라이언트로 부터 서버로 요청이 들어오기 전에 서블릿을 거쳐서 필터링 하는것
- Servlet은 HTTPServletRequest였다면 Filter는 ServletRequest

- 공통적인 기능을 서블릿이 호출되기 전에 전처리 하거나, 후처리 하고 싶으면 서블릿 필터로 구현

- 기능 종류
    - 사용자 인증 필터
    - 로깅 및 감시 필터
    - 이미지 변환 데이터 압축
    - 암호화 등
    
## Servlet container
http 요청을 받아 servlet을 실행시키고 생명주기를 관리하는 컴포넌트

- 멀티 스레딩을 지원하고 관리한다.
- 웹 서버(nginx, apache..)와 소캣으로 통신할 수 있는 API 지원
- 선언적인 보안 관리
    - Web.xml에 정의하며, 보안에 대해 수정할 일이 생겨도 자바 소스 코드를 수정하여 다시 컴파일 하지 않아도 된다

대표적인 container로 tomcat, jetty, jboss등이 있다

## 동작과정
1. 사용자(클라이언트)가 URL을 입력하면 동적 자원 요청일 경우 HTTP Request가 Servlet Container로 전송
    - 정적 페이지는 WEB 서버가 제공

2. 요청을 전송받은 servlet container에서 HttpServletRequest, HttpServletResponse 객체를 생성

3. 요청된 URL을 배포서술자(DD, Deplyment Descriptor) 분석을 통해 요청된 서블릿 클래스를 찾음

4. 서블릿 컨테이너에서 실행된 적 or 메모리에 생성된 인스턴스(process)가 있는지 체크
    - 처음 실행 : 인스턴스 생성 후 init() 호출 -> 초기화 후 스레드 생성
    - 이미 실행 : 기존 인스턴스에 스레드 생성

5. 컨테이너는 해당 서블릿에서 service() 메서드를 호출한후 HTTP 요청 메서드에 따라 doGet() 또는 doPost()를 호출
    - request와 response 객체가 제공

6. doGet(), doPost()메서드는 요청을 처리하여 HttpServletResponse 객체에 응답을 전달

7. 응답이 완료되면 HttpServletRequest, HttpServletResponse객체는 소멸


    

    
