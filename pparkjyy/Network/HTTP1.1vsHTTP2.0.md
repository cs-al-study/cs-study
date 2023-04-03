# HTTP 1.1 vs HTTP 2.0

<br>

![image](https://user-images.githubusercontent.com/92436863/229444218-3ac3d719-5a67-4768-97ed-87c78e8aff32.png)


## HTTP 1.1
- 기본적으로 Connection당 하나의 요청을 처리하도록 설계
- 동시 전송이 불가능하고 요청과 응답이 순차적으로 이뤄짐

## HTTP 1.x / 단점

### HOL (Head Of Line) Blocking - 특정 응답의 지연
- 패킷이 순서대로 도착해야하므로 패킷이 도착할때까지 그 이후 패킷은 전송되지 못하는 것

- Pipelining을 통해 해결
    - 요청에 대한 응답을 기다리지 않고 여러개의 요청을 보낸다.

### RTT (Round Trip Time) 증가
- 일반적으로 하나의 connection에 하나의 요청을 처리
- 매 요청별로 connection을 만들게 되고 TCP상에서 동작하는 HTTP의 특성상 3-way Handshake가 반복적으로 일어나 불필요한 RTT 증가

- Connection Keep-alive을 통해 해결
    - TCP 커넥션을 재사용하는 것

### 무거운 Header 구조 (특히 Cookie)

- HTTP 1.1은 다수의 http 요청이 발생할때마다 중복된 헤더값을 전송하게 됨
    - 쿠키 정보도 헤더에 담겨 요청되므로 헤더가 매우 무거워짐


<br>

## HTTP 2.0

### Multiplexed Streams
- 한 커넥션으로 동시에 여러 개의 메세지를 주고 받을수 있으며, 응답은 순서에 상관없이 stream으로 주고 받음

### Stream Prioritization
- 리소스간 의존관계(우선순위)를 설정하여 이런 문제를 해결

### Server Push
- 서버는 클라이언트의 요청에 대해 요청하지도 않은 리소스를 보냄

### Header Compression
- Header 정보를 압축하기위해 Header Table과 Huffman Encoding 기법을 사용하여 처리


<br>

## HTTP 3
- HTTP 1,2 가 TCP로 통신하는 것과는 달리 HTTP 3은 UDP 기반 QUIC 프로토콜을 사용하여 통신