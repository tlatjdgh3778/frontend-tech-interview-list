# 1편

* [브라우저의 렌더링 과정에 대해서 설명](#-브라우저의-렌더링-과정에-대해서-설명)
* [브라우저 저장소(local storage, session storage, 쿠키)](#브라우저-저장소local-storage-session-storage-쿠키)
* [This의 용법 아는대로 설명](This의-용법-아는대로-설명)
* [이벤트 버블링, 이벤트 캡처링](이벤트-버블링-이벤트-캡처링)
* [비동기 처리에 대한 설명(Callback, Promise, async await)](비동기-처리에-대한-설명Callback-Promise-async-await)
* [클로저에 대해 설명](클로저에-대해-설명)

## 브라우저의 렌더링 과정에 대해서 설명
<p align='center'><img src="https://davidhwang.netlify.app/static/4ec9d46ea98033d0bf8d5c6966ba0462/d19c0/browser.png" /></p>

브라우저가 렌더링 되는 과정

* 사용자가 사용자 인터페이스의 주소표시줄에 URI를 입력하여 브라우저 엔진에 전달한다.
* 브라우저 엔진은 먼저 자료 저장소에서 전달된 URI에 대한 정보를 찾고, 있다면 해당 데이터를 렌더링 엔진으로 전달한다.
  * 없으면 렌더링 엔진 - 통신 레이어로 전달 후 통신 레이어가 서버에 요청해서 해당하는 정보를 받아온다.
* 렌더링 엔진은 통신 레이어에서 받거나, 자료 저장소에서 받아온 HTML, CSS를 파싱한다
  * HTML을 파싱하여 DOM tree 생성
  * CSS를 파싱하여 CSSOM 생성
* JavaScript파일은 JavaScript 해석기가 파싱한다.
* JavaScript 해석기는 파싱한 결과를 렌더링 엔진에 전달하여 만들어진 DOM tree를 조작한다.
* 조작이 완료된 DOM Node(DOM tree안에 있는 요소)는 render ojbect(render tree안에 있는 요소)로 변한다.
* UI 백엔드가 render object를 브라우저 렌더링 화면에 띄워준다.

## 브라우저 저장소(local storage, session storage, 쿠키)
### Web Storage
웹 스토리지는 서버가 아닌 클라이언트에 데이터를 저장할 수 있도록 하는 HTML5의 새로운 기능이다.
쿠키는 약 4KB의 데이터를 저장할 수 있는 반면에 웹 스토리지는 5MB까지 저장이 가능하다.

웹 스토리지의 개념은 **키/값** 쌍으로 데이터를 저장하고, **키를 기반으로 데이터를 조회**하는 패턴이다. **영구저장소(Local Storage)와 임시저장소(SessionStorage)**를 따로 두어 데이터의 지속성을 구분할 수 있다

### 쿠키와 웹 스토리지의 비교
* **쿠키는 매번 서버로 전송된다.**
  * 쿠키를 설정하면 이후의 모든 웹 요청은 쿠키정보를 포함해서 서버로 전송된다.
  * 웹 스토리지는 저장된 데이터가 클라이언트에 존재할 뿐 서버로 전송되지는 않는다.
* **웹 스토리지는 단순 문자열을 넘어서 객체정보를 저장할 수 있다.**
* **웹 스토리지는 용량의 제한이 없다.**
  * 하나의 사이트에서 최대 쿠키 수는 20개이고, 크기는 4KB로 제한되어 있다.
* **웹 스토리지는 영구 데이터 저장이 가능하다.**
  * 쿠키는 만료일자를 지정하게 되어있어서 언젠가는 제거된다. 만료일자를 지정하지 않으면 세션 쿠키가 되고, 영구적인 쿠키를 원한다면 만료일자를 엄청 멀게 설정하면 된다.
  * 웹 스토리지는 만료기간의 설정이 없다. 즉, 한 번 저장한 데이터는 영구적으로 존재한다.
  
### 로컬 스토리지
* window.localStorage
* 브라우저를 종료해도 데이터는 유지된다. 명시적으로 지우지 않는 이상 영구적으로 저장이 가능하다.
* 도메인별로 생성되며, 다른 도메인의 로컬 스토리지에는 접근이 불가능하다.
* 서로 다른 브라우저 탭이라도 동일한 도메인이라면 동일한 로컬 스토리지를 사용한다.
* 지속적으로 필요한 정보를 저장하기에 좋다. (ex. 자동 로그인)

### 세션 스토리지
* window.sessionStorage
* 탭/윈도우 단위로 세션 스토리지가 생성된다.
* 즉, window 객체와 동일한 유효 범위 및 생존 기간을 가지며, 탭/윈도우를 닫을 시 데이터가 삭제된다.
* 동일한 탭/윈도우라도 다른 도메인이라면 또 다른 세션 스토리지가 생성된다.
* 잠시 동안 필요한 정보를 저장하기에 적합하다. (ex. 입력 폼 저장, 일회성 로그인)

## This의 용법 아는대로 설명
자바스크립트는 함수 호출 방식에 따라서 this에 바인딩 할 객체가 동적으로 결정된다.
함수를 선언할 때 this에 바인딩 할 객체가 정적으로 결정되는 것이 아니고, **함수를 호출할 때 함수가 어떻게 호출되었는지**에 따라서 this에 바인딩 할 객체가 동적으로 결정된다.

* **함수 호출**
* **메소드 호출**
* **생성자 함수 호출**
* **apply/call/bind 호출**
* **화살표 함수**

### 함수 호출
기본적으로 this는 전역 객체에 바인딩 된다. 전역 함수는 물론 내부 함수의 경우도 this는 전역 객체에 바인딩 된다.
```js
function foo() {
	console.log("foo's this: ", this); // window
  function bar() {
  	console.log("bar's this: ", this); // window 
  }
  bar();
}
foo();
```

콜백 함수의 경우에도 this는 전역 객체에 바인딩 된다.
```js
var value = 1;

var obj = {
  value: 100,
  foo: function () {
    setTimeout(function () {
      console.log("callback's this: ", this); // window
      console.log("callback's this.value: ", this.value); // 1
    }, 100);
  },
};

obj.foo();
```

### 메소드 호출
메소드 호출 시에는 해당 메소드를 호출한 객체에 바인딩 된다.
```js
function foo() {
  this.check = function () {
    console.log("this is", this);
  };
}

var f = new foo();
f.check(); // this is foo {check: ƒ}
```

### 생성자 함수 호출
자바스크립트의 생성자 함수는 객체를 생성하는 역할을 한다. 기존 함수에 new를 붙여서 호출하면 해당 함수는 생성자 함수로 동작한다.

일반 함수에 new를 붙여서 호출해돋 생성자 함수처럼 동작할 수 있기 때문에 일반적으로 생성자 함수는 첫 글자를 대문자로 한다.

생성자 함수가 생성하는 객체로 this가 바인딩 된다.
```js
function Person(name) {
  this.name = name;
}

var kim = new Person("kim");

console.log(kim.name); // {name: kim}
```

### apply/call/bind 호출
this에 바인딩 되는 객체는 함수가 어떻게 호출되는지에 따라 자바스크립트 엔진이 결정하는데, 이러한 방식 말고 this를 특정 객체에 명시적으로 바인딩하는 방법이 apply, call이다.

```js
var Person = function (name) {
  this.name = name;
};

var foo = {};

// apply 메소드는 생성자함수 Person을 호출한다. 이때 this에 객체 foo를 바인딩한다.
Person.apply(foo, ['name']);
console.log(foo); // { name: 'name' }

// call()
Person.call(foo, 'name')
console.log(foo) // { name: 'name' }

// bind()
Person.bind(foo, 'name')()
console.log(foo)  // { name: 'name' }

```

apply의 경우는 두 번째 매개변수를 배열 형태(또는 유사배열 객체)로 넣는다는 차이점 빼고는 call이랑 동일하다.

bind는 함수에 인자로 전달한 this가 새로운 함수를 리턴한다. apply, call과 같이 함수를 실행하지는 않기 때문에 명시적으로 함수를 호출할 필요가 있다.

## 이벤트 버블링, 이벤트 캡처링
### 이벤트 버블링
**이벤트 버블링**이란 한 요소에 이벤트가 발생하면 이 요소에 할당된 핸들러가 동작하고, 이어서 부모 요소의 핸들러, 최상단의 부모 요소를 만날 때까지 반복되면서 핸들러가 동작하는 현상을 말한다.

### 이벤트 캡처링
**이벤트 캡처링**은 버블링과는 반대로 최상단에서 해당 태그를 찾아 내려간다.
addEventListener의 옵션 객체에 { capture: true }또는 true를 설정해주면 캡처링을 구현할 수 있다.

더욱 자세한 설명은 여기
[이벤트 버블링과 캡처링](https://velog.io/@tlatjdgh3778/%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%B2%84%EB%B8%94%EB%A7%81%EA%B3%BC-%EC%BA%A1%EC%B2%98%EB%A7%81%EC%97%90-%EB%8C%80%ED%95%9C-%EC%A0%95%EB%A6%AC)

## 비동기 처리에 대한 설명(Callback, Promise, async await)
비동기 처리란 특정 코드의 연산이 끝날 때까지 코드의 실행을 멈추지 않고 다음 코드를 먼저 실행하는 것을 말한다.

### Callback 
콜백 함수로 비동기 처리를 할 수 있다.

```js
console.log("Hello");
setTimeout(function () {
  console.log("Bye");
}, 3000);
console.log("Hello Again");
```

콜백 함수를 익명함수로 전달하는 과정이 반복되어 코드의 들여쓰기 수준이 늘어남에 따라서 **콜백 지옥** 현상이 발생하는 문제점이 있다.
```js
setTimeout(
  function (name) {
    let coffeeList = name;
    console.log(name);

    setTimeout(
      function (name) {
        coffeeList += ", " + name;
        console.log(name);

        setTimeout(
          function (name) {
            coffeeList += ", " + name;
            console.log(name);

            setTimeout(
              function (name) {
                coffeeList += ", " + name;
                console.log(name);
              },
              500,
              "카페라떼"
            );
          },
          500,
          "카페모카"
        );
      },
      500,
      "아메리카노"
    );
  },
  500,
  "에스프레소"
);
// 에스프레소
// 에스프레소, 아메리카노
// 에스프레소, 아메리카노, 카페모카
// 에스프레소, 아메리카노, 카페모카, 카페라떼
```

이를 해결하기 위해서 ES6에서 Promise가 도입되었다.

### Promise
```js
new Promise(executor);
```

Promise 객체는 new 키워드와 생성자를 사용해서 만든다. 생성자는 매개변수로 executor라는 콜백 함수를 받는데 이 콜백 함수는 인자로 resolve, reject함수를 인자로 받는다.
```js
const myFirstPromise = new Promise((resolve, reject) => {
  // do something asynchronous which eventually calls either:
  //
  //   resolve(someValue)        // fulfilled
  // or
  //   reject("failure reason")  // rejected
});
```
resolve 함수는 비동기 작업을 성공적으로 완료해 결과를 값으로 반환할 때 호출하고
reject 함수는 작업이 실패하여 오류의 원인을 반환할 때 호출하면 된다.

resolve, reject 의 처리 결과 모두 **후속 처리 메소드**로 전달한다.

#### 후속 처리 메소드
Promise 객체의 상태에 따라 후속 처리 메소드를 호출하게 된다.
```js
promise
  .then((value) => {
    console.log(value);
  })
  .catch((error) => {
    console.log(error);
  })
  .finally(() => {
    console.log("finally");
  });
```

* then() 메소드는 두 개의 콜백 함수를 인자로 받는다. 
```js
.then(onFulfilled, onRejected);
```
첫 번째 콜백 함수는 resolve함수가 호출되면 호출되고, 두 번재 콜백 함수는 reject함수가 호출되면 호출된다.

* catch() 메소드는 예외(비동기 처리 또는 then 메소드에서 발생한 에러)가 발생하면 호출된다.
```js
.catch(onRejected);
```

* finally() 메소드는 Promise가 처리되면 상태에 상관없이 지정된 콜백 함수가 실행된다.
```js
.finally(onFinally);
```

에러 처리는 then의 두 번째 콜백 함수 또는 catch로 에러 핸들링이 가능하지만 catch로 하는 것이 더 좋다

그 이유는 then으로 에러 핸들링을 하게되면 then의 첫 번째 콜백 함수에서 발생하는 에러는 잘 잡아내지 못하기 때문이다.

### Async/Await
async/await는 ES2017(ES8)에서 추가된 Promise를 더욱 쉽게 사용할 수 있도록 하는 문법이다.

#### async
async함수는 function 앞에 위치하고 해당 함수는 항상 Promise를 반환한다.
```js
async function f() {
	return 1;
}

f().then((value) => console.log(value)); // 1
```

#### await
자바스크립트는 await키워드를 만나면 프로미스가 처리될 떄까지 기다린다. 결과는 그 이후 반환된다. 
await은 async 키워드를 사용한 함수에서만 사용이 가능하다.
```js
async function f() {

  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("완료!"), 1000)
  });

  let result = await promise; // 프로미스가 이행될 때까지 기다림 (*)

  console.log(result); // 1초후 "완료!"
}

f();
```
함수를 호출하고 실행되는 도중에 `let result = await promise;` 부분에서 실행이 잠시 중단 되었다가 프로미스가 처리되면 실행이 재개된다. 이 때 프로미스 객체의 result 값이 변수에 할당된다.

프로미스가 처리되길 기다리는 동안에는 엔진이 다른 일(다른 스크립트 실행, 이벤트 처리 등)을 할 수 있기 때문에 CPU 리소스가 낭비되지 않는다.


#### async/await은 promise보다 간결하고 깔끔한 코드 작성이 가능하다.
```js
// promise 연속 호출
function getData() {
    return promise1()
        .then(response => {
            return response;
        })
        .then(response2 => {
            return response2;
        })
        .catch(err => {
            //TODO: error handling
            // 에러가 어디서 발생했는지 알기 어렵다.
        });
}

// async / await 연속 호출
async function getData() {
    const response = await promise1();
    const response2 = await promise2(response);
    return response2;
}
```

## 클로저에 대해 설명
클로저는 함수와 함수가 선언된 어휘적 환경(Lexical environment)의 조합이다.
흔히 함수 내에서 함수를 정의하고 사용하면 클로저라고 한다.

먼저 자바스크립트가 어떻게 변수의 유효 범위를 지정하는지를 알아보자.

#### 렉시컬 스코프
함수가 중첩되어 있을 때, 내부 함수에 찾는 식별자가 없으면 스코프 체인으로 상위 스코프에서 식별자를 찾아 나간다.
```js
var x = 1;

function foo() {
  var x = 10;
  bar();
}

function bar() {
  console.log(x);
}

foo(); // ?
bar(); // ?
```

bar()에는 x가 정의되어 있지 않기 때문에 스코프 체인에 의해서 상위 스코프로 이동하면서 x가 어디에 선언되어 있는지 확인한다.
bar()의 상위 스코프가 foo()라면 x는 10이 될 것이고, 상위 스코프가 전역이라면 x는 1이 될 것이다.

자바스크립트는 함수를 어디서 선언했는지에 따라 상위 스코프를 결정하는 방식인 **렉시컬 스코프**(또는 **정적 스코프**) 를 따른다.

즉 어디서 선언했는지에 따라 결정이 되므로 bar()의 상위 스코프는 전역 스코프이고 x의 값은 1이 된다.

#### 클로저
> 함수가 속한 렉시컬 스코프를 기억하여 함수가 렉시컬 스코프 밖에서 실행될 때에도 이 스코프에 접근할 수 있는데, 이 때 함수가 접근할 수 있는 렉시컬 스코프를 클로저라고 부른다.

```js
function outter() {
  var title = "coding everybody";
  return function () {
    console.log(title);
  };
}
var inner = outter();
inner();
```

`outter` 라는 외부 함수를 실행한 결과(`return`)는 `inner` 변수에 담긴다. 변수에 담겨있는 함수(`function() { console.log(title); }`) 를 호출하면 `coding everybody` 가 출력된다.

여기서 이상한 점은 `inner` 변수에 담긴 함수를 호출할 때 `outter` 함수는 이미 생을 마감하고 종료되었는데도 불구하고 `inner`가 외부함수 `outter`에 존재하는 `title`에 접근하고 있다는 것이다.

반환된 익명함수 `function() { console.log(title); }` 를 클로저라고 한다.

#### 클로저의 활용
* **정보 은닉**
```js
function factory_movie(title) {
  return {
    get_title: function () {
      return title;
    },
    set_title: function (_title) {
      title = _title;
    },
  };
}
ghost = factory_movie("Ghost in the shell");
matrix = factory_movie("Matrix");

console.log(ghost.get_title());
console.log(matrix.get_title());

ghost.set_title("공각기동대");

console.log(ghost.get_title());
console.log(matrix.get_title());

// Ghost in the shell
// Matrix
// 공각기동대
// Matrix
```

위의 코드를 통해 알 수 있는 사실들이 있다.
1. 클로저는 객체의 메소드에서도 사용할 수 있다. 위의 코드는 `get_title`과 `set_title`메소드를 가진 객체를 반환하고 있다. 이 메소드들은 외부함수인 `factory_movie`의 인자값으로 전달된 지역변수 `title`을 사용하고 있다.
2. 동일한 외부함수 안에서 만들어진 내부함수나 메소드는 외부함수의 지역변수를 공유한다. `ghost.set_title('공각기동대');` 의 코드로 지역변수 `title`을 `공각기동대` 로 변경했다.
두 번째 `console.log(ghost.get_title());` 의 값이 `공각기동대` 인 이유는 `set_title`과 `get_title` 메소드가 지역변수 `title`의 값을 공유하고 있다는 뜻이다.
3. 똑같은 외부함수 `factory_movie` 를 공유하고 있는 `ghost`와 `matrix`의 `get_title` 값이 다른 이유는 외부함수가 실행될 때마다 새로운 지역변수를 포함하는 클로저가 생성되기 때문에 `ghost`와 `matrix`는 서로 완전히 독립된 개체가 되기 때문이다.
4. `factory_movie`의 지역변수 `title`의 값을 읽고 수정할 수 있는 것은 `factory_movie` 메소드를 통해서 만들어진 객체 뿐이다.
5. `factory_movie` 가 어떠한 값을 리턴했을 때 그 함수는 생이 마감되었기 때문에 지역변수인 `title`은 `factory_movie` 의 내부함수인 **`get_title` 과 `set_title`을 통해서만 접근할 수 있는 `private`한 변수가 되는 것**이다.



## 프로토타입에 대해 설명
## 이벤트 루프에 대해 설명
## 실행 컨텍스트에 대해 설명
## 호이스팅에 대해 설명
## CORS에 대해 설명, 해결 방법
## RESTful API란

### 참고
* [https://davidhwang.netlify.app/Developments/browser-rendering-process/](https://davidhwang.netlify.app/Developments/browser-rendering-process/)
* [https://opentutorials.org/course/743/6544](https://opentutorials.org/course/743/6544)
