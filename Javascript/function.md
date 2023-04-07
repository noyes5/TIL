# 자바스크립트 함수(Function)
## 함수의 선언과 호출
~~~js
함수 선언: function functionName(parameters) { // code }
함수 호출: functionName(arguments);
~~~

자바스크립트에서 선언되는 함수들은 선언 시 호이스팅 됨.

BUT 아래와 같은 <code class="notranslate">함수 표현식</code>은 호이스팅 되지 않음.

예시코드
~~~js
sayHello(); // 에러: sayHello is not a function

var sayHello = function() {
    console.log("Hello!");
};
~~~

<code class="notranslate">호이스팅이란? 자바스크립트 엔진이 코드를 해석하고 실행하기 전에 변수 및 함수 선언을 먼저 처리하는 것.</code>


### 변수의 종류
~~~
var로 선언된 변수 : 호이스팅 되어 선언되며(할당 X), 중복선언 가능
let으로 선언된 변수 : 블록 스코프 내에서만 유효. 재할당 가능
const로 선언된 변수 : 상수. 재할당 불가능
~~~
> let과 const는 ECMAScript6(이하 ES6)이후 버전부터 사용가능


- var
~~~js
var x = 5;
if (true) {
    var x = 10;
    console.log(x); // 출력: 10
}
console.log(x); // 출력: 10 
~~~
블록 스코프 개념이 없으므로 x에 10이 할당 됨

- let
~~~js
let y = 5;
if (true) {
    let y = 10;
    console.log(y); // 출력: 10
}
console.log(y); // 출력: 5 (블록 스코프로 인해 변수가 격리됨)
~~~
if 블록 내부에서 선언된 y변수는 블록종료시 사라짐

- const
~~~js
const pi = 3.14159; 

console.log(pi); // 출력: 3.14159

// pi = 3.1; // 재할당 시도 (오류 발생)
// TypeError: Assignment to constant variable.
~~~
한 번 선언된 pi 변수는 재할당 시 타입에러 발생