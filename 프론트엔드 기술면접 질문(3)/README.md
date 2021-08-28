> 본 포스트는 [React Interview Questions and Answers (2021)](https://www.interviewbit.com/react-interview-questions/) 를 참고하여 작성하였습니다.

## 목차
* [1. React를 사용하면 어떤 장점이 있나요?](#1-react를-사용하면-어떤-장점이-있나요)
* [2. JSX란 무엇인가요?](#2-jsx란-무엇인가요)
* [3. 함수형 컴포넌트와 클래스형 컴포넌트의 차이점이 무엇인가요?](#3-함수형-컴포넌트와-클래스형-컴포넌트의-차이점이-무엇인가요)
* [4. virtual DOM이 무엇인가요? React는 어떻게 virtual DOM을 사용하여 UI를 렌더링하나요?](#4-virtual-dom이-무엇인가요-react는-어떻게-virtual-dom을-사용하여-ui를-렌더링하나요)
* [5. 제어 컴포넌트와 비제어 컴포넌트의 차이점은 무엇인가요?](#5-제어-컴포넌트와-비제어-컴포넌트의-차이점은-무엇인가요)
* [6. React에서 lifecycle 메소드에는 어떤 것들이 있나요?](#6-react에서-lifecycle-메소드에는-어떤-것들이-있나요)
* [7. React의 Strict Mode에 대해서 설명해주세요](#7-react의-strict-mode에-대해서-설명해주세요)
* [8. React에서 리렌더링을 어떻게 방지하나요?](#8-react에서-리렌더링을-어떻게-방지하나요)
* [9. React의 state와 props에 대해서 설명해주세요](#9-react의-state와-props에-대해서-설명해주세요)
* [10. React Hooks에 대해서 설명해주세요](#10-react-hooks에-대해서-설명해주세요)
* [11. React 컴포넌트의 스타일을 지정하는 방법들은 어떤 것들이 있나요?](#11-react-컴포넌트의-스타일을-지정하는-방법들은-어떤-것들이-있나요)
* [12. React 앱 성능을 최적화 하는 몇가지 방법들에 대해 설명해주세요](#12-react-앱-성능을-최적화-하는-몇가지-방법들에-대해-설명해주세요)
* [13. React에서 key란 무엇인가요?](#13-react에서-key란-무엇인가요)
* [14. React 컴포넌트 사이에서 데이터를 어떻게 주고받나요?](#14-react-컴포넌트-사이에서-데이터를-어떻게-주고받나요)
* [15. HOC(Higher Order Components)가 무엇인가요?](#15-hochigher-order-components가-무엇인가요)
* [16. React에서 prop drilling이 무엇인가요?](#16-react에서-prop-drilling이-무엇인가요)
* [17. 에러 경계(Error Boundaries)란 무엇인가요?](#17-에러-경계error-boundaries란-무엇인가요)

## 1. React를 사용하면 어떤 장점이 있나요?
* **Virtual DOM을 사용하여 효율성 향상.**
  * React는 virtual DOM을 사용하여 뷰를 렌더링한다. 이름에서 알 수 있듯이 virtual DOM은 real DOM을 가상으로 표현한 것이다. react 앱에서 데이터가 변경될 때마다 새로운 virtual DOM이 생성된다. virtual DOM을 만드는 것이 브라우저 내에서 UI를 렌더링 하는 것보다 더욱 빠르다.
* **러닝 커브가 별로 없다.**
  * React는 Angular와 같은 프레임워크에 비해서 완만한 러닝 커브를 가지고 있다. 누구나 Javascript의 지식을 조금만 가지고 있어도 React를 사용하여 웹 앱을 만들 수 있다.
* **SEO 친화적이다.**
  * React는 개발자가 다양한 검색 엔진에서 쉽게 탐색될 수 있는 사용자 인터페이스를 개발할 수 있도록 한다. 그리고 Server-Side Rendering도 가능하기 때문에 앱의 SEO가 향상된다.
* **재사용 가능한 컴포넌트**
  * React는 컴포넌트 기반 아키텍처를 사용한다. 컴포넌트는 독립적이며 재사용 가능한 코드의 조각들이다. 이러한 컴포넌트는 유사한 기능을 가진 다양한 애플리케이션에서 공유할 수 있다. 재사용 가능한 컴포넌트들은 개발 속도를 향상시켜준다.
* **거대한 커뮤니티. **
  * 거대한 커뮤니티는 React 애플리케이션을 만드는 데 사용할 수 있는 많은 라이브러리를 제공한다.

* [맨 위로](#목차)

## 2. JSX란 무엇인가요?
JSX(JavaScript XML의 약자)을 사용하면 `appendChild()`, `createElement()` 와 같은 기능을 사용하지 않고도 JavaScript 내부에 HTML을 작성하여 돔에 적용시킬 수 있는 문법이다.

[공식 문서](https://ko.reactjs.org/docs/react-without-jsx.html)에 따르면 JSX는 `React.createElement()` 함수에 surgar syntax를 제공한다. 때문에 JSX로 할 수 있는 모든 것은 순수 JavaScript로도 가능하다.

*JSX를 사용하지 않고도 React 애플리케이션을 만들 수 있다.*

**Without using JSX**
```js
const text = React.createElement('p', {}, 'This is a text');
const container = React.createElement('div','{}',text );
ReactDOM.render(container,rootElement);
```

**Using JSX**
```js
const container = (
 <div>
   <p>This is a text</p>
 </div>
);
ReactDOM.render(container,rootElement);
```

* [맨 위로](#목차)
## 3. 함수형 컴포넌트와 클래스형 컴포넌트의 차이점이 무엇인가요?
Hooks가 도입되기 전에 함수형 컴포넌트는 stateless 컴포넌트로 불렸다. 기능 기반에서 클래스형 컴포넌트 뒤에 있었다. 하지만 Hooks가 도입된 후 함수형 컴포넌트는 클래스형 컴포넌트와 동일한 기능을 가지게 되었다.

**Stateful 컴포넌트** - state를 사용하는 경우 / Container
```js
class Main extends Component {
 constructor() {
   super()
   this.state = {
     books: []
   }
 }
 render() {
   <BooksList books={this.state.books} />
 }
}
```
**Stateless 컴포넌트** - state를 사용하지 않는 경우 / Presentational
```js
const BooksList = ({books}) => {
 return (
   <ul>
     {books.map(book => {
       return <li>book</li>
     })}
   </ul>
 )
}
```

Hooks가 새로운 트렌드로 들어왔지만 React 팀은 클래스형 컴포넌트를 유지한다고 했다. 때문에 클래스형 컴포넌트도 알고 있는 것이 좋다. 

다음을 기준으로 함수형 컴포넌트와 클래스형 컴포넌트를 비교한다.

### 3-1. Decalaration
**함수형 컴포넌트**

함수형 컴포넌트는 화살표 함수 또는 함수 선언식으로 선언이 가능하다.
```js
function card(props){
 return(
   <div className="main-container">
     <h2>Title of the card</h2>
   </div>
 )
}

const card = (props) =>{
 return(
   <div className="main-container">
     <h2>Title of the card</h2>
   </div>
 )
}
```

**클래스형 컴포넌트**

클래스형 컴포넌트는 ES6의 class문법으로 선언이 가능하다.
```js
class Card extends React.Component{
 constructor(props){
   super(props);
 }

 render(){
   return(
     <div className="main-container">
       <h2>Title of the card</h2>
     </div>
   )
 }
}
```

### 3-2. Handling props
아래 컴포넌트를 각각 컴포넌트에서 어떻게 렌더링 하는지 살펴보자.
```js
<StudentInfo name="Vivek" rollNumber="23" />
```

**함수형 컴포넌트**
함수형 컴포넌트에서 props를 다루는 것은 매우 간단하다. 함수형 컴포넌트에 인수로 제공된 모든 props들은 HTML 요소 내에서 직접적으로 사용이 가능하다.
```js
function StudentInfo(props){
 return(
   <div className="main">
     <h2>{props.name}</h2>
     <h4>{props.rollNumber}</h4>
   </div>
 )
}
```

**클래스형 컴포넌트**
클래스형 컴포넌트에서 props를 다루기 위해서는 `this` 키워드를 사용한다.
```js
class StudentInfo extends React.Component{
 constructor(props){
   super(props);
 }

 render(){
   return(
     <div className="main">
       <h2>{this.props.name}</h2>
       <h4>{this.props.rollNumber}</h4> 
     </div>
   )
 }
}
```

### 3-3. Handling state
**함수형 컴포넌트**
함수형 컴포넌트에서는 state를 다루기 위해서 hooks를 사용한다.
```js
function ClassRoom(props){
 let [studentsCount,setStudentsCount] = useState(0);

 const addStudent = () => {
   setStudentsCount(++studentsCount);
 }
 return(
   <div>
     <p>Number of students in class room: {studentsCount}</p>
     <button onClick={addStudent}>Add Student</button>
   </div>
 )
}
```
**클래스형 컴포넌트**
클래스형 컴포넌트에서는 hooks를 사용할 수 없기 때문에 다른 방식으로 state를 다룬다.

* `this.state` 를 사용하여 `studentsCount` 변수를 추가하고 값을 `0` 으로 초기화한다
* state를 읽을 때에는 `this.state.studentsCount` 로 값을 읽을 수 있다.
* state를 변경하기 위해서는 `this.setState` 를 사용한다.

```js
class ClassRoom extends React.Component{
  constructor(props){
    super(props);
    this.state = {studentsCount : 0};

    this.addStudent = this.addStudent.bind(this);
  }

  addStudent(){
    this.setState((prevState)=>{
      return {studentsCount: prevState.studentsCount++}
    });
  }

  render(){
    return(
      <div>
        <p>Number of students in class room: {this.state.studentsCount}</p>
        <button onClick={this.addStudent}>Add Student</button>
	  </div>
	)
  }
}
```

* [맨 위로](#목차)

## 4. virtual DOM이 무엇인가요? React는 어떻게 virtual DOM을 사용하여 UI를 렌더링하나요?
[virtual DOM](https://ko.reactjs.org/docs/faq-internals.html)은 UI의 이상적인 또는 가상적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 "실제" DOM과 동기화하는 프로그래밍 개념이다.

DOM 조작은 모든 웹 애플리케이션에서 필수적인 부분이지만, JavaScript의 DOM 조작은 다른 작업에 비해 상당히 느리다.
여러 DOM 조작이 수행되면 애플리케이션의 효율성에 영향을 안좋은 영향을 준다. 대부분의 JavaScript 프레임워크는 DOM의 작은 부분이 변경되더라도 전체 DOM을 업데이트한다.
예를 들어, 목록의 항목 중 하나가 변경되면 변경된 항목만 렌더링 하는 것이 아니라 전체 목록이 다시 렌더링된다. 
이러한 문제점을 해결하기 위해 도입된 것이 **virtual DOM** 이다.

### 4-1. virtual DOM의 동작
모든 DOM object에 대해 동일한 속성을 가진 가상 DOM object가 존재한다.
real DOM object와 virtual DOM object의 주요 차이점은 virtual DOM object의 변경 내용이 화면에 직접 반영되지 않는다는 것이다. virtual DOM object를 real DOM object의 청사진(Blueprint)로 간주한다.
JSX요소가 리렌더링 될 때마다 모든 virtual DOM object가 업데이트된다.

> 모든 virtual DOM object를 업데이트 하는 것이 비효율적이라고 생각할 수도 있지만, virtual DOM 업데이트가 real DOM 업데이트보다 훨씬 빠르다. real DOM의 청사진(Blueprint)만 업데이트하기 때문이다.

React는 두 개의 virtual DOM을 사용하여 UI를 렌더링한다. 하나는 객체의 현재 상태를 저장하는 데 사용되고, 다른 하나는 객체의 이전 상태를 저장하는 데 사용된다.

* **변화가 일어나면 변화된 버전을 virtual DOM 으로 바꾼다.**
  * 데이터가 업데이트 되면 전체 UI을 virtual DOM에 리렌더링 한다.
* **virtual DOM끼리 비교한다.**
  * 변화 전의 virtual DOM과 변화 후의 virtual DOM을 비교한다.
* **바뀐 부분을 real DOM에 적용한다.**
  * 바뀐 부분만 적용을 함으로서 레이아웃 계산은 한 번만 수행된다.

<p align="center"><img src="https://media.vlpt.us/images/mollog/post/fdc15800-579c-457c-aa26-3b4c916c9c1e/image.png" /></p>

* [맨 위로](#목차)

## 5. 제어 컴포넌트와 비제어 컴포넌트의 차이점은 무엇인가요?

### 5-1. 제어 컴포넌트(Controlled component)
제어 컴포넌트는 컴포넌트의 상태나 속성(props)으로 주어진 값을 활용하는 컴포넌트이다.

제어 컴포넌트에서 input 요소의 값은 React에 의해 제어된다. input 요소의 상태를 코드 내부에 저장하며, 이벤트 기반 콜백을 사용하여 input 요소의 변경 사항이 코드에도 반영된다.
사용자가 제어 컴포넌트의 input 요소 내부에 데이터를 입력하면 `onChange` 함수가 트리거되고 코드 내부에 입력한 값이 유효한지 유효하지 않은지 확인한다. 값이 유효하면 상태를 변경하고 input 요소를 새 값으로 리렌더링한다.

```js
function FormValidation(props) {
 const [inputValue, setInputValue] = useState("");

 const updateInput = e => {
   setInputValue(e.target.value);
 };

 return (
   <div>
     <form>
       <input type="text" value={inputValue} onChange={updateInput} />
     </form>
   </div>
 );
}
```

위 코드에서 볼 수 있듯이 input 요소의 값은 `inputValue` 변수의 상태에 따라 결정된다.

### 5-2. 비제어 컴포넌트(Uncontrolled component)
HTML 태그 중에서 태그 자체적으로 상태를 갖는 경우가 있다. 대표적인 경우가 input 태그로, 입력 폼에서 값을 입력하면 해당 값은 입력 폼 내부의 상태로 관리된다.

비제어 컴포넌트에서 input 요소의 값은 DOM 자체에서 처리되고 비제어 컴포넌트 내부의 input 요소는 일반 input form 요소와 동일하게 동작한다.
input 요소의 상태는 DOM에서 처리되고 값이 변경될 때마다 이벤트 기반 콜백이 호출되지 않는다.
> 기본적으로 input 요소에 변경 사항이 있어도 React는 어떤 작업도 수행하지 않음(컴포넌트의 상태가 바뀌지 않아서)

input 요소의 값에 접근하기 위해서 ref를 사용한다.

```js
function FormValidation(props) {
 let inputValue = React.createRef();

 let handleSubmit = e => {
   alert(`Input value: ${inputValue.current.value}`);
   e.preventDefault();
 };

 return (
   <div>
     <form onSubmit={handleSubmit}>
       <input type="text" ref={inputValue} />
       <button type="submit">Submit</button>
     </form>
   </div>
 );
}
```

* [맨 위로](#목차)

## 6. React에서 lifecycle 메소드에는 어떤 것들이 있나요?
React의 각 컴포넌트는 다음 세 단계를 거친다. **Mounting**, **Updating**, **Unmounting**

> 자주 사용되는 메소드는 * 표시

### 6-1. Mounting
컴포넌트를 마운트할 때 순서대로 호출된다.
* **constructor()*** 
  * 해당 컴포넌트가 마운트되기전에 호출된다. 
  * 이 메소드 안에서 컴포넌트의 초기 상태를 설정할 수 있다.
  * 초기 상태 및 바인딩 메소드를 설정하는 데 사용된다.
* **getDerivedStateFromProps()** 
  * 최초 마운트 시, 갱신 시 모두에서 render 를 호출하기 직전에 호출된다.
  * 받은 props를 기준으로 컴포넌트의 상태를 설정할 수 있다.
  * 매우 드물게 사용된다.
* **render()***
  * 클래스형 컴포넌트에서 반드시 구현되어야하는 유일한 메소드이다.
  * DOM 내부에서 렌더링 될 HTML 요소를 반환한다.
  * React Element, 배열과 Fragment, Portal, 문자열과 숫자, Boolean or null 중에 하나를 반환해야 한다.
* **componentDidMount()***
  * 컴포넌트가 DOM 내부에서 렌더링된 직후(트리에 삽입된 직후) 호출된다.
  * DOM 노드가 있어야 하는 초기화 작업은 이 메소드에서 이루어지면 된다.
  * 외부에서 데이터를 불러와야 한다면, 네트워크 요청을 보내기 적절한 위치이다.
  
### 6-2. Updating
props또는 state가 변경되면 업데이트가 발생한다. 업데이트가 발생하면 컴포넌트가 다시 렌더링 된다. 아래 메소드들은 컴포넌트가 다시 렌더링될 때 순서대로 호출된다.
* **getDerivedStateFromProps()**
  * 컴포넌트가 리렌더링될 때 호출된다.(기능은 위와 동일)
* **shouldComponentUpdate()**
  * 이 메소드를 사용하면 현재 state 또는 props의 변화가 컴포넌트의 출력 결과에 영향을 미치는지 여부를 React가 알 수 있다.
  * 기본 동작은 매 state 변화마다 다시 렌더링을 수행하는 것으로 값은 true이다.
  * false를 반환하면 `render()`, `componentDidUpdate()` 는 호출되지 않는다.
* **render()***
  * 동일
* **getSnapshotBeforeUpdate()**
  * 가장 마지막으로 렌더링된 결과가 DOM에 반영되었을 때 호출된다.
  * 이 메소드를 사용하면 컴포넌트가 DOM으로부터 스크롤 위치 등과 같은 정보를 이후 변경되기 전에 얻을 수 있다.
  * 반환하는 값(스냅샷 값 or null)은 `componentDidUpdate()` 의 인자로 전달된다.
  * 채팅 화면처럼 스크롤 위치를 따로 처리하는 작업이 필요한 UI등에 사용한다.
* **componentDidUpdate()***
  * 컴포넌트가 리렌더링된 후에 호출된다.
  * `componentDidMount()` 와 동일하게 작동하지만 초기 렌더링 시에는 호출되지 않는다는 차이점이 있다.
  
### 6-3. Unmounting
컴포넌트가 DOM 상에서 제거될 때 호출된다.
* **componentWillUnmount()**
  * 컴포넌트가 마운트 해제되어 제거되기 직전에 호출된다.
  * 타이머 제거, 네트워크 요청 취소, `componentDidMount()` 에서 생성된 구독 해제 등 필요한 모든 정리 작업(clean-up)을 수행한다.
  
* [맨 위로](#목차)

## 7. React의 Strict Mode에 대해서 설명해주세요
StrictMode는 애플리케이션 내의 잠재적인 문제를 알아내기 위한 도구이다.

`<React.StrictMode>` 를 사용하여 Strict Mode를 사용할 수 있다.
```js
function App() {
  return (
    <React.StrictMode>
      <div classname="App">
        <Header/>
        <div>
          Page Content
        </div>
        <Footer/>
      </div>
    </React.StrictMode>
  );
}
```

Strict Mode의 **[이점](https://ko.reactjs.org/docs/strict-mode.html#identifying-unsafe-lifecycles)**

* [맨 위로](#목차)

## 8. React에서 리렌더링을 어떻게 방지하나요?
컴포넌트의 props 또는 state가 변경될 때마다 컴포넌트 및 하위 컴포넌트의 리렌더링이 발생한다. 업데이트 되지 않은 컴포넌트까지 렌더링 한다면 애플리케이션 성능에 좋지 않은 영향을 주는 것이다.

* `shouldComponentUpdate()` 의 반환값을 false로 주어서 리렌더링을 방지할 수 있다.
```js
class Message extends React.Component {
 constructor(props) {
   super(props);
   this.state = { message: "Hello, this is vivek" };
 }
 shouldComponentUpdate() {
   console.log("Does not get rendered");
   return false;
 }
 render() {
   console.log("Message is getting rendered");
   return (
     <div>
       <p>{this.state.message}</p>
     </div>
   );
 }
}
```

* 함수형 컴포넌트에서는 `React.memo` 로 위의 기능을 구현할 수 있다.
```js
const MyComponent = React.memo(function MyComponent(props) {
 /* only rerenders if props change */
});
```

* [맨 위로](#목차)

## 9. React의 state와 props에 대해서 설명해주세요

### 9-1. state
React의 모든 컴포넌트에는 해당 컴포넌트에 속하는 모든 속성 값이 포함된 state 객체를 가지고 있다. state 객체는 컴포넌트의 동작을 제어하고 state 객체의 속성 값이 변경되면 컴포넌트가 리렌더링된다.

> state 객체는 함수형 컴포넌트에서 사용할 수 없지만 Hooks를 사용하여 함수형 컴포넌트에서도 사용이 가능해졌다.

```js
class Car extends React.Component {
 constructor(props) {
   super(props);
   // declare state object 
   this.state = {
     brand: "BMW",
     color: "Black"
   };
 }

 changeColor() {
   // update state object
   this.setState(prevState => {
     return { color: "Red" };
   });
 }

 render() {
   return (
     <div>
       <button onClick={() => this.changeColor()}>Change Color</button>
       <p>{this.state.color}</p>
     </div>
   );
 }
}
```

위 코드에서 볼 수 있듯이 `this.state.propertyName` 으로 state를 사용할 수 있고 `this.setState()` 함수로 state를 업데이트 할 수 있다.

### 9-2. props
props는 부모 컴포넌트에서 자식 컴포넌트로 전달되는 데이터이다. props는 수정될 수 없으며(read-only) 표시되거나 다른 값을 계산하는데만 사용된다.

```js
<Car brand="Mercedes"/>
```

클래스형 컴포넌트와 함수형 컴포넌트에서 props를 받아서 사용하는 방법

```js
// 클래스형 컴포넌트
class Car extends React.Component {
 constructor(props) {
   super(props);
   this.state = {
     brand: this.props.brand,
     color: "Black"
   };
 }
}
// ...
// 함수형 컴포넌트
function Car(props) {
 const [brand, setBrand] = useState(props.brand);
}
```

* [맨 위로](#목차)

## 10. React Hooks에 대해서 설명해주세요
React Hooks는 React 16.8에서 추가된 기능이다. Hooks를 이용하여 함수형 컴포넌트에서 state 및 lifecycle 기능을 사용할 수 있다.

> 이전에는 함수형 컴포넌트를 stateless 컴포넌트라고 했다. lifecycle과 상태 관리를 하기 위해서는 클래스형 컴포넌트로 작성을 해야했는데 함수형 컴포넌트에서도 이런 기능들을 사용하기 위해서 Hooks가 만들어졌다.

**ex) useState hook**
```js
import React, { useState } from 'react';

function Example() {
  // "count"라는 새로운 상태 값을 정의합니다.
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

* [맨 위로](#목차)

## 11. React 컴포넌트의 스타일을 지정하는 방법들은 어떤 것들이 있나요?
React 컴포넌트의 스타일을 지정할 수 있는 방법은 여러 가지가 존재한다.

### 11-1. Inline Style
inline style 속성을 사용해서 요소의 스타일을 직접 지정한다.
Javascript 객체 형식인지 확인
```js
class RandomComponent extends React.Component {
 render() {
   return (
     <div>
       <h3 style={{ color: "Yellow" }}>This is a heading</h3>
       <p style={{ fontSize: "32px" }}>This is a paragraph</p>
     </div>
   );
 }
}
```

### 11-2. Javascript object
별도의 Javascript 객체를 작성하고 원하는 스타일 속성을 설정할 수 있다.
이 객체를 inline style 속성의 값으로 사용할 수 있다.
```js
class RandomComponent extends React.Component {
 paragraphStyles = {
   color: "Red",
   fontSize: "32px"
 };

 headingStyles = {
   color: "blue",
   fontSize: "48px"
 };

 render() {
   return (
     <div>
       <h3 style={this.headingStyles}>This is a heading</h3>
       <p style={this.paragraphStyles}>This is a paragraph</p>
     </div>
   );
 }
}
```

### 11-3. CSS Stylesheet
별도의 CSS 파일을 만들고 그 파일안에 컴포넌트에 대한 스타일을 작성한다.
이 파일을 컴포넌트에서 import 해서 사용한다.
```js
import './RandomComponent.css';

class RandomComponent extends React.Component {
 render() {
   return (
     <div>
       <h3 className="heading">This is a heading</h3>
       <p className="paragraph">This is a paragraph</p>
     </div>
   );
 }
}
```

### 11-4. CSS Modules
별도의 CSS 모듈을 만들고 이 모듈을 컴포넌트에서 불러와서 사용할 수 있다.
CSS Module을 사용하면 CSS 클래스가 중첩되는 것을 완벽하게 막을 수 있다.
>파일 이름을 `.module.css` 으로 만든다.

```js
// styles.module.css
.paragraph{
 color:"red";
 border:1px solid black;
}

// RandomComponent.js
import styles from  './styles.module.css';

class RandomComponent extends React.Component {
 render() {
   return (
     <div>
       <h3 className="heading">This is a heading</h3>
       <p className={styles.paragraph} >This is a paragraph</p>
     </div>
   );
 }
}
```

* [맨 위로](#목차)

## 12. React 앱 성능을 최적화 하는 몇가지 방법들에 대해 설명해주세요

## 12-1. useMemo()
메모이제이션된 값을 반환한다. `useMemo` 는 의존성이 변경되었을 때만 메모이제이션된 값만 다시 계산한다. 
```js
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

첫 번째 파라미터에 함수를 넣어주고 두 번째 파라미터에는 의존성 배열을 넣어주는데 의존성 배열에 있는 값이 변경될 때만 함수를 실행하고 변경되지 않으면 이전에 연산한 값을 재사용한다.

[useMemo로 최적화하기](https://velog.io/@tlatjdgh3778/React-Hooks-useMemo%EB%A1%9C-%EC%B5%9C%EC%A0%81%ED%99%94%ED%95%98%EA%B8%B0)

## 12-2. React.PureComponent
`React.PureComponent` 는 `React.Component` 와 아주 유사하지만 다른 점이 있는데 그것은 `shouldComponentUpdate` 를 다루는 차이가 있다.

`React.PureComponent` 에는 `shouldComponentUpdate` 가 이미 구현되어 있는데 props와 state를 얕은 비교를 통해 비교한 뒤 변경된 것이 있을 때만 리렌더링한다. 
하지만 props나 state가 복잡한 데이터 구조를 포함하고 있다면 비교하는 과정에서 의도하지 않은 결과가 발생할 수 있다. 

```js
class App extends PureComponent
```

> 얕은 비교([Shallow compare](https://stackoverflow.com/questions/36084515/how-does-shallow-compare-work-in-react))
* equality를 체크한다.
* scalar value(number, string)을 비교할 때는 그들의 값을 비교한다.
* **object**를 비교할 때는 attributes를 비교하지 않고 **reference**를 비교한다.
```js
user = {
  name: "John",
  surname: "Doe"
}
// ...
// ex1)
const user = this.state.user;
user.name = "Jane";
console.log(user === this.state.user); // true
// user와 this.state.user는 같은 reference
// ...
// ...
// ex2)
const user = clone(this.state.user);
console.log(user === this.state.user); // false
// user와 clone(this.state.user)는 다른 reference
```

## 12-3. State Colocation
State Colocation은 코드의 위치를 필요한 곳에 최대한 가깝게 이동하는 것을 말한다. 
때때로 React 애플리케이션에서는 상위 컴포넌트 내부에 불필요한 state가 많아 코드를 읽기 어렵고 유지하기가 어렵게 만든다. 한 컴포넌트 내부에 여러 state가 있으면 컴포넌트에 불필요한 리렌더링이 발생하게 된다. 상위 컴포넌트에 덜 중요한 state는 별도의 컴포넌트로 전환하는 것이 좋다.

굳이 global일 필요가 없는 state라면 global state redux나 global context가 아니라 관련된 컴포넌트에 위치시키는 것이 효과적이다. 

[State Colocation](https://ideveloper2.dev/blog/2019-10-12--state-colocation-will-make-your-react-app-faster/)

## 12-4. Lazy Loading
React 애플리케이션의 로딩 속도를 줄이기 위한 기법이다. Lazy Loading은 페이지 내에서 실제로 필요로 할 때까지 리소스의 로딩을 뒤로 미루는 것이다. 페이지를 로드하자마자 리소스를 로딩하는 일반적인 방법 대신, 실제로 사용자 화면에 보여질 필요가 있을 때까지 이러한 로딩을 지연하는 것이다.

* [맨 위로](#목차)

## 13. React에서 key란 무엇인가요?
key는 요소 목록을 사용할 때 포함되어야 하는 특수 문자열이다.

```js
const ids = [1,2,3,4,5];
const listElements = ids.map((id)=>{
 return(
 <li key={id.toString()}>
   {id}
 </li>
 )
})
```

* key는 어떤 요소가 추가, 변경 또는 제거되었는지 확인하는 데 도움이 된다.
* 각 요소에 고유한 ID를 제공하기 위해 배열 요소에 key를 제공해야 한다.
  * 이상적으로는 UUID 또는 기타 고유 문자열을 사용하지만 Array index도 사용이 가능하다.
* key가 없으면 React는 각 요소의 순서나 고유성을 이해하지 못한다.
* 일반적으로 API에서 가져온 데이터 목록을 표시하는 데 사용된다
* *배열 내에서 사용되는 키는 형제간에 고유해야 한다.


* [맨 위로](#목차)

## 14. React 컴포넌트 사이에서 데이터를 어떻게 주고받나요?
<p align="center"><img src="https://assets.interviewbit.com/assets/skill_interview_questions/react/parent-child-08a78d11384e8648988c4ef517f35c68c344bf35c29c90f5d518b41c756193d6.png.gz" /></p>

### 14-1. Parent Component -> Child Component
Parent -> Child 의 데이터 전달은 props를 사용해서 전달이 가능하다.
```js
// Parent Component
import ChildComponent from "./Child";

function ParentComponent(props) {
  const [counter, setCounter] = useState(0);

  const increment = () => setCounter(++counter);

  return (
    <div>
    	<button onClick={increment}>Increment Counter</button>
		<ChildComponent counterValue={counter} />
  	</div>
  );
} 
```

위 코드에서 볼 수 있듯이 `ChildComponent` 로 `counterValue` 라는 props으로 데이터를 전달하고 있는 것을 볼 수 있다. 

```js
function ChildComponent(props) {
 return (
   <div>
     <p>Value of counter: {props.counterValue}</p>
   </div>
 );
}
```

`props.counterValue`를 사용해서 부모 컴포넌트에서 받은 데이터를 사용할 수 있다.

### 14-1. Child Component -> Parent Component
Child -> Parent의 데이터 전달은 Callback(함수)을 사용한다.
1. 부모 컴포는트에 Callback(함수)를 만들어 매개 변수로 필요한 데이터를 가져온다.
2. 이 Callback(함수)를 props로 자식 컴포넌트에게 전달한다.
3. 자식 컴포넌트에서 Callback(함수)을 사용해서 부모 컴포넌트로 전달한다.

**step1, step2 - 부모 컴포넌트에서 Callback을 작성하고 props로 자식 컴포넌트로 전달한다.**
```js
function ParentComponent(props) {
 const [counter, setCounter] = useState(0);

 const callback = valueFromChild => setCounter(valueFromChild);

 return (
   <div>
     <p>Value of counter: {counter}</p>
     <ChildComponent callbackFunc={callback} counterValue={counter} />
   </div>
 );
}
```

**step3 - 자식 컴포넌트에서 부모 컴포넌트로 데이터를 전달한다.**
```js
function ChildComponent(props) {
 const childCounterValue = props.counterValue;

 return (
   <div>
     <button onClick={() => props.callbackFunc(++childCounterValue)}>
       Increment Counter
     </button>
   </div>
 );
}
```
버튼을 클릭하면 증가된 `childCounterValue`를 `props.callbackFunc`에 전달한다.

* [맨 위로](#목차)

## 15. HOC(Higher Order Components)가 무엇인가요?
> 고차 컴포넌트(HOC, Higher Order Components)는 **컴포넌트 로직을 재사용**하기 위한 React의 고급 기술입니다. 고차 컴포넌트(HOC)는 React API의 일부가 아니며, 리액트의 구성적 특성에서 나오는 패턴입니다. -React 공식 문서-

간단히 말하면 HOC는 컴포넌트를 가져와 새로운 컴포넌트를 반환하는 함수이다.

React 애플리케이션을 개발하다 보면 서로 비슷한 컴포넌트를 만들 때가 있다. 큰 애플리케이션을 개발하는 경우에 코드를 DRY(Do not Repeat Yourself)한 상태로 유지해야하기 때문에 이러한 비슷한 컴포넌트들을 줄이고 여러 컴포넌트에서 공유할 수 있는 추상화를 만들어야 한다.

HOC를 통해 이러한 추상화를 만들 수 있다.

**ArticlesList**
```js
// "GlobalDataSource" is some global data source
class ArticlesList extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {
      articles: GlobalDataSource.getArticles(),
    };
  }

  componentDidMount() {
    // Listens to the changes added
    GlobalDataSource.addChangeListener(this.handleChange);
  }

  componentWillUnmount() {
    // Listens to the changes removed
    GlobalDataSource.removeChangeListener(this.handleChange);
  }

  handleChange() {
    // States gets Update whenver data source changes
    this.setState({
      articles: GlobalDataSource.getArticles(),
    });
  }

  render() {
    return (
      <div>
        {this.state.articles.map((article) => (
          <ArticleData article={article} key={article.id} />
        ))}
      </div>
    );
  }
}
```

**UserList**
```js
// "GlobalDataSource" is some global data source
class UsersList extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {
      users: GlobalDataSource.getUsers(),
    };
  }

  componentDidMount() {
    // Listens to the changes added
    GlobalDataSource.addChangeListener(this.handleChange);
  }

  componentWillUnmount() {
    // Listens to the changes removed
    GlobalDataSource.removeChangeListener(this.handleChange);
  }

  handleChange() {
    // States gets Update whenver data source changes
    this.setState({
      users: GlobalDataSource.getUsers(),
    });
  }

  render() {
    return (
      <div>
        {this.state.users.map((user) => (
          <UserData user={user} key={user.id} />
        ))}
      </div>
    );
  }
}
```

`ArticlesList` 와 `UserList` 컴포넌트를 보면 코드가 매우 유사하지만 API endpoint에 대해 서로 다른 메소드를 호출하는 것을 볼 수 있다.

추상화를 만들기 위해 HOC로 작성해보자.

**HOC**
```js
// Higher Order Component which takes a component
// as input and returns another component
// HOC는 컴포넌트를 가져와 새로운 컴포넌트를 반환하는 함수이다.

// "GlobalDataSource" is some global data source
function HOC(WrappedComponent, selectData) {
  return class extends React.Component {
    constructor(props) {
      super(props);
      this.handleChange = this.handleChange.bind(this);
      this.state = {
        data: selectData(GlobalDataSource, props),
      };
    }

    componentDidMount() {
      // Listens to the changes added
      GlobalDataSource.addChangeListener(this.handleChange);
    }

    componentWillUnmount() {
      // Listens to the changes removed
      GlobalDataSource.removeChangeListener(this.handleChange);
    }

    handleChange() {
      this.setState({
        data: selectData(GlobalDataSource, this.props),
      });
    }

    render() {
      // Rendering the wrapped component with the latest data data
      return <WrappedComponent data={this.state.data} {...this.props} />;
    }
  };
}
```

위의 코드에서 `ArticlesList` 컴포넌트와 `UserList` 컴포넌트 간에 공유할 수 있는 기능을 수행하는 HOC라는 함수를 만들었다.
HOC의 두 번째 매개변수인 `selectData`는 API endpoint의 메소드를 호출하는 함수이다.

다음과 같이 `ArticlesList` 컴포넌트와 `UserList` 컴포넌트를 렌더링 할 수 있다.
```js
const ArticlesListWithHOC = HOC(ArticlesList, (GlobalDataSource) => GlobalDataSource.getArticles());
const UsersListWithHOC = HOC(UsersList, (GlobalDataSource) => GlobalDataSource.getUsers());
```

HOC를 사용해서 각 컴포넌트의 기능을 변경하려는 것이 아니라 컴포넌트들의 기능을 공유하려고 사용하는 것이다.

* [맨 위로](#목차)

## 16. React에서 prop drilling이 무엇인가요?
<p align="center"><img src="https://assets.interviewbit.com/assets/skill_interview_questions/react/prop-drilling-8c64f4d4219c5d9535272d44774fa09e494a07d2a2f2cc735ea2e73d1be56821.png.gz" /></p>

prop drilling은 React 컴포넌트 트리에서 데이터를 전달하기 위해서 필요한 과정을 의미한다.

React 애플리케이션을 개발하다 보면 부모 컴포넌트에서 자식의 자식 컴포넌트(또는 더 하위 컴포넌트)로 props를 전달하게 된다.
이렇게 전달하다 보면 중간에 있는 컴포넌트는 단지 하위 컴포넌트로 props를 전달하는 일만 담당한다.

prop drilling 자체가 나쁜 것은 아니지만 pass되는 컴포넌트가 10 ~ 15개가 있다면 코드를 읽을 때 해당 prop을 추적하기가 힘들 것이다. 그리고 단지 전달만 하는 컴포넌트가 존재하게 될 것이다.

물론 좋은 점도 있다.
명시적으로 데이터를 전달할 수 있고, 때문에 데이터를 수정하거나 삭제하기가 편한 장점들도 존재한다.

React의 Context API나 redux, mobx 같은 상태 관리 라이브러리를 사용해서 prop drilling을 회피하는 방법들도 존재한다.

* [맨 위로](#목차)

## 17. 에러 경계(Error Boundaries)란 무엇인가요?
> UI의 일부분에 존재하는 자바스크립트 에러가 전체 애플리케이션을 중단시켜서는 안 됩니다. React 사용자들이 겪는 이 문제를 해결하기 위해 React 16에서는 에러 경계(“error boundary”)라는 새로운 개념이 도입되었습니다.
에러 경계는 하위 컴포넌트 트리의 어디에서든 자바스크립트 에러를 기록하며 **깨진 컴포넌트 트리 대신 폴백 UI를 보여주는 React 컴포넌트**입니다. 에러 경계는 렌더링 도중 생명주기 메서드 및 그 아래에 있는 전체 트리에서 에러를 잡아냅니다. -[React 공식 문서](https://ko.reactjs.org/docs/error-boundaries.html#gatsby-focus-wrapper)-

에러 경계는 다음과 같은 에러는 포착하지 않는다.
* 이벤트 핸들러
* 비동기적 코드
* 서버 사이드 렌더링
* 자식에서가 아닌 에러 경계 자체에서 발생하는 에러

**에러 경계를 사용하지 않는 코드**
```js
class CounterComponent extends React.Component{
 constructor(props){
   super(props);
   this.state = {
     counterValue: 0
   }
   this.incrementCounter = this.incrementCounter.bind(this);
 }

 incrementCounter(){
   this.setState(prevState => counterValue = prevState+1);
 }

 render(){
   if(this.state.counter === 2){
     throw new Error('Crashed');
   }

   return(
     <div>
       <button onClick={this.incrementCounter}>Increment Value</button>
       <p>Value of counter: {this.state.counterValue}</p>
     </div>
   )
 }
}
```
위의 코드에서 `counterValue` 가 2일 때 `render` 메소드 내부에 에러를 발생시키는데 에러 경계를 사용하지 않을 경우 에러가 표시되지 않고 빈 페이지가 표시된다.
`render` 메소드에서 에러가 발생하면 컴포넌트가 unmount 된다.
`render` 메소드에서 발생하는 에러를 표시하기 위해서 에러 경계를 사용한다.

**에러 경계를 사용하는 코드**
```js
class ErrorBoundary extends React.Component {
 constructor(props) {
   super(props);
   this.state = { hasError: false };
 }

 static getDerivedStateFromError(error) {     
   // 다음 렌더링에서 폴백 UI가 보이도록 상태를 업데이트한다.
   return { hasError: true }; 
 }
  componentDidCatch(error, errorInfo) {
    // 에러 리포팅 서비스에 에러를 기록할 수도 있다.
   logErrorToMyService(error, errorInfo); 
 }

 render() {
   if (this.state.hasError) {     
     // 폴백 UI를 커스텀하여 렌더링 할 수 있다.
     return <h4>Something went wrong</h4>     
   }
   return this.props.children;
 }
}
```

`getDerivedStateFromError` 함수는 `render` 메소드에 에러가 있을 때 폴백 UI 인터페이스를 렌더링한다.
`componentDidCatch` 는 에러 리포팅 서비스에 에러 정보를 기록한다.

**CounterComponent에 에러 경계 적용하기**
```js
<ErrorBoundary>
  <CounterComponent/>
</ErrorBoundary>
```

* [맨 위로](#목차)
