# 컬렉션 1

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