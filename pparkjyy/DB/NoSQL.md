# NoSQL

<br>

## NoSQL이란?

- Not Only SQL
- 비관계형 데이터베이스
- 대량의 분산된 데이터를 저장하고 조회하는데 특화
- 빅데이터 처리시 RDBMS로만 트래픽을 감당하기 힘들경우에 사용

### NoSQL 특징

- RDBMS와 달리 데이터 간의 관계를 정의하지 않는다
    - RDBMS는 데이터간 관계를 외래키 등으로 정의하고 JOIN연산을 수행할 수 있지만, NoSQL은 JOIN 불가
- RDBMS에 비해 대용량의 데이터를 저장할 수 있다.
- 분산형 구조이다.
    - 여러 곳의 서버에 데이터를 분산 저장
- 고정되지 않은 테이블 스키마를 갖는다.

### NoSQL 장단점

- 장점
    - RDBMS에 비해 저렴한 비용으로 분산, 병렬처리 가능
    - 비정형 데이터 구조 설계로 설계 비용 감소
    - Big Data 처리에 효과적
    - 가변적인 구조로 데이터 저장 가능
    - 데이터 모델의 유연한 변화가 가능

- 단점
    - 데이터 업데이트 중 장애 발생시 데이터 솔실 발생 가능
    - 많은 인덱스를 사용하려면 충분한 메모리가 필요
    - 데이터 일관성이 항상 보장되지 않음

### 종류

- `Key/Value` : Redis, Memcache, Oracle NoSQL
    - Key-Value 하나의 묶음으로 저장되는 구조
- `Document Store` : MongoDB
    - 테이블의 스키마가 유동적, 즉 레코드마다 각각 다른 스키마를 가질 수 있다.
- `Wide Column Storage` : DynamoDB, Cassandra, HBase
    - 각각 다른 값의 다른 수의 스키마를 가질 수 있다.

<br>

## MongoDB

- Document-Oriented DB
- BSON(Binary JSON) 형태로 저장
- 다양한 인덱스 지원
    - B-Tree 구조로 되어있음
- memory mapped file으로 파일 엔진 DB
    - 메모리 크기가 성능 좌우

<br>

## Redis

- Key-value 형태
- 프로세스 기반 싱글스레드
- 인메모리 기반
    - 속도가 매우 빠름
    - 기본적으로 데이터를 디스크에 저장하지 않음
    - 하지만 저장할 수도 있음
- String, Set, Sorted Set, Hash, List 자료구조 지원
    - 캐싱에 자주 사용됨

<br>
