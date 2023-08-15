# HTTP 메시지

## HTTP 메시지 구조

|start-line 시작라인|
|:----------------|
|header 헤더|
|empty line 공백 라인 (CRLF)|
|message body|

## HTTP 요청 메시지
> 요청 메시지도 body 본문을 가질 수 있음

|GET /search?q=hello&hl=ko HTTP/1.1|
|:----------------|
|HOST: www.google.com|
|&nbsp;|
|&nbsp;|
        

### start-line

> request-line/ status-line

request-line = method SP(공백) request-target SP HTTP-version CRLF(엔터)

METHOD 종류: GET, POST, PUT, DELETE

    서버가 수행해야 할 동작 지정
    GET: 리소스 조회
    POST: 요청 내역 처리
    PUT: 리소스 생성 또는 업데이트
    DELETE: 리소스 삭제 요청

요청 대상(request-target)

    absolute-path[?query] (절대경로[?쿼리])
    절대경로 = "/"로 싲가하는 경로


## HTTP 응답 메시지

|HTTP/1.1 200 OK|
|:----------------|
|Content-Type: text/html;charset=UTF-8<br>Content-Length: 3423|
|&nbsp;|
|\<html><br> &nbsp;\<body>....\</body><br>\<html>|

### start-line

> request-line/ status-line

status-line = HTTP-version SP status-code SP reasonPharse CRLF

HTTP 상태코드(status-code): 요청 성공, 실패를 나타냄

- 200: 성공
- 400: 클라이언트 요청 오류
- 500: 서버 내부 오류

이유문구(reasonPharse): 사람이 이해할 수 있는 짧은 상태 코드 설명 글

### header-field

 > field-name ":" OWS field-value OWS (OWS: 띄어쓰기 허용)

용도 HTTP 전송에 필요한 모든 부가 정보

    ex) 메시지 바디의 내용, 바디의 크기, 압축, 인증, 요청 클라이언트 정보, 서버 애플리케이션 정보, 캐시 정보 등등....

### message body

    실제 전송할 데이터
    HTML문서, 이미지, 영상, JSON 등 byte로 표현할 수 있는 모든 데이터 전송 가능