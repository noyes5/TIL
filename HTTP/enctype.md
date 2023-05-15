# ectype 속성
- application/x-www-form-urlencoded : 모든 문자를 서버로 전송하기 전에 인코딩됨을 명시. 
form 데이터를 서버로 전송하는 기본값.

- multipart/form-data : 텍스트와 바이너리 데이터를 전송함을 명시. \<form>요소에 파일이나 이미지를 포함하여 전송할때 사용한다. Method는 반드시 post방식만

- text/plain
공백 문자(space)는 "+" 기호로 변환하지만, 나머지 문자는 모두 인코딩 하지 않음.