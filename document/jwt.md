## 목차

<!-- 목차 -->
-   [목차](#목차)
-   [JWT](#jwt)
-   [JWT 사용 이유](#jwt-사용-이유)
-   [JWT 주의점](#jwt-주의점)
<!-- /목차 -->

## JWT
* Json Web Token 의 약자
* json 형식의 데이터를 토큰화하여 호스트끼리 데이터를 교류하는 기술
* JWT 는 헤더, 페이로드, 시그니처로 나뉘어져있다.
    - 헤더 : 시그니처를 해싱하기 위한 알고리즘을 지정하는 곳
        - typ : 토큰 타입 지정 / jwt
        - alg : 해싱 알고리즘 지정
    - 페이로드 : 송신측에서 전송할 데이터를 클레임 단위로 담고 있다.
    - 시그니처 : 헤더와 페이로드를 Base64 로 인코딩한 값을 합친 후 비밀 키로 해싱한 부분
        - 해싱은 헤더에 지정된 알고리즘으로 함
* 헤더와 페이로드 모두 Base64 로 인코딩되기 때문에 누군가 토큰을 탈취한다면 페이로드의 값을 읽을 수 있기 때문에 JWE 를 통해 암호화를 하거나 페이로드에 중요한 데이터를 넣으면 안된다.
* 헤더와 페이로드를 시크릿 키로 해시한 값이 시그니처이기 때문에 시크릿 키가 유출되지 않았다면 누군가 탈취한 데이터를 변형해서 보낸다고해도 문제가 되지 않는다.

## JWT 사용 이유
* JWT 는 토큰 자체에 데이터를 가지고 있다는 장점이 있다.
* 즉, 클라이언트의 정보를 다른 작업 없이 토큰에서 가져올 수 있다.
* 권한을 인증하는 방법이 서버, 서비스마다 다르다면 이후 scale-out 을 할 때 고려해야할 요소가 많아지지만, JWT 를 사용하고 권한 인증을 통일화한다면 같은 Secret Key 를 가지고 있는 서버는 모두 권한 인증을 할 수 있기 때문에 편리하다.

## JWT 주의점
* 토큰의 길이
    - 페이로드는 클레임 단위로 저장하는데, 각 데이터는 Base64 로 인코딩된 문자열이다.
    - 담은 데이터가 많을수록 페이로드의 길이가 길어지고, 단순한 request 보다 토큰의 길이가 더 길어지는 오버헤드가 발생할 수 있다.
* 보안
    - 헤더와 페이로드 모두 단순 Base64 로 인코딩된 문자열이다.
    - 따라서 토큰을 누군가가 탈취한다면 페이로드를 볼 수 있는 단점이 있다.
    - 따라서 페이로드에 중요한 데이터를 넣지 않는 방법을 사용하거나, JWE 를 통해 보안을 강화함으로써 사용할 수 있다.

## 쿠키 vs 세션
* 쿠키는 브라우저에서, 세션은 서버에서 관리
* 쿠키는 보안에 취약하고, 세션은 쿠키에 비해 보안이 높으나 서버에서 생성하여 관리하므로 서버에 부담이 간다.
* 쿠키는 Cookie Injection 문제 때문에 보안에 취약하다 그래서 세션 방식이 나온 것
* 세션은 서버에서 정보를 관리하기 때문에 확장성이 떨어진다.
* 해결책
    - JWT