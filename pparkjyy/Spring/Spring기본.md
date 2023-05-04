# Spring 기본

<br>

## Spring vs Spring MVC vs Spring Boot

- Spring : Java 기반의 웹 애플리케이션 개발을 위한 오픈소스 프레임워크
- Spring MVC : 웹 애플리케이션 개발에 있어 MVC 패턴을 적용할 수 있도록 Spring에서 제공하는 프레임워크
- Spring Boot : Spring 설정들을 자동화하는 Spring 기반의 프레임워크

**Spring vs SpringBoot**  
a) Auto Configuration 자동 실행  
b) 쉬운 의존성 관리  
c) 내장 서버

**SpringBoot vs SpringMVC**
1) 빌드 구성을 수동할 필요 없음 / 해야함
2) 배포 구성 필요 x / 필요함
3) boot가 좀더 개발 시간 단축

규모가 작아 WAS가 따로 필요없으면 boot 아니면 MVC

### Spring MVC 동작 과정

- 프론트 컨트롤러 패턴 / 프론트 컨트롤러가 Dispatcher Servlet
- Dispacher Servlet가 HandlerMapping 객체를 이용해 요청과 매핑되는 controller을 검색
- Handler Adapter가 요청에 맞는 ModleAndView를 반환 /  이때, 컨트롤러 사용
- 그리고 받은 ModleAndView객체에서 View name에 맞는 이름을 검색하여 view를 만들어 반환

- Model : 백그라운드에서 동작하며, 사용자가 원하는 데이터나 정보를 제공한다.
- View : 사용자의 요청을 화면으로 출력한다.
- Controller : 사용자의 요청을 처리하고, 그 요청에 따른 전체적인 흐름을 제어한다.

