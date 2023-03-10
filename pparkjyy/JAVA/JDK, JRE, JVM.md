# JDK, JRE, JVM

<br>

<img width="400" src="https://user-images.githubusercontent.com/92436863/221352074-696cb05e-b842-49fd-a8ed-b16e5038a29d.png">

### JVM : Java Virtual Machine | 자바 가상 머신
- 자바 프로그램을 컴파일 해서 나온 결과인 바이트코드(.class)를 실행시켜주는 가상 머신
- OS 별로 존재함 (OS에 종속적)

### JRE : Java Runtime Environment | 자바 실행 환경
- JVM을 동작하는데에 필요한 각종 자바 라이브러리를 담고 있음
- 자바 프로그램 실행기 (java.exe)와 라이브러리를 자바 코드와 결합 한 후 JVM이 원활하게 잘 작동할 수 있도록 환경을 구성하는 역할

### JDK : Java Development Kit | 자바 개발 도구
- JRE와 javac 등의 컴파일러, 디버거등을 포함하는 프로그램

<br>

## JAVA 컴파일과정

![image](https://user-images.githubusercontent.com/92436863/221355639-2537f753-9fd5-4285-a555-d651e0ef5681.png)

자바는 OS에 독립적인 특성을 가지고 있음(JVM 때문)

### 컴파일 순서
    1. 개발자가 소스코드(.java) 작성
    2. 컴파일러(`javac`)가 java 파일을 컴파일 | .java -> .class
    3. 바이트코드(.class)를 JVM의 클래스로더(Class Loader)에게 전달
    4. 클래스 로더는 동적로딩(Dynamic Loading)을 통해 필요한 클래스들을 런타임 데이터 영역(Runtime Data Area), 즉 JVM의 메모리에 올린다.
    5. JVM의 실행엔진(Execution Engine)이 JVM 메모리에 올라온 바이트 코드를 실행

<br>

### 컴파일 언어 vs 인터프리터 언어

#### 컴파일 언어
- 빌드타임에 작성한 모든 소스코드에 대한 기계어를 생성하고 런타임에 생성된 모든 기계어를 한번에 JVM같은 machine으로 보냄
- 컴파일 과정에서 사간이 많이 소요되고 메모리도 많이 차지함
- 컴파일 이후에는 실행이 빠름
- 대표적으로 C, C++

#### 인터프리터 언어
- 빌드타임에는 별다른 동작을 하지 않고, 런타임시 한 행씩 해석하여 알맞은 기계어를 생성한 뒤 명령어를 실행
- 실행속도가 느리지만 코드 변경시 빌드 과정없이 즉시 실행 가능하여 테스트에 용이
- 별도의 실행파일이 존재하지 않음
- 소스 코드가 실행되기 전까지는 소스 코드의 버그를 인지하는 것이 어렵다.
- 빌드 속도는 빠르지만 연산 속도나 실행 속도에 민감한 프로그램은 인터프리터 언어로 개발하지 않음
- 대표적으로 R, Python, Ruby

#### 자바는 컴파일? 인터프리터?
- 자바는 빌드타임에 자바 코드를 컴파일하여 바이트 코드를 생성하고 런타임 시 JVM의 실행 엔진이 jvm 메모리에 적재된 바이트 코드를 기계어로 인터프리터하여 실행
- 컴파일과 일터프리터 둘다 사용하며 순수 컴파일에 비해 실행 속도가 느림
- JIT 컴파일러를 사용하면 매번 기계어로 번역하지 않고 이전에 실행한 코드를 캐싱하여 재사용하기 때문에 좀 더 빠른 실행이 가능

<br>

## JVM
- 4가지 영역으로 구분

### Class Loader
- 클래스 파일을 로드하고 링크를 통해 비치하는 모듈
- 클래스들은 동적 로딩됨 (실행시 모든 클래스가 로드되는게 아닌 필요한 시점에 로딩)


### Runtime Data Area
- JVM의 메모리 영역으로 5가지 영역으로 분리
- Method와 Heap 영역만이 공유 메모리 영역

#### Method
- 클래스, 변수, 메소드, static 변수, constant pool 정보가 저장되는 영역
- 클래스가 로드될때 할당됨

#### Heap
- 동적할당된 객체와 배열이 저장되는 영역
- 런타임시 할당됨

#### Stack
- 지역변수, 매개변수, 리턴값 등의 임시값이 생성될때 저장되는 영역
- 메소드 호출시마다 개별 스택 프레임이 생성되고, 종료시 해제됨
- 컴파일시 할당됨

#### PC register
- 현재 스레드가 실행되는 부분의 주소와 명령을 저장
- 스레디가 생성될때 할당됨

#### Native Method
- 자바 외 언어로 작성된 네이티브 코드를 위한 메모리 영역(JNI)

### Execution Engine
- JVM 메모리 영역의 바이트 코드를 명령어 단위로 실행함
- 두가지 실행방법
    - 인터프리터 : 바이트 코드를 하나씩 읽어서 실행 (느림, 초기에 사용)
    - JIT : 바이트코드 전체를 바이너리 코드로 컴파일 후 실행 (빠름)


### Garbage Collector
- JVM의 Heap 영역에서 동적으로 할당했던 메모리 중 필요 없게 된 메모리 객체(garbage)를 모아 주기적으로 제거하는 프로세스
- C/C++ 에서는 수동이로 메모리 할당과 해제를 해줘야 하지만 java에서는 필요없음

#### 동작 방식

![image](https://user-images.githubusercontent.com/92436863/221358936-9ff16e05-b73a-4ccb-840c-ac1ccfb7a592.png)

Mark and Sweep (optionally Compact)

- Mark
    - 모든 변수를 스캔하면서 각가 어떤 객체를 참조하고 있는지 찾아서 마킹
    - 유효한 참조를 한다면 Reachable, 그렇지 않다면 Unreachable

- Sweep
    - 마킹되지 않은 객체를 Heap에서 제거

- Compact
    - 단편화 된 메모리로 정리



![image](https://user-images.githubusercontent.com/92436863/221358967-eee98bfa-2651-4a27-a0ab-be3ef7235a54.png)

- 영 제너레이션
    - 새롭게 생성된 객체가 할당되는 공간
    - 에덴과 서바이버 공간으로 나뉜다

- 올드 제너레이션
    - 영 제너레이션에서 특정 age가 넘은 참조 메모리들이 이동하는 공간
    - 이 공간이 가득차면, mager GC(올드제너레이션에서 mark and sweep)가 일어난다.


1. 객체가 힙메모리에 할당 되면 우선 에덴에 할당. 에덴 영역이 가득 찬다면, 마이너 GC(에덴 영역에서의 mark and sweep)가 일어남. 여기에서 reachable하여 살아남은 객체는 servivor 영역으로 이동
2. 살아남은 객체는 age 증가
3. 또 다음 마이너 gc가 일어나면, 새로운 reachable 객체들은 서바이버 영역으로 이동하고, 기존 서바이버는 age가 1 증가
4. 이 과정이 반복되어 age가 일정 임계점을 돌파하면, old generation 영역으로 이동(promotion)한다.


- 영 제너레이션 올드 제너레이션 나눈 이유
    - 대부분의 객체는 금방 접근 불가능한 상태가 된다.
    - 오래된 객체에서 젊은 객체로의 참조는 아주 적게 존재한다.
    - 따라서 힙 전체에서 GC를 진행하지 않고 영 제너레이션 에서만 GC를 수행했을때 대부분의 garbage가 수거되어 메모리 낭비를 막을 수 있다.

<br>

## Java8 , java11

### Java 8에서 추가된 기능
- Heap Permanent Generation 제거
- 인터페이스 디폴트 메소드와 정적 메소드 추가
- 함수형 인터페이스, 람다 표현식, 메소드 참조 기능 추가
- 스트림 API 도입
- 새로운 날짜 관련 라이브러리 추가
- Optional 지원
- 병렬 처리 지원

### Java 11에서 추가된 기능
- String에 새로운 메소드 추가
- Files 클래스에 새로운 메소드 추가
- 컬렉션 인터페이스에 새로운 메소드 추가
- Predicate 인터페이스에 새로운 메소드 추가
- 람다에서 로컬 변수 Var사용
- 자바 파일 실행 방식 단순화

