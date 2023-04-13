# DNS

<br>

## DNS (Domain Name System)
- 도메인 이름(www.naver.com)을 IP 주소로 변환하는 시스템


## 동작 원리
![image](https://user-images.githubusercontent.com/92436863/231700862-e45dd8c7-3af0-417a-8bdd-85c38bd2b9d5.png)

1. 웹 프라우저에 www.naver.com을 입력했을 때, 먼저 Local DNS에 "www.naver.com"의 IP 주소 물어봄
없으면 Root DNS로

+) Root DNS : 도메인 네임 시스템의 루트 존

2. Root DNS에 네이버 정보 물어봄

3. Root DNS서버는 "com 도메인"을 관리하는 TLD(Top-Level Domain) 정보를 줌

+) TLD : 다음 레벨의 도메인 서버 / 예시는 .com을 관리하는 서버

4. TLD에 네이버 정보 물어봄

5. TLD에서 "naver.com" 관리하는 DNS 정보 전달

6. "naver.com" 도메인 관리 DNS 서버에 물어봄

7. Local DNS 서버에거 "www.naver.com" IP 주소 222.122.195.6 응답

8. Local DNS는 www.naver.com에 대한 IP 주소 캐싱 후 주소 전달

<br>

## Blocking & Non-Blocking

Blocking : 호출된 함수가 작업을 하는동안 호출한 함수에게 작업에 대한 제어권이 없는 상태로, 작업이 끝날 때까지 기다렸다가 자신의 작업을 시작하는 방식

Non-Blocking : 함수를 호출할 때 호출한 함수에게 바로 제어권을 건내주어 호출한 합수가 다른 일을 진행할 수 있는 방식

둘의 차이는 제어권의 유무

<br>

## Synchronous & Asynchronous

Synchronous : Synchronous 에서는 System Call이 끝나면 그때 결과물을 가져온다

Asynchronous : System Call이 완료되지 않아도 나중에 완료가 되면 그때 결과물을 가져온다. 주로 Callback 함수를 통해 결과물을 가져온다

순서의 차이