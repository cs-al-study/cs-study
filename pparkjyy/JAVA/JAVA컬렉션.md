# 컬렉션

: 컬렉션 프레임워크란, **데이터를 쉽고 효과적으로 처리하기 위해 표준화된 방법을 제공하는 클래스의 집합**

- List
    - 특징 : 순서가 있는 데이터의 집합, 데이터의 중복을 허용
    - 구현 클래스 : ArrayList, LinkedList, Stack ...
- Set
    - 특징 : 순서를 유지하지 않는 데이터의 집합. 데이터의 중복을 허용하지 않는다
    - 구현 클래스 : HashSet, LinkedHashSet, TreeSet ...
- Map
    - 특징 : 키(Key)와 값(Value)의 쌍(Pair)으로 이루어진 데이터의 집합
      키 중복 허용 X, 값의 중복 허용 O, 순서 유지 X
    - 구현 클래스 : HashMap, Hashtable, LinkedHashMap, TreeMap ...


<br>

## hashcode() & equals()
hashcode, equals 모두 Object 클래스에 정의되어 있다.

### 동등성 vs 동일성
- 동일성 : 두 객체가 주소까지 완전히 동일한 객체인 경우 만족
    - 동일성 비교는 ==
- 동등성 : 두 객체가 가전 정보를 비교해 동등하다 판단되는 경우
    - 동일성 비교는 equal()
### equals()
- 2개의 객체의 동등성을 비교하는 메서드로 == 연산을 사용하여 객체의 주소값 비교


### hashcode()
- 객체가 가지는 고유의 값을 반환하는 메서드
- Object 클래스의 기본 메소드는 객체의 메모리 주소값을 해시코드로 만들어 반환


### hashcode 와 equals의 관계

Collection(HashMap, HashSet, HashTable)은 객체의 동등성을 비교할 떄,**hashcode**메서드를 실행해서 리턴된 해시코드 값이 같은지 본다. 해시 코드값이 다르다면 다른 객체라고 판단 같다면 **equals()** 메서드로 다시 비교한다.

- 두 객체가 equals()에 의해 동일하다면, 두 객체의 hashcode() 값도 일치
- hashcode 값이 같다고 해서 equals 결과가 true일 필요는 없다.
- equals() 와 hashcode()는 같이 재정의해야 한다.

### Tread Safe & Syncronized

#### Tread Safe
- 여러 스레드에서 클래스 혹은 클래스의 객체에 동시에 접근해서 사용하더라도 정확하게 동작함을 의미


#### Tread Safe 하지 않은 경우 ( value++ 시 )
![image](https://user-images.githubusercontent.com/92436863/224007218-25a1522f-af51-476d-b1b8-11fb54af80d6.png)

#### Syncronized (동기화)
lock을 걸어 여러 스레드가 대상에 동시에 접근하는 상황을 방지한다. 임계영역을 가지고 있는 lock을 단 하나의 스레드에게만 허용
- Synchronized method는 함수와 자신이 포함된 객체에 lock을 건다.
- Synchronized method는 필요한 부분만 동기화 처리를 해줄 수 있다.
- 부모 클래스의 메소드에 synchronized 키워드로 임계영역을 설정해주면, 서로 다른 두 자식 객체가 오버라이딩 한 동기화된 메소드를 사용할 수 있다.

## String

: 자바에서 제공하는 문자열 클래스로 문자열과 관련된 다양한 유용한 기능들을 제공하는 클래스

- String 인스턴스는 한번 생성되면 읽기만 가능하며 수정하는 것은 불가
- 불변 객체(Immutable Object)

### String vs StringBuffer vs StringBuilder

#### StringBuffer

: 내부적으로 버퍼(buffer)라고 하는 독립적인 공간을 가집니다. 버퍼 크기는 기본적으로 16 문자를 저장할 수 있으며, 생성자를 통해 별도로 크기를 지정할 수 있다
**주요 메소드 종류**

- append()
- capacity() : 현재의 버퍼 크기를 반환
- delete(int start, int end) : 해당 문자열의 start ~ (end-1) 인덱스에 해당하는 문자 제거
  **String vs StringBuffer**  
  String 클래스는 변경이 불가한 반면, StringBuffer 클래스의 인스턴스는 그 값을 변경할 수도 있고, 추가할 수도 있다  
  따라서 공간 낭비가 String에 비해 적고, 속도도 빨라진다
  이유 : 덧셈(+) 연산자를 이용해 String 인스턴스의 문자열을 결합하면, 내용이 합쳐진 새로운 String 인스턴스를 생성

### Immutable Object

: 생성 후 그 상태를 바꿀 수 없는 객체

- ex ) String, Integer, Boolean
- 장점
    - 객체에 대한 신뢰도가 높아집니다. 객체가 한번 생성되어서 그게 변하지 않는다면 transaction 내에서 그 객체가 변하지 않기에 우리가 믿고 쓸 수 있기 때문
    - 생성자, 접근메소드에 대한 방어 복사가 필요없다
    - 멀티스레드 환경에서 동기화 처리없이 객체를 공유할 수 있다
