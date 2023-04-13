# jQuery(제이쿼리)

> 자바스크립트로 만들어진 라이브러리로 DOM 조작, 이벤트 처리, 애니메이션, AJAX요청 등을 쉽게 사용할 수 있도록 지원

## 기능

- DOM 
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

