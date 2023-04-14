# BOM과 DOM

## BOM(Browser Object Model) 브라우저객체

> 브라우저 내에서 문서 이외의 요소를 객체로 관리하는 모델

### 주요 구성 요소
 
- window 객체 : 브라우저창을 대표하는 객체로, BOM의 최상위 객체

- navigator 객체 : 브라우저 종류나 버전 체크 등 확인하는 객체

- document 객체 : DOM을 조작하여 웹 페이지의 요소를 선택하고 조작할 수 있는 객체

- XMLHttpRequest 객체 : Ajax 요청을 보내고 받는데 사용되며, 비동기적으로 서버와 데이터 교환하여 웹페이지 업데이트에 사용하는 객체

- localStorage, sessionStorage : 클라이언트 측에서 데이터를 저장하고 유지하기 위해서 사용하는 객체

## DOM(Document Object Model) 

> HTML 문서의 모든 구성 요소를 객체로 정의하고 계층 구조로 관리하는 객체 모델

- 웹 페이지의 문서를 제어하기 위한 규칙을 표준으로 정해놓은 방법
- HTML 문서의 태그들을 객체화, 자바스크립트를 통해 동적으로 조작 가능

### 구성요소

    element: HTML 문서를 구성하는 컨텐츠(태그)
    text: 태그와 태그 사이에 입력한 문자열
    attribute: 태그 내부에 정의되어 있는 속성
    document: DOM 객체의 상위 객체
    node: 엘리먼트 1개
    nodeList: 엘리먼트 여러 개


### DOM API의 메소드

    querySelector: 선택자를 기준으로 DOM 객체를 반환
    querySelectorAll: 선택자를 기준으로 여러 개의 DOM 객체를 반환
    getElementById: id 속성값을 기준으로 반환
    getElementsByTagName: 태그명을 기준으로 모든 엘리먼트 반환
    getAttribute: 속성에 정의된 값 반환
    appendChild: 노드를 부모 노드의 마지막 자식으로 삽입
    inserBefore(새노드,기존 노드): 새 노드를 기존 노트 앞에 삽입
    createElement: 엘리먼트(태그 요소)를 생성
    createTextNode: 텍스트 노드를 생성
    setAttribute: 엘리먼트의 속성을 정의
    removeChild: 노드를 삭제

예시 코드
~~~html
<!DOCTYPE html>
<html>
<head>
    <title>DOM 예시</title>
</head>
<body>
    <h1 id="title" class="header">Hello DOM</h1>
    <p>This is a <span>sample</span> paragraph.</p>
    <a href="https://www.example.com" target="_blank">Visit Example</a>
    <ul>
        <li>Item 1</li>
        <li>Item 2</li>
        <li>Item 3</li>
    </ul>

    <script>
        // element: h1 요소를 선택
        const titleElement = document.getElementById("title");

        // text: p 요소의 텍스트 내용 선택
        const paragraphText = document.querySelector("p").textContent;

        // attribute: a 요소의 href 속성 값 선택
        const linkHref = document.querySelector("a").getAttribute("href");

        // document: document 객체는 이미 DOM의 최상위 객체

        // node: ul 요소 선택
        const ulNode = document.querySelector("ul");

        // nodeList: ul 아래의 모든 li 요소를 선택
        const liNodes = ulNode.querySelectorAll("li");

        console.log("titleElement:", titleElement);  // 결과 : <h1 id="title" class="header">Hello DOM</h1>
        console.log("paragraphText:", paragraphText); // 결과 : This is a sample paragraph.
        console.log("linkHref:", linkHref); // 결과 : https://www.example.com
        console.log("ulNode:", ulNode); // 결과 : <ul></ul> 내부부분이 반환
        console.log("liNodes:", liNodes); // 결과 : NodeList형태로 반환
    </script>
</body>
</html>
~~~


### DOM API의 속성

    textContent: 태그와 태그 사이의 문자열 반환
    childNodes: 모든 자식 노드를 NodeList 형태로 반환. 공백 포함.
    firstChild: 첫 번째 자식 노드 반환
    lastChild: 마지막 자식 노드 반환
    nodeName: 노드의 이름을 반환 (엘리먼트명과 동일 - 텍스트노드나 공백노드는 #text로 출력)