- 단점
    - 객체가 가지는 값마다 새로운 객체가 필요하다
    - 따라서 메모리 누수와 새로운 객체를 계속 생성해야하기 때문에 성능저하를 발생시킬 수 있다

### StringBuilder vs SringBuffer

#### StringBuilder가 유리한 점

- **단일 스레드 환경**에서의 비번한 추가, 수정, 삭제가 일어나는 경우 StringBuffer에 비해 효율적

#### StringBuffer가 유리한 점

- **멀티 스레드 환경**에서의 빈번한 추가, 수정, 삭제가 일어나는 경우 StringBuilder에 비해 효율적

### String a = "" vs String a = new String("")

#### String a = new String("") - new 연산자를 이용하는 방식

- Heap 영역에 메모리가 할당
- 같은 문자열이라도 다른 객체라서 선언한 만큼의 새로운 객체가 메모리에 할당

#### String a = "" - 리터럴을 이용하는 방식

- String을 리터럴로 선언하면 내부적으로 String의 intern() 메소드가 호출
  intern() 메소드는 주어진 문자열이 **Heap의 String Constant Pool**에 존재하는 검색 
  만약 있다면 그 주소값을 반환하고 없다면 여기에 새로 하나 만들고 그 주소값을 반환


## List
### ArrayList vs LinkedList
검색은 ArrayList가 메모리상 연속되어서 할당되어있기 때문에 효율적이다
하지만 삽입하거나 삭제 하는 등의 연산은 이전 노드와 다음 노드를 연결하면 됨으로 LinkedList가 더 효율적


## Map
특징 : 키(Key)와 값(Value)의 쌍(Pair)으로 이루어진 데이터의 집합


#### HashMap
- 정렬이 되어있지 않다. 즉, 일정한 순서가 없다
- key나 value값은 null이 허용된다
- key로 올 수 있는 타입은 integer, string, 객체 등이 가능
- 객체를 key로 갖는 경우 hashcode()와 equals()를 재정의해줘야한다
- 비동기적이다


#### HashTable
- get(), put() 메서드를 확인해보면 synchronized하게 구현
- HashMap과 달리 비동기적(unsynchronized)
- key나 value값은 null이 허용되지 않는다

**충돌 해결 방법**
1. Separate Chaining 방식 : 연결리스트나 트리 형태로 엔트리에 값을 이어 붙이는 방식
2. Open addressing 방식 : hash table array의 빈 버킷을 찾아 저장하는 방식, 탐색시 비효율적
   - 선형 탐색법 : 해시 충돌시 다음 버킷, 혹은 몇 개를 건너뛰어 데이터를 삽입
   - 2차 검색법 : 원래 저장할 위치로부터 떨어진 영역을 차례대로 검색하여 첫번째 빈 영역에 키를 저장하는 방법
   - 이중 해싱 : 해시 충돌시 다른 함수를 한번 더 적용한 결과를 이용
   - 리사이징 : 새로운 배열에 기존 배열의 키를 새롭게 재 해싱

#### LinkedHashMap
- 순서가 있다
- 조회보다 삽입, 삭제가 효율적이다


#### TreeMap
- red-black tree 구조를 구현한 것으로 정렬된 키(key)를 가지고 있다
- red-black tree 규칙 : 왼쪽 < 부모 < 오른쪽


#### HashTable vs HashMap
- 동기화 유무
  : HashTable 동기적, HashMap 비동기적
cf) Hashtable은 모든 데이터 변경 메소드가 synchronized로 선언되어 있어서, 메소드 호출 전
스레드 간의 동기화 lock을 통해 멀티 스레드 환경에서 data의 무결성을 보장해준다. (thread-safe)

- null 허용 유무
  : HashTable 허용 안됨, HashMap 허용


#### LinkedHashmap vs Hashmap
- 순서의 유무
- 연산에서의 성능 차이
  : HashMap은 순차적으로 데이터를 저장하는 반면 LinkedHashMap은 데이터들을 연결해주기 때문에
    LinkedHashMap이 중간에 위치한 데이터를 접근하여 삽입, 수정, 삭제할 때는 속도면에서 더 유리


### HashMap vs ConcurrentHashMap
- 동기화 유무
  : HashMap 비동기적, ConcurrentHashMap 동기적
- null 허용 유무
  : HashMap null 허용, ConcurrentHashMap null 허용 안됨
