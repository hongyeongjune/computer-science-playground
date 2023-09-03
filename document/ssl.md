## SSL
* HTTP 통신규약과 함께 사용되어 HTTP 통신 간의 보안을 높여주는 기술
* SSL 은 보안 계층이라는 독립적인 프로토콜 계층을 만들어서 응용 계층과 전송 계층사이에 속하게 된다.
* SSL 은 TCP 기반의 프로토콜이기 때문에 TCP 연결의 3-way Handshake 와 SSL 연결의 3-way Handshake 를 수행하게 된다.
* Key (암호화 알고리즘)
    - 대칭키 = 비밀키
        - 송신자와 수신자가 같은 키로 암호화와 복호화를 진행
        - 하나의 키로 암호화하고 그와 같은 키로 복호화를 진행하기 때문에 대칭키라고한다.
        - 또한 이 키는 외부에 노출되면 안되기 때문에 비밀키라고도 한다.
    - 비대칭키 = 공개키
        - 송신자는 외부에 공개된 키(public key)로 암호화하여 송신하고 수신자는 개인키(private key)로 복호화한다.
        - 송신자와 수신자가 사용하는 키가 다르므로 비대칭키라고 한다.
* SSL 인증서
    - 공개키 방식은 대칭키를 배송하는 역할을 하고 대칭키로 전송하는 데이터의 암/복호화를 한다.
    - 클라이언트가 접속한 서버가 클라이언트가 의도한 서버가 맞는지를 보장하는 역할
    - 내용
        - 서비스의 정보
        - 서버 측 공개키
* CA(인증 기관)
    - SSL 인증서를 증명해주는 기관
    - 브라우저는 CA의 공개키를 처음부터 가지고 있다.
* 동작 방식
    - 웹 서버의 정보와 공개키를 인증기관(CA : Certificate Authority)으로 전송
    - 인증기관은 개인키(private key)를 가지고 웹 서버의 정보와 공개키를 암호화하고 웹 서버로 반환한다.
    - 클라이언트가 웹 브라우저로 사이트에 접속하면 웹 서버는 인증서를 보낸다. -> 인증서 : CA 가 개인 키로 암호화한 웹 서버의 정보와 공개 키
    - 브라우저는 이미 가지고 있는 인증기관의 공개키로 웹 서버한테 받은 웹 서버의 정보과 공개키를 복호화한다.
    - 브라우저는 요청할 데이터를 암호화할 대칭키를 생성하고 인증서에서 꺼낸 웹 서버의 공개키로 대칭키를 암호화하여 웹 서버로 전송
    - 웹 서버는 자신이 가지고 있는 개인키로 복호화하여 브라우저가 보낸 대칭키를 얻음
    - 이제 대칭키를 통해서 데이터를 암호화하여 주고받음
    - 정리
        - 실제 전송되는 데이터의 암호화는 대칭키
        - 키 교환에는 공개키 암호화를 사용
* SSL handshake (위의 동작방식과 같음)
  ![images](https://fascinated-game-c50.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F15c152b5-8cd0-4f2b-89d9-648a19c61ab0%2FUntitled.png?table=block&id=232b439d-efdb-4144-9bad-a51ea56093be&spaceId=388b68a4-8d73-4550-857a-eae96c4971c9&width=1870&userId=&cache=v2)
    - Client Hello
        - 브라우저는 Https 를 사용하는 것을 알게되면 client hello 를 한다.
        - 전달 목록
            - 사용 가능한 Cipher Suite 목록
                - SSL Protocol Version, 인증서 검정, 데이터 암호화 프로토콜, Hash 방식 등 Cipher Suite 알고리즘에 따라 암호화를 진행한다.
                - Cipher Suite 구성 예시
                    - Cipher Suite : TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
                    - TLS : 암호화 프로토콜
                    - ECDHE : 키 교환 방식
                    - RSA : 인증서 검증
                    - AES_128 : 대칭키를 이용한 블록 암호화 방식
                    - CBC : 블록 암호 운용방식
                    - SHA :메세지 인증
            - Session ID
                - 이전에 SSL 성공했다면 그 때 생성된 Session ID
            - SSL Protocol Version
            - Random Type
                - 브라우저가 순간적으로 생성한 임의의 난수
                - Replay Attack 방어 수단
                    - Replay Attack : 유효한 데이터 전송을 가로챈 후 반복하는 사이버 공격
    - Server Hello
        - 전달 목록
            - 브라우저의 암호화 방식 정보 중에서, 서버가 지원하고 선택한 방식(Cipher suite)
            - 인증서 전송 -> 인증서 : CA 가 개인 키로 암호화한 웹 서버의 정보와 공개 키
            - Random Type
                - 서버가 순간적으로 생성한 임의의 난수
                - Replay Attack 방어 수단
                    - Replay Attack : 유효한 데이터 전송을 가로챈 후 반복하는 사이버 공격
    - 서버 인증서 확인
        - 브라우저가 가지고 있던 CA 의 공개키로 복호화를 할 수 있다면 해당 서버는 CA 로부터 인증받음을 증명
    - Pre-master Secret 전송
        - 브라우저의 난수와 서버의 난수를 이용하여 Pre-master Secret 이라는 값을 생성하고, 이를 복호화한 웹 서버의 공개키로 암호화 (사실은 여기서 대칭키를 만드는게 아님)
    - Pre-master Secret 복호화
        - 웹 서버는 비밀 키로 브라우저가 보낸 값을 복호화하여 Pre-master Secret 값을 꺼내서 이 값을 Master Secret 이라는 값으로 저장한다.
        - 그리고 이것을 사용하여 Session Key 를 만드는데 이 키는 대칭 키 암호화에 사용될 키 이다.
        - 이 대칭 키로 브라우저와 서버 사이에 주고받는 데이터를 암/복호화 한다.
    - SSL handshake 종료
        - SSL handshake 가 정상적으로 완료되면, 이제 Session Key 를 사용하여 데이터를 주고받는다.
        - Https 통신이 완료되는 시점에 서로에게 공유된 Session Key 를 파기한다.
        - 만약 세션이 여전히 유지된다면 브라우저는 SSL handshake 요청이 아닌 Session ID 만 서버에게 알려주면 된다.