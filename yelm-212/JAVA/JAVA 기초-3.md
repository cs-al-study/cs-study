# Stream 
- for문 / Iterator를 사용할 경우 **코드의 복잡도를 개선**하기 위해 고안됨
- Collection에 저장되어 있는 element들을 하나씩 순회하며 처리가 가능하다.
- 생성, 중간 연산, 최종 연산 세 단계의 파이프라인으로 구성 
	- -> 더 찾아보기
- 원본 데이터 소스 변경하지 않음(read-only)
- 일회용임
- 내부 반복자
- `count()`. `max()`, `min()` + `sum()` `average()`

| 스트림(Stream) | 이터레이터(Iterator) |
| --- | --- |
| 병렬 또는 순차적으로 처리할 수 있는 데이터 요소의 시퀀스를 나타냄 | 하나씩 데이터 요소에 접근할 수 있는 시퀀스를 나타냄 |
| 순차 및 병렬 처리 모두 지원함 | 순차 처리만 지원함 |
| 데이터 처리를 위한 API를 제공함 | 데이터 순환 및 제거에 대한 간단한 API만 제공함 |
| 필요할 때에만 데이터를 처리하도록 lazy evaluation를 지원함 | 항상 데이터를 즉시 처리함 |
| filtering, mapping, reducing 및 collecting 등의 작업을 지원함 | Collection에서 요소 제거만 지원함 |
| Collection, 배열 및 기타 소스에서 생성할 수 있음 | Collection 및 배열에서만 생성할 수 있음 |

## lambda
- 메서드를 간단하고 편리하게 표현하기 위해 고안된 문법 요소
- 반환 타입과 이름이 생략 가능해 익명 함수라 하기도 함
- 멀티쓰레드를 활용해 병렬처리를 할 수 있다
- 표현식 : `() -> {}`

## reflexion
- 구체적인 클래스 타입을 알지 못해도 그 클래스의 메소드, 타입, 변수들에 접근할 수 있도록 해주는 자바 API
- 런타임 단계에서 클래스, 인터페이스, 필드, 메서드를 검사하거나 수정할 수 있다.
- 객체 인스턴스화, 메소드 호출, 필드 값을 가져오거나 설정할 수 있다.
- 클래스의 인스턴스를 동적으로 생성할 수 있다.
- 객체의 메소드를 동적으로 일으킬(invoke) 수 있다
- 객체의 필드에 접근과 수정을 동적으로 할 수 있다.
- 프레임워크나 IDE에서 reflexion의 동적 바인딩 이용한 기능을 제공함 
	- ex/ 인텔리제이 자동완성 기능, 스트링 어노테이션 등...
## dynamic proxy
- 프록시는 타겟 코드의 수정없이 접근제어 혹은 부가기능을 추가하기 위해 주로 사용되나, 일반적인 프록시는 반복되는 코드가 발생하는 단점이 있음
- 런타임 시점에 프록시 클래스를 만들어주는 방식 
- `newProxyInstance()` Reflexion API 사용
 ```
 @CallerSensitive 
 public static Object newProxyInstance(ClassLoader loader, 
				 Class<?>[] interfaces, 
				 InvocationHandler h)
```
-   `ClassLoader` : 프록시 클래스를 만들 클래스로더
-   `Class` : 프록시 클래스가 구현할 인터페이스 목록(배열)
-   `InvocationHandler` : 메소드가 호출되었을때 실행될 핸들러
	-  `invoke()` 추상메서드 하나만 정의되어있는 걸 볼 수 있다.
		- 동적 프록시의 메소드가 호출되었을 때 이를 대신 실행해주는 메소드.
		- -> 코드 중복을 줄일 수 있음