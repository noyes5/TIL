## URI(Uniform Resource Identifier)?

![noname](https://github.com/noyes5/TIL/assets/116651434/84591912-6acd-43cd-b5b5-faf41564223e)

URI(Uniform Resource Identifier)

URL(Uniform Resource Locator) : 리소스가 있는 위치를 지정

URN(Uniform Resource Name) : 리소스에 이름을 부여

위치는 변할 수 있지만, 이름은 변하지 않음



### URL 구조

- scheme://[userinfo@]host[:port][/path][?query][#fragment]

- https://www.google.com:443/search?q=hello&hl=ko

스키마 : 프로토콜 사용

userinfo@는 유저 정보를 담아서 보내줘야 할때 사용하는데 거의 사용하지 않음

호스트 : 도메인명 혹은 IP 주소 사용가능

포트 : 일반적으로 생략, http는 80 , https는 443 

path : 리소스가 있는 경로. 계층적 구조

query : key=value 형태. ?로 시작하고 &로 추가가능. 보통 (쿼리)파라미터 혹은 쿼리 스트링이라고 불림.

fragment : 한 페이지에서 북마크 등을 사용할때 사용(잘 사용하지 않음)


### 요청 흐름

1. IP랑 PORT 정보를 찾아 냄
2. HTTP 요청 메시지를 생성
   
        GET /search?q=hello&hl=ko HTTP/1.1
        HOST: www.google.com

3. SOCKET 라이브러리를 통해서 전달
    
        1. TCP/IP 연결(IP, PORT)
        2. 데이터 전달

4. HTTP메시지가 포함된 TCP/IP 패킷 생성

        출발지IP + 도착지IP + HTTP메시지

5. 네트워크 인터페이스를 통해 인터넷으로 나감
6. 서버가 패킷을 받으면 껍데기를 벗겨서 HTTP메시지를 읽음
7. 서버에서 HTTP 응답 메시지를 보냄
        
        HTTP/1.1 200 OK
        Content-Type: text/html;charset=UTF-8
        Content-Length: 3423
        <html>
            <body>...</body>
        </html>

8. 웹브라우저가 HTML 렌더링을 해서 화면을 보여줌