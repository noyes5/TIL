# AJAX(Asynchronous Javascript and XML)

> 자바스크립트의 라이브러리중 하나로, XMLHttpRequest 객체를 이용하여 비동기통신(원하는 부분만 로드)하는 기법

HTTP 프로토콜은 단방향 통신이기 때문에 클라이언트에서 REQUEST를 보내고, 서버에서 RESPONSE하면 연결이 끊어진다.

이 경우 데이터를 다시 받으려면 페이지 전체를 갱신해야해서 리소스와 시간을 많이 들게 한다. 
이럴때 Ajax를 통해 일부만 갱신하도록 하여 필요한 데이터만 받기에 리소스와 시간을 아낄수 있다.

---

## 예시 코드

exam.js
```js
$.ajax({
url: "/erp/ajax/gugu", // 요청이 전송될 URL 주소
type: "GET",    // http요청방식
data: {key : value}, // 요청 시 보내는 데이터
dataType : 'json', // 응답데이터 형식(명시하지 않으면 자동 추측)
success: function (data) {
    // ajax로 요청하는 경우 response되는 데이터는 무조건 success에서
    // 실행되는 함수 내부에서만 사용할 수 있다.
    $("#result2").html(data);
},
error: function (obj, msg, statusMsg) {},
});

```
- url로 요청을 보내고 데이터를 받아올 수 있다.

- success 했을 때와 error 일 때의 분기를 나눠서 함수를 적어야 한다.

    success에서 받는 매개변수 (data, textStatus, jqXHR)
    
    - data : 서버로부터 전달받은 응답 데이터를 의미
    - textStatus : 주로 "success"값 전달
    - jqXHR : jQuery XMLHttpRequest 객체!이며, 요청을 취소하거나 응답 상태확인이 가능하다. 단, 서버에는 이미 응답이 된 상태고, 클라이언트에게만 보여지지 않는다.

    error에서 받는 매개변수 (jqXHR, textStatus, errorThrown)
    - jqXHR : 생략
    - textStatus : 주로 "error"값 전달
    - errorThrown : 에러에 대한 추가 정보를 가져오는 문자열

