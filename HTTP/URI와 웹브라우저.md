### URI(Uniform Resource Identifier)

URI? URL? URN?

URI ≒ URL + URN 이다.

URI ⊃ URL
URI ⊃ URN
URL ∩ URN = ∅

URI(Uniform Resource Identifier)

URL(Uniform Resource Locator) : 리소스가 있는 위치를 지정

URN(Uniform Resource Name) : 리소스에 이름을 부여

위치는 변할 수 있지만, 이름은 변하지 않는다.



URL 분석

https://www.google.com/search?1=hello&hl=ko

- scheme://[userinfo@]host[:port][/path][?query][#fragment]

- https://www.google.com:443/search?q=hello&hl=ko

스키마 : 프로토콜 사용

userinfo@는 유저 정보를 담아서 보내줘야 할때 사용하는데 거의 사용하지 않음.

포트 : 일반적으로 생략, http는 80 , https는 443 

path : 리소스가 있는 경로. 계층적 구조.

query : key=value 형태. ?로 시작하고 &로 추가가능. 보통 (쿼리)파라미터 혹은 쿼리 스트링이라고 불림.

fragment : 한 페이지에서 북마크 등을 사용할떄 사용(잘 사용하지 않음)


## 요청 흐름


+-----------------------------------+
| GET /search?q=hello&hl=ko HTTP/1.1|
| HOST : www.google.com             |
+-----------------------------------+