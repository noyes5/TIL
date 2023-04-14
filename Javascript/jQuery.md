# jQuery(제이쿼리)

> 자바스크립트로 만들어진 라이브러리로 DOM 조작, 이벤트 처리, 애니메이션, AJAX요청 등을 쉽게 사용할 수 있도록 지원

## 기능

- DOM 
  
예시코드
~~~html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>
        $(document).ready(function () {
            $("#myButton").click(function () {
                $("#myDiv").text("Button clicked!");
            });
        });
    </script>
    </body>
</head>
<body>
    <button id="myButton">Click me</button>
    <div id="myDiv">Hello, world!</div>
</html>
~~~
- AJAX

예시코드
~~~html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>
    <button id="loadData">Load Data</button>
    <div id="dataContainer"></div>

    <script>
        $(document).ready(function () {
            $("#loadData").click(function () {
                $.ajax({
                    url: "data.json",
                    dataType: "json",
                    success: function (data) {
                        $("#dataContainer").html(data.content);
                    }
                });
            });
        });
    </script>
</body>
</html>
~~~

- 애니메이션 효과
  
예시코드
~~~html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>
    <button id="animateButton">Animate</button>
    <div id="animateDiv" style="width: 100px; height: 100px; background-color: red;"></div>

    <script>
        // 버튼 클릭 시 자연스럽게 네모가 커지는 효과 
        $(document).ready(function () {
            $("#animateButton").click(function () {
                $("#animateDiv").animate({
                    width: "200px",
                    height: "200px",
                    backgroundColor: "blue"
                }, 1000);
            });
        });
    </script>
</body>
</html>
~~~

- 플러그인
   
   필요한 기능들을 미리 만들어 놓은 것을 가져와서 사용하는 것

## jQuery 사용 방법
1. 라이브러리 파일을 다운로드 받아서 프로젝트에 추가하여 작업
2. CDN 방식(외부 사이트에서 공유한 jQuery 라이브러리 주소를 추가해서 작업)


## 문법
- $() 형식으로 선택자와 동작(메소드) 정의
- 선택자로 요소 선택, 동작으로 해당 요소에 기능 적용

## 선택자

선택자를 사용하여 원하는 요소 선택

    $(객체): 객체 선택 
    $(*): 모든 DOM 요소에 적용
    $(”#id명”): id 속성으로 정의한 요소에 적용
    $(”class명”): class 속성으로 정의한 요소에 적용
    $(”태그명”): 해당 태그로 정의된 요소에 적용
    $(this): 현재 작업 중인 객체에 적용
    $(”선택자1 선택자2”): 선택자1의 하위 선택자2

## 특정 요소 선택 방법

    $("선택자1:first"): 선택자1 중 첫 번째 요소 선택
    $(”선택자1 선택자2:first"): 선택자1의 하위 선택자2 중 첫 번째 요소 선택
    $(”선택자1 선택자2:first-child"): 선택자1의 하위 선택자2 중 첫 번째 자식 노드 요소 선택
    $(”[속성명]”): 속성을 갖고 있는 요소 모두 선택
    $(”태그명[속성명=속성값]”): 정의된 태그의 속성명과 속성값이 일치하는 요소 선택
    $(”:input태그의 type속성”): 해당 타입으로 정의된 form 태그의 요소 선택

<code class="notranslate">first 와 first-child의 차이</code>

예시 코드
~~~html
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>
        $(document).ready(function(){
            $('.container span:first').css('color','red');
            $('.container2 span:first-child').css('color','skyblue');
        });
    </script>
</head>

<body>
    <div class="container">
        <ul>
            <ul>
                <li>
                    <span class="board_no">1</span>
                    <span class="title">제목1</span>
                    <span class="content">내용1</span>
                </li>
                <li>
                    <span class="board_no">2</span>
                    <span class="title">제목2</span>
                    <span class="content">내용2</span>
                </li>
                <li>
                    <span class="board_no">3</span>
                    <span class="title">제목3</span>
                    <span class="content">내용3</span>
                </li>
                <li>
                    <span class="board_no">4</span>
                    <span class="title">제목4</span>
                    <span class="content">내용4</span>
                </li>
            </ul>
        </ul>   
      </div>
      <div class="container2">
        <ul>
            <ul>
                <li>
                    <span class="board_no">1</span>
                    <span class="title">제목1</span>
                    <span class="content">내용1</span>
                </li>
                <li>
                    <span class="board_no">2</span>
                    <span class="title">제목2</span>
                    <span class="content">내용2</span>
                </li>
                <li>
                    <span class="board_no">3</span>
                    <span class="title">제목3</span>
                    <span class="content">내용3</span>
                </li>
                <li>
                    <span class="board_no">4</span>
                    <span class="title">제목4</span>
                    <span class="content">내용4</span>
                </li>
            </ul>
        </ul>   
      </div>
</body>
</html>
~~~
결과

![스크린샷 2023-08-15 오전 10 25 20](https://github.com/noyes5/java-lotto/assets/116651434/049e31f1-1002-466a-8f6c-d067ca595ac2)

- $(".container span:first-child")는 "container"클래스 중 첫번째 \<span> 요소만 선택하여 cs를 적용 
- $(".container span:first")는 "container"클래스 중 모든 첫번째 \<span> 요소에  적용됨


## EVENT
  on 메소드를 사용하여 이벤트 처리

    $(선택자).on(이벤트명, 함수): 이벤트 발생 시 함수 실행
    이벤트명 예시: click, keyup, change, mouseover 등

## 값 가져오기/설정하기

    양식태그 중 <input> 태그의 값 읽어오기
        val(): 값 읽어오는 getter

    <input> 태그에 값을 설정하기
        val(설정할값): 값을 설정하는 setter

    <div> 태그나 <span> 태그 내부 텍스트 추가
        text(추가할값): 텍스트 추가하는 setter

    <div> 태그나 <span> 태그 내부 텍스트 읽어오기
        text(): 텍스트 읽어오는 getter