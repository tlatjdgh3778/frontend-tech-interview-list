# 2편
## 목차
* [이벤트 루프에 대해 설명](#이벤트-루프에-대해-설명)
* [실행 컨텍스트에 대해 설명](#실행-컨텍스트에-대해-설명)
* [호이스팅에 대해 설명](#호이스팅에-대해-설명)
* [CORS에 대해 설명, 해결 방법](#cors에-대해-설명-해결-방법)
* [RESTful API란](#restful-api란)


## 이벤트 루프에 대해 설명

이벤트 루프를 한 문장으로 설명하면 다음과 같다.
> "The  event loop job is to look at the stack and look at the task queue. If the stack is empty, it takes the first thing on the queue and pushed it on to the stack."
[What the heck is the event loop anyway? - JSConf YouTube](https://www.youtube.com/watch?v=8aGhZQkoFbQ)

Call stack과 Task Queue를 주시하고 Call stack이 비어있다면 Task Queue에 있던 작업을 Call stack으로 보내주는 역할을 한다.

<p align="center"><img src="https://miro.medium.com/max/700/1*4lHHyfEhVB0LnQ3HlhSs8g.png" /></p>

### JS Engine
<p align="center"><img src="https://miro.medium.com/max/700/1*OnH_DlbNAPvB9KLxUCyMsA.png" /></p>

자바스크킵트 엔진은 Memory Heap과 Call Stack으로 이루어져 있다. 가장 유명한 예시는 Google의 V8 엔진이 있다.

* Memory Heap - 메모리 할당이 발생하는 곳(JS를 사용해 만든 함수, 배열, 객체 등의 저장 공간)
* Call Stack - 코드가 실행될 때 스택 형태로 쌓이는 곳

### Call Stack
자바스크립트는 Call stack을 하나만 가지고 있으므로 한 번에 하나의 함수만 처리할 수 있다.

```js
function a() {
  b();
  console.log("a");
}

function b() {
  console.log("b");
}
a();
```

이러한 코드가 Call stack에서 어떻게 실행되는지 그림으로 보자.

<p align="center"><img src="https://media.vlpt.us/images/tlatjdgh3778/post/723b4b64-927d-4e6f-a07c-3191dc4e48ab/callsatck.png" /></p>

이처럼 자바스크립트 엔진에서는 하나의 작업만 실행 할 수 있지만 자바스크립트는 자바스크립트 엔진으로만 돌아가는 것이 아니다.

### Web APIs
Web APIs는 자바스크립트 엔진에 존재하지 않고 브라우저에서 제공하는 API로, DOM, AJAX, Timeout등이 있다.

자바스크립트에서 `setTimeout`과 같은 함수를 실행하면, 자바스크립트 엔진은 Web API에 `setTimeout` 을 요청하고 동시에 `setTimeout`에 넣어준 Callback 까지 전달한다. Call stack 에서는 Web API 요청 이후 `setTimeout` 작업이 완료되어 제거된다.
Web API는 방금 받은 `setTimeout` 을 완료하고, 동시에 전달받은 Callback 을 Task Queue라는 곳에 넘겨준다.

### Task Queue
TaskQueue는 Callback Queue라고도 한다. 큐 형태로 Web API에서 넘겨받은 Callback 함수를 저장한다. 이 Callback 함수들은 자바스크립트 엔진의 Call stack의 모든 작업이 완료되면 순서대로 추가된다. 이 때 Call stack에 남은 작업이 있는지와 Task Queue에 Task가 존재하는지를 판단하고 Task를 Call stack으로 보내주는 역할을 하는 것이 **Event Loop**의 역할이다.

다음 코드가 어떻게 동작하는지 애니메이션으로 보자.

```js
setTimeout(function() {
    console.log("Hello World");
}, 5000);
```

<p align="center"><img src="https://images.velog.io/images/tlatjdgh3778/post/de3a4ab7-4069-4c30-9b05-e2302595066c/event-loop.gif" /></p>

* [맨 위로](#목차)

## 호이스팅에 대해 설명
호이스팅이란 모든 선언(**var, let, const, function, function*, class**)문에 해당 스코프의 최상단으로 옮겨진 것처럼 동작하는 특성을 말한다.

먼저 변수가 어떤 생성 과정을 거치는지 보자.
* 선언 단계 - 변수를 실행 컨텍스트의 변수 객체에 등록한다. 이 변수 객체는 스코프가 참조하는 대상이 된다.
* 초기화 단계 - 변수 객체에 등록된 변수를 위한 공간을 메모리에 확보한다. 이 단계에서 변수는 `undefined` 로 초기화 된다.
* 할당 단계 - `undefined` 로 초기화된 변수에 실제 값을 할당한다.

### 변수 호이스팅
**var 키워드**로 변수를 생성하면 선언 단계와 초기화 단계가 동시에 이루어진다.

<p align="center"><img src="https://media.vlpt.us/images/tlatjdgh3778/post/be33b2de-c79d-4fe8-8e2c-82c55bfa1e33/var-lifecycle.png" /></p>

```js
// 스코프의 선두에서 선언 단계와 초기화 단계가 실행된다.
// 따라서 변수 선언문 이전에 변수를 참조할 수 있다.
console.log(foo); // undefined

var foo;
console.log(foo); // undefined

foo = 1; // 할당문에서 할당 단계가 실행된다.
console.log(foo); // 1
```

스코프에 변수를 동록하고(선언 단계) 메모리에 변수를 위한 공간을 확보한 후, `undefined` 로 초기화 한다(초기화 단계). 따라서 변수 선언문 이전에 변수에 접근하여도 스코프에 변수가 존재하기 때문에 에러가 발생하지 않는다. 이후 변수 할당문에 도달하면 그 때 값이 할당된다.

**let 키워드**로 변수를 생성하면 선언과 초기화가 분리되어 진행된다.

<p align="center"><img src="https://media.vlpt.us/images/tlatjdgh3778/post/7abfd2c7-bb4a-4988-af0e-16443261f26e/let-lifecycle.png" /></p>

```js
// 스코프의 선두에서 선언 단계가 실행된다.
console.log(foo); // ReferenceError: foo is not defined

let foo; // 변수 선언문에서 초기화 단계가 실행된다.
console.log(foo); // undefined

foo = 1; // 할당문에서 할당 단계가 실행된다.
console.log(foo); // 1
```

스코프에 변수를 등록하지만(선언 단계) 초기화 단계는 변수 선언문에 도달했을 때 이루어진다. 초기화 이전에 변수에 접근하려고 하면 `ReferenceError` 가 발생한다. 변수를 위한 메모리 공간이 아직 확보되지 않았기 때문이다. 따라서 스코프의 시작 지점부터 초기화 시작 지점까지는 변수를 참조할 수 없다. 이 구간을 **일시적 사각지대(Temporal Dead Zone; TDZ)** 라고 부른다.

**const 키워드**는 반드시 선언과 동시에 할당이 이루어져야 한다. 때문에 `let` 과 마찬가지로 `TDZ` 의 제한을 받는다.

`let`, `const` 에서는 호이스팅이 일어나지 않는다는 생각을 할 수도 있지만 사실은 호이스팅은 일어나지만 `TDZ` 의 영향 때문에 호이스팅이 일어나지 않는 것처럼 보이는 것이다. 

### 함수 호이스팅
**함수 선언식**으로 선언한 함수는 호이스팅이 되며 함수 자체가 호이스팅 된다.

```js
sum(10, 20); // this funcion has been hoisted
function sum(a, b) {
  return a + b;
}
```

위 코드는 아래와 같이 동작한다.

```js
function sum(a, b) {
  return a + b;
}
sum(10, 20);
```

**함수 표현식**으로 선언한 함수는 변수 호이스팅이 발생하게 된다.

```js
sum(10, 20);
let sum = function (a, b) {
  return a + b;
};
// Uncaught ReferenceError: sum is not defined
```

실제로는 이렇게 동작한다.

```js
let sum;
sum(10, 20);
sum = function (a, b) {
  return a + b;
};
// Uncaught ReferenceError: sum is not defined
```

`let` 변수에 대해서 호이스팅을 하는데 `let`은 `TDZ`의 영향을 받기 때문에 호이스팅은 수행하지만 초기화 되기전에 참조를 해서 `ReferenceError`가 출력되는 것이다.

그럼 var 키워드 일때는 어떻게 될까

```js
sum(10, 20);
var sum = function (a, b) {
  return a + b;
};
// Uncaught TypeError: sum is not a function
```

실제로는 이렇게 동작한다.

```js
var sum;
sum(10, 20);
sum = function (a, b) {
  return a + b;
};
// Uncaught TypeError: sum is not a function
```

`var sum;`을 선언하고 초기화도 함께 되었지만 `sum(10, 20);` 을 실행할 때에는 변수이기 때문에 `sum is not a function` 오류가 발생한다.

* [맨 위로](#목차)

## 실행 컨텍스트에 대해 설명
실행 컨텍스트(Execution context, EC)는 **실행 가능한 코드가 실행되기 위해 필요한 환경**을 말한다. 

자바스크립트가 가지고 있는 세 가지 실행 컨텍스트가 있다.
1. **Global execution context(GEC)** - 기본적으로 자바스크립트 코드가 시작할 때는 기본적으로 가지고 시작하는 실행 컨텍스트이다. 이 GEC는 무조건 하나만 생성된다.(자바스크립트는 싱글 스레드 언어이기 때문에)
2. **Functional execution context(FEC)** - 함수가 실행될 때 마다 정의되는 컨텍스트이다. GEC는 단 한 번만 정의하는 것과 달리, FEC는 매 실행시마다 정의되어 함수 실행이 종료되면 Call Stack에서 제거된다.
3. **Eval context**: eval 함수로 실행한 코드의 컨텍스트이다.

### Execution context stack (ECS)
ECS는 만들어진 컨텍스트들을 스택 형태로 저장하는 저장소이다. 전역 실행 컨텍스트는 기본적으로 ECS에 있으며 스택의 맨 아래에 존재한다. 자바스크립트 엔진이 함수 호출을 찾으면 해당 함수에 대한 컨텍스트를 ECS에 push한다. 그 다음 자바스크립트 엔진은 ECS 스택의 맨 위에 컨텍스트 함수(FEC)를 실행하고 함수의 모든 코드가 실행되면 해당 함수를 pop 하고 그 아래에 있는 함수에 대해서 동일하게 진행한다.

아래 코드를 보면서 동작 과정을 이해해보자.

```js
var a = 10;

function functionA() {
	console.log("Start function A");
	function functionB(){
		console.log("In function B");
	}
	functionB();
}
functionA();

console.log("GlobalContext");
```

<p aling="center"><img src="https://miro.medium.com/max/700/1*bDebsOuhRx9NMyvLHY2zxA.gif" /></p>

1. 코드를 실행하면 자바스크립트 엔진은 제일 먼저 GEC를 스택으로 push한다.
2. `functionA` 를 호출하면`functionA` 에 대한 실행 컨텍스트를 스택에 push하고 `functionA` 를 실행한다.
3. `functionA` 컨텍스트 안의 `functionB` 를 호출하면 `functionB` 에 대한 실행 컨텍스트를 스택에 push한다. 
4. `functionB` 의 모든 코드가 실행되고 나면 자바스크립트 엔진은 스택에서 `functionB` 실행 컨텍스트를 pop한다.
5. 그 후 `functionA` 의 남아 있는 코드들을 실행하고 모두 실행하면 자바스크립트 엔진은 스택에서 `functionA` 실행 컨텍스트를 pop한다.
6. 전역 실행 컨텍스트에서 나머지 코드들을 실행한다. 모든 코드가 실행되면 스택에서 전역 실행 컨텍스트를 pop하고 JavaScript의 실행을 종료한다.

더욱 자세한 설명과 실행 컨텍스트의 생성 과정을 알고 싶다면

* [실행 컨텍스트와 자바스크립트의 동작 원리 - PoiemaWeb](https://poiemaweb.com/js-execution-context)
* [Execution context, Scope chain and JavaScript internals](https://medium.com/@happymishra66/execution-context-in-javascript-319dd72e8e2c)

* [맨 위로](#목차)

## CORS에 대해 설명, 해결 방법
교차 출처 리소스 공유(Cross-origin resource sharing, CORS)는 추가적인 HTTP헤더를 사용해서 애플리케이션이 다른 origin의 리소스에 접근할 수 있도록 하는 메커니즘을 말한다.

브라우저에서 기본적으로 API요청을 할 때에는 브라우저의 현재 주소와 API 주소의 도메인이 일치해야만 데이터를 접근할 수 있게 되어있다. 만약 다른 도메인에서 API를 요청해서 사용할 수 있게 해주려면 CORS요청을 가능하게 서버에서 특정 헤더인 Access-Control-Allow-Origin과 함께 응답하면 된다.

```js
app.get('/', (req,res) => {
  res.header("Access-Control-Allow-Origin", "*"); // 모든 도메인
  ...
}
```
또는
```js
app.get('/', (req,res) => {
  res.header("Access-Control-Allow-Origin", "허용하고자 하는 도메인");
  ...
}
```

위와 같이 서버 쪽에 코드를 작성해주면 된다. 

* [맨 위로](#목차)

## RESTful API란

### REST
REST 란 REpresentational State Transfer 의 약자로 웹에 존재하는 모든 자원(이미지, 동영상, DB 자원)에 고유한 URI를 부여해 활용하는 것으로, 자원을 정의하고 자원에 대한 주소를 지정하는 방법론을 의미한다고 한다.

더 구체적으로는 **HTTP URI을 통해 자원을 명시하고, HTTP Method(POST, GET, DELETE, PUT)를 통해 해당 자원에 대한 CRUD(CREATE, READ, UPDATE, DELETE) 오퍼레이션을 적용하는 것**이라고 한다.

기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그래도 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일이다. 

#### REST의 구성 요소
자원, 행위, 표현으로 구성되어 있다.

1. 자원(Resource) : **URI**
* 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
* 자원을 구별하는 ID는 ‘/groups/:group_id’와 같은 HTTP URI 다.
* Client는 URI를 이용해서 자원을 지정하고, 해당 자원의 상태(정보)에 대한 조작을 Server에 **요청**한다.
2. 행위(Verb)
* **HTTP Method(POST, GET, PUT, DELETE)**
3. 표현(Representation)
* **JSON, XML** 등을 통해 데이터 주고 받기
* Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 **응답**(Representation)을 보낸다.

### REST API
REST API는 REST 기반으로 서비스 API를 구현한 것이다. 

REST API의 특징으로는 
* 각 요청이 어떤 동작이나 정보를 위한 것인가를 그 요청의 모습 자체로 추론이 가능하다는 점이다.
  * 이를 **Self-descriptive** 라고 한다.
* 때문에 원래는 POST로도 모든 기능을 전부 할 수 있지만.. 하지 않는 것이 REST하게 만들기 위함이다.

### RESTful
RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다. REST API를 제공하는 웹 서비스를 **RESTful** 하다고 할 수 있다.

* [맨 위로](#목차)

### 참고
* [https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf](https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf)
* [https://www.digitalocean.com/community/tutorials/understanding-hoisting-in-javascript](https://www.digitalocean.com/community/tutorials/understanding-hoisting-in-javascript)
* [https://poiemaweb.com/es6-block-scope](https://poiemaweb.com/es6-block-scope)
* [Execution context, Scope chain and JavaScript internals](https://medium.com/@happymishra66/execution-context-in-javascript-319dd72e8e2c)
* [그런 REST API로 괜찮은가](https://www.youtube.com/watch?v=RP_f5dMoHFc)
