# Join
- 한 데이터베이스 내의 여러 테이블의 레코드를 조합하여 하나의 열로 표현한 것

<br>

## 조인의 종류

![image](https://user-images.githubusercontent.com/92436863/233326557-2af9207e-6cbc-45ff-a94c-b0c9c8169d7e.png)


### 내부조인

#### 교차 조인 (CROSS JOIN)
- 두 테이블에 대한 곱집합 결과 / 테이블 A와 B의 각 행을 다 조합한 결과

#### 내부 조인 (INNER JOIN)
- 두 테이블에 대한 교집합 결과 / 공통된 부분만 출력

#### 등가 조인 (EQUI JOIN)
- 동등비교(=)를 사용하는 조인

#### 비등가 조인(NON-EQUI JOIN)
- 동등비교를 사용하지 않는 조인 / 비교등을 사용하면 비등가

#### 자연 조인(NATURAL JOIN)
- 동등 조인의 한 유형으로 두 테이블의 컬럼명이 같은 기준으로 조인 조건문이 암시적으로 일어나는 내부 조인
- 같은 이름 가진 칼럼 한번만 출력

<br>

### 외부조인

#### 왼쪽 (LEFT OUTER JOIN)
- 왼쪽 테이블 정보 + 오른쪽이랑 겹치는 부분 까지 출력 / 안겹치는 부분은 NULL

#### 오른쪽 (RIGHT OUTER JOIN)
- 오른쪽 테이블 + 왼쪽이랑 겹치는 부분 출력 / 안겹치는 부분 NULL

#### 완전 (FULL OUTER JOIN)
- 오른쪽 외부조인 + 왼쪽 외부조인 결과

<br>

### 셀프 조인 (SELF JOIN)
- 자기자신과 조인
- 칼럼간의 관계를 이용해서 데이터를 추출할때 매우 유용

### 안티 조인 (ANTI JOIN)
- 서브 쿼리내에서 존재하지 않는 데이터만 추출하여 메인 쿼리에서 추출하는 조인

### 세미 조인 (SEMI JOIN)
- 안티 조인과 반대로 서브 쿼리 내에서 존재하는 데이터만을 가지고 메인 쿼리에서 추출하는 방식

<br>

# Sharding & Master/Slave

## 샤딩(sharding)
- 같은 테이블 스키마를 가진 데이터를 다수의 데이터베이스에 분산하여 저장하는 방법

### 장단접
- 장점
    - 스캔의 범위가 줄어 쿼리 반응이 빠름
    - 특정 DB의 장애가 전면장애로 이어지지 않음
- 단점 
    - 잘못썼을떄의 risk
    - 데이터가 한쪽 shard에 쏠리면 무의미
    - 한번 쪼개면 다시 돌리기 어려움

### 기법
- Hash Sharding, Dynamic Sharding, Entity Group, Pitfall .. 

## Master & Slave
- MySQL을 사용할 때 이중화 구성(Master-Slave)을 하는 경우가 많음. 데이터가 날아가는 것을 방지 이를 Replication 이라함
- Master는 등록/수정/삭제 쿼리 요청이 있을 시 Binarylog를 생성하여 Slave로 전달
- Slave는 Master의 정보를 복제해놓는 역할 담당 / 또한 읽기 쿼리 요청 담당
- 쿼리 요청을 분담함으로써 DB 부하 분산 가능