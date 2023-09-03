## Http Version
* HTTP/0.9
    - 아주 단순하게 GET 통신만 가능
    - 헤더가 존재하지 않기 때문에 전송은 HTML 문서로만 가능하고 다른 유형은 전송할 수 없다.
* HTTP/1.0
    - 상태코드가 응답 값 시작 부분에 포함
    - 헤더가 요청과 응답 모두에 추가되어 프로토콜의 확장이 가능해졌다.
    - Content-Type 의 도움으로 HTML 파일 이외에 다른 문서들도 전송이 가능해짐
    - POST, HEAD 메서드가 추가되었다.
    - Connection 하나로 요청과 응답 각각 하나씩만 처리할 수 있다. -> 매번 새로운 요청마다 커넥션을 새로 해야하기 때문에 비용이 증가한다.
* HTTP/1.1
    - HTTP 의 첫 번째 표준 버전으로 OPTION, PUT, DELETE, TRACE 메서드가 추가되었다.
    - Persistent Connection
        - 요청과 응답이 끝나면 Connection 을 종료하지 않고 일정 시간(timeout) 동안 커넥션을 닫지 않는 방삭
    - Pipelining
        - 하나의 커넥션에서 응답을 기다리지않고 요청들만 먼저 보낸 후 그 순서에 맞춰 응답을 받는 방식
        - head of line blocking 문제 발생
            - A,B,C 요청을 보냈고 A 요청의 응답 시간은 100초, B 요청의 응답 시간은 2초라고 가정하자
            - B 요청은 빠르게 처리해서 응답할 수 있지만 A 요청이 오래걸리기 때문에 계속 기다리는 현상
    - Header 구조의 중복
        - 연속된 요청은 Header 가 중복되는 경우가 많은데, 그대로 전송한다.
* HTTP/2
  ![images](https://media.vlpt.us/images/taesunny/post/eddc9c22-7d46-4899-877c-f8ce751609d5/image.png)
  ![images](https://media.vlpt.us/images/taesunny/post/17fd473d-7e43-4e73-9bba-8f64ee3ef21d/image.png)
    - 메세지 전송 방식이 기존에 text 형식으로 주고 받았던 방식 말고, 바이너리 포맷으로 인코딩된 계층을 사용한다.
    - Stream : 구성된 연결 내에서 전달되는 바이트의 양방향 흐름, 하나 이상의 메시지가 전달 가능하다.
    - Message : 논리적 요청 또는 응답 메시지에 매핑되는 프레임의 전체 시퀀스이다.
    - Frame
        - HTTP/2에서 통신의 최소 단위.
        - 각 최소 단위에는 하나의 프레임 헤더가 포함된다.
        - HEADERS Type Frame, DATA Type Frame 이 존재한다.
    - HOL Blocking, head of line blocking 의 해결
      ![images](https://media.vlpt.us/images/taesunny/post/8ba0ec32-1e59-4ffc-a801-21502f44e8a4/image.png)
        - Multiplexing 가능
            - 하나의 Connection 으로 동시에 여러 개의 메세지를 주고 받을 수 있다.
        - Http/1.1 까지는 한번에 하나의 파일만 전송이 가능했지만, Http/2 는 여러 파일을 한번에 병렬 전송한다.
        - 하나의 연결 내의 여러 스트림을 병렬로 처리한다.
        - Http 메세지를 독립된 프레임으로 세분화하고 이 프레임을 인터리빙한 다음, 클라이언트에서 다시 조립하는 기능
    - Stream Prioritization
        - 응답에 대한 우선순위를 정해 우선순위가 높을수록 응답을 빨리 한다.
    - Server Push
      ![images](https://developers.google.com/web/fundamentals/performance/http2/images/push01.svg?hl=ko)
        - 서버가 단일 클라이언트 요청에 대해 여러 응답을 보낼 수 있는 것
        - 위 그림을 토대로 하나의 html 요청안에 css 와 jpg 파일이 있다고 가정하자.
        - 기존에는 html 요청을 하고 다시 css, jpg 를 요청해야했지만, 이제는 서버가 알아서 css, jpg 도 같이 응답해주는 것을 말함
    - Header Compression (헤더 압축)
      ![images](https://developers.google.com/web/fundamentals/performance/http2/images/header_compression01.svg?hl=ko)
        - 기존 헤더의 중복 문제를 해결함
        - 전송되는 헤더 필드를 정적 Huffman Encoding 을 사용하여 크기를 줄인다.
        - Header 에 중복 값이 존재하는 경우 정적 테이블/동적 테이블 개념을 사용하여 중복 header 를 검출하고 중복된 header 는 index 값만 전송하고 중복되지 않은 header 는 huffman encoding 을 사용하여 전송한다.
        - 정적 테이블
            - 모든 연결에 사용될 가능성이 있는 공용 HTTP 헤더 필드 제공
        - 동적 테이블
            - 처음에는 빈 공간이고, 특정 연결에서 교환되는 값에 따라 업데이트된다.
        - Huffman Encoding
            - 주어진 문자열을 트리를 통해 2진수로 압축하는 알고리즘
* HTTP/3
    - UDP 를 기반으로 하는 QUIC 을 프로토콜로 사용한다.
    - 연결 설정 시 지연시간 감소
        - QUIC 는 TCP 를 사용하지 않기 때문에 3-way handshake 과정을 거치지 않는다.
        - TCP 는 연결을 생성하기 위해 1RTT 가 필요하고, TLS(=SSL)을 사용한 암호화까지 하려면 TLS 의 handshake 도 더해져 3RTT 가 필요하다.
        - 반면 QUIC 는 첫 연결 설정에 1RTT 가 소요된다. -> handshake 를 할 때 필요한 정보와 데이터도 함께 보냄으로서 가능해짐
        - TCP+TLS 는 데이터를 보내기 전에 신뢰성있는 연결과 암호화에 필요한 정보를 교환하고 유효성을 검사한 뒤 데이터를 교환하지만, QUIC 는 바로 데이터부터 보낸다.
        - 또한, 클라이언트가 서버로 첫 요청을 보낼 때는 서버의 Connection ID 를 사용하여 특별한 키인 Initial Key 를 생성한 후 통신을 암호화 한다.
        - 그리고 한 번 연결에 성공하면 서버는 그 설정을 캐싱하고 있다가 다음 연결 때는 캐싱해놓은 설정을 사용하여 바로 연결을 성립시키기 때문에 0RTT 로 통신이 가능하다.
        - 그리고 Connection ID 를 통해 서버와 연결을 생성하기 때문에 클라이언트의 IP 와 전혀 무관한 데이터라서 클라이언트의 IP 가 변경되더라도 기존의 연결을 계속 유지할 수 있다.
            - Connection ID 는 고유한 랜덤 값
    - 독립 스트림을 사용하여 향상된 멀티 플렉싱을 제공한다.
        - TCP 자체에 HOL Blocking 문제를 발견
        - 하나의 커넥션 내에서 여러 스트림을 병렬로 처리하는데 어떤 스트림의 데이터가 손실되면 병렬러 처리하던 다른 스트림도 대기 해야한다. -> 재조립을 해야돼서
        - 하지만, Quic 은 하나의 커넥션에 하나의 스트림만 허용한다.