**구조**
![img](https://media.vlpt.us/images/gillog/post/566eb042-5ddf-45cb-99ee-3ee1153e7e6b/a.png)


### MVC1 과 MVC2

#### MVC1
모든 클라이언트 요청과 응답을 JSP가 담당한다. 즉, JSP가 Controller 와 View 의 기능을 모두 담당하는 구조이다
(jsp 페이지 안에서 로직 처리를 위해 자바코드가 함께 사용)

장점 : 단순해서 작은 프로젝트에서 사용될 수 있다.
단점 : 웹이 복잡해질수록 유지보수가 힘들어진다. (JSP 내에서 html, 자바코드 같이 사용)

#### MVC2
요청 결과를 출력해 주는 뷰의 역할을 jsp 가 담당하고, 흐름 제어와 비즈니스 로직 처리 요청하는 컨트롤러의 역할을 서블릿이 담당한다.

구조가 복잡하지만 유지보수, 확장에 용이하다

## Dispatcher Servlet

: 가장 앞단에서 HTTP 프로토콜로 들어오는 모든 요청을 가장 먼저 받아 적합한 컨트롤러에 위임해주는 프론트 컨트롤러(Front Controller)

- 프론트 컨트롤러 패턴과 관련있음
- 클라이언트 -> 서블릿 컨테이너 -> 디스패처 서블릿 -> 공통적인 작업을 먼저 처리 -> 세부 컨트롤러에게 작업 위임

**장점**

- dispatcher-servlet이 해당 어플리케이션으로 들어오는 모든 요청을 핸들링
- 공통 작업을 처리
- 우리는 컨트롤러를 구현해두기만 하면 디스패처 서블릿가 알아서 적합한 컨트롤러로 위임을 해주는 구조

**단점**

- Dispatcher Servlet이 모든 요청을 처리하다보니 이미지나 HTML/CSS/JavaScript 등과 같은 정적 파일에 대한 요청마저 모두 가로채는 까닭에 정적자원(
  Static Resources)을 불러오지 못하는 상황도 발생
    - 해결방법
        1. 정적 자원에 대한 요청과 애플리케이션에 대한 요청을 분리
        2. 애플리케이션에 대한 요청을 탐색하고 없으면 정적 자원에 대한 요청으로 처리
        

## IoC (Inversion of Control) : 제어의 역전

제어의 역전의 방법 중 하나가 의존성 주입(DI)이다.

- 의존관계의 제어를 개발자가 직접 해주었다. 그러나 제어권이 컨테이너로 넘어갔고 객체의 생성부터 생명주기의 관리까지 객체에 대한 제어권이 바뀐것을 IoC라고 한다.

![img](https://t1.daumcdn.net/cfile/tistory/9933C93F5AF277561A)

### Spring 에서 IoC 패턴을 사용하는 이유

: 변경에 유연한 코드 구조를 가져가기 위해서

## DL(Dependency Lookup) : 의존성 검색

- 컨테이너에서 제공하는 API를 이용해 사용하고자 하는 빈(Bean)을 저장소에서 Lookup하는 것을 말한다.

## DI (Dependency Injection) : 의존성 주입

- 각 객체간의 의존성을 컨테이너가 자동으로 연결해주는 것으로 개발자가 빈(Bean) 설정파일에 의존관계가 필요한 정보를 추가해주면 컨테이너가 자동적으로 연결해준다.
- Spring 프레임워크에서는 Setter Injection, Constructor Injection 두 가지 방식이 있다.

### IoC 컨테이너

: 모든 작업을 사용하는 쪽에서 제어하게 되면서 IoC 컨테이너에서 제어하게 되는데, 기본적으로 컨테이너는 객체를 생성하고 객체간의 의존성을 이어주는 역할을 한다.
- Application Context
- Bean Factory
위 둘은 무겁고 가볍고의 차이

### 빈(Bean) 요청 시 처리 과정

클라이언트에서 해당 빈을 요청하면 애플리케이션 컨텍스트는 다음과 같은 과정을 거쳐 빈을 반환한다.

1. ApplicationContext는 @Configuration이 붙은 클래스들을 설정 정보로 등록해두고, @Bean이 붙은 메소드의 이름으로 빈 목록을 생성한다.
2. 클라이언트가 해당 빈을 요청한다.
3. ApplicationContext는 자신의 빈 목록에서 요청한 이름이 있는지 찾는다.
4. ApplicationContext는 설정 클래스로부터 빈 생성을 요청하고, 생성된 빈을 돌려준다.
   ![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FLuLhA%2Fbtq4squITMm%2FmqqtgMfiiahkAFBuPLMaLk%2Fimg.png)

## Bean, Component

### Bean

: 스프링 컨테이너가 설정 파일을 읽어서 정보를 읽고 관리한다.

### Bean 설정 방식

1. XML 방식 -> `<bean>`으로 등록
2. java Config 방식 -> @Bean

### Bean 등록 과정

Bean은 런타임시점에 ComponentScan이 설정 파일들을 읽고 ApplicationContext에 의하여 IoC컨테이너에 등록된다

### Bean vs Component

- @Component는 Class Level에서, @Bean은 Method Level에서 적용된다.
- @Bean은 사용자가 컨트롤 하지 못하는 Class나, 좀 더 유연하게 객체를 생성해서 넘기고 싶을 때 (이를 테면 외부 라이브러리),
- @Component는 Class 자체를 빈으로 등록하고 싶을 때, 사용하면 된다.
- @SpringBootApplication이 @Configuration, @ComponentScan을 상속받고 있다.

### @Component @Service @Controller

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fk0eNV%2FbtqIdTkRQ2A%2FdMWPvZl1djOkItdzxFeWH0%2Fimg.jpg)


### @Component

: **Spring에서 관리되는 객체임**을 표시하기 위해 사용하는 가장 기본적인 annotation이다. 즉, scan-auto-detection과 dependency
injection을 사용하기 위해서 사용되는 가장 기본 어노테이션이다.

### @Service

: 비즈니스 로직이나 respository layer 호출하는 함수에 사용된다.

### @Controller

: Web MVC 코드에 사용되는 어노테이션이다. @RequestMapping 어노테이션을 해당 어노테이션 밑에서만 사용할 수 있다.

- Component vs Controller/Service/Repository  
  : 일반적으로 컴포넌트 클래스들에 @Component를 붙일 수 있지만, @Repository, @Service, @Controller를 붙인다면 도구들이 클래스들을 처리하는데
  더 적합하도록 할 수 있고 관점(aspects)에 더 연관성을 부여할 수 있다.
  (= AOP 를 통한 처리가 쉽게 가능하다)

## Container

- Application Context
  : 직접 오브젝트를 생성하고 관계를 맺어주는 코드가 없고, 그런 생성 정보와 연관관계 정보에 대한 설정을 읽어 처리한다.

- IoC 컨테이너
  : 객체에 대한 생성 및 생명주기를 관리할 수 있는 기능을 제공
    - IoC Container는 오브젝트의 생성과 관계설정, 사용, 제거 등의 작업을 대신 해준다하여 붙여진 이름이다.
    - 이때, IoC Container에 의해 관리되는 오브젝트들은 Bean 이라고 부른다.

## VO vs DTO vs DAO

- DAO(Data Access Object)는 데이터베이스의 데이터에 접근하기 위한 객체이다. 데이터 베이스 접근을 위한 로직과 비즈니스 로직을 분리하기 위해서 사용된다.

- DTO(Data Transfer Object)는 계층간 데이터 교환을 위한 자바 객체이다. 여기서 계층은 컨트롤러, 뷰, 비즈니스 로직, presistent layer 가 있다. 

-VO(Value Object) : VO는 값 자체에 의미가 있는 객체로ㅡ DTO와 Data를 전달하는 객체로 동일한 개념이지만,  read only 특징을 가지고 있다는 차이가 있다. 같은 객체라는 것을 보장하기 위해서는 equals와 hashcode를 재정의해주어야한다.

- Entity 클래스는 실제 DataBase의 테이블과 1 : 1로 Mapping 되는 Class로, DB의 테이블내에 존재하는 컬럼만을 속성(필드)으로 가져야 한다.
