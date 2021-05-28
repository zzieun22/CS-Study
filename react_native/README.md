- **작성자** : 박지은
- 리액트 네이티브(모던 자바스크립트 개발자를 위한 리액트 프로그래밍)

## 목차

[1. Node.js 환경설정 ](#Node.js환경설정)

[2. 리액트 입문](#리액트입문)

[3. 리액트컴포넌트만들기](#리액트_컴포넌트만들기)

[4. 리액트 네이티브](#리액트네이티브)

[5. firebase 연동](#firebase연동)

# Node.js환경설정



## Node.js와 환경설정

### Node.js 구조 

|     node .js 코어 라이브러리 (자바스크립트)     |
| :---------------------------------------------: |
|                 node.js 바인딩                  |
| V8 (자바스크립트 엔진)   /   비동기 I/O (C언어) |

- 서버사이드 자바스크립트 실행환경 

- 비동기 처리를 표준 api로 제공하여 실행 효율이 좋은 웹 앱플리케이션을 쉽게 만들고 사용할 수 있음 



### 편한 라이브러리와 간단한 사용 

npm을 이용하면 간단하게 라이브러리를 설치 할 수 있음 



## 패키지 매니저 npm

간단하게 라이브러리 설치와 제거를 할 수 있음 

npm으로 설지하는 각 라이브러리 



### 로컬모듈설치 

npm 표준 설정으로 현재 디렉터리에 라이브러리가 설치되는데 이렇게 설치되는 모듈을 "로컬모듈"

이라고 한다.

```
npm install requset
```

설치를 하고 실행한 디렉터리를 열어보면 node_modules;라는 이름의 디렉터리가 생성되어있으며, 해당 디렉터리 내부에 설치된 모듈이 다운되어있음 

### 전역설치

머신 전체에 공유할 수 있는 도구 또는 라이브러리 설치 

```
npm root -g
```

어떤 디렉토리에 설치되었는지 확인할 때 

```
npm install -g coffee-script
```

전역으로 설치 



### npm을 사용한 프로젝트 생성 

```
npm init
```

package.json이 만들어진다. 

**package.json** 는 npm으로 프로젝트를 관리하기 위한 전용 설정 파일이라고 할수있음 



프로젝트에서 사용할 라이브러리를 npm에서 설치할때 "**--save**" 또는 "**-S**"옵션을 붙여서 설치하면 package.json의존 모듈로써 설치한 모듈과 버전이 기록된다. 

"**dependencies**" 항목이 추가되어있고, 모듈과 버전이 적혀있음 



### npm을 사용해 스크립트 실행하기

```
"scripts": {
	"start": "node index.js",
	"check": "node-v"
}
```

start 엔트리 추가 후 `npm run start` 명령어 실행하면 package.json의 scripts/start에 작성된 셀 명령어가 실행된다.(`node index.js`)





### 웹 어플리케이션 구조

웹서버는 인터넷으로 연결된 수많은 웹 클라이언트(브라우저) 에서 접속을 받고 통신을 시작한다. 이때 통신에서 사용되는 규약이 바로 HTTP이다. 

- HTTP통신은 웹 브라우저가 웹서버에 요청하면 웹서버가 웹 브라우저에게 응답해주는 구조 

- HTTP 통신은 stateless통신으로 응답하는 순간 접속이 종료된다. > 누가 접속했는지 , 이전사이트 어떤페이지 봤는지 식별 불가능 하다.===>>> 그래서 **쿠키** 기능이 등장 (웹 브라우저 내에 쿠키를 저장한다.)



## 바벨

모던자바스크립트 코드를 기존의 자바스크립트로 변환해주는 트랜스 다목적 컴파일러



#### 바벨설치

바벨 기본세트와 ES2015 프리셋 전역설치

```
npm install --global babel-cli babel-preset-es2015
```



### 바벨 전용 설정파일 만들기

매번 실행할때마다 명령어가 치기 귀찮으므로 **.babelrc**라는 파일을 만들어 해당파일에서 옵션 설정을 참조할 수 있다.

1. 프로젝트 초기화

   ```
   npm init -y (질문받지 않고 바로 생성)
   ```

2. 필요한 라이브러리설치

   ```
   npm install --save-dev babel-cli
   npm install --save-dev babel-preset-es2015
   ```

3. 바벨설정파일 .babelrc만들기

   .babelrc파일을만들어 아래 내용 입력

   ```
   { "presets : " ["es2015"] }
   ```

4. babel명령어로 JS파일 변환하기

   aa.js에 입력하여 실행 

   변환한 결과를 파일로 저장할때는 `--out-file` or `-o`옵션을 지정함 

   ```
   babel aa.js -o aa.out.js // 변환
   node aa.out.js // 변환된 프로그램 실행 
   ```

5. .package.json에 명령어 등록 

   ```
   {
   	"name": "babeltest",
   	...
   	"scripts": {
      		"build": "babel aa.js -o aa.out.js",
      		"start": "node aa.out.js",
     },
     ...
   }
   ```

   실행해보기 

   ```
   npm run build
   npm run start 
   ```

   > 4번과 같이 실행이 된다. 

6. 변경을 감시해서 자동으로 변환 

   감시모드는 프로그램을 저장할때마다 곧바로 저장해주는 기능 

   `-w` or `--watch`를 붙인다.

   ```
   {
   	"name": "babeltest",
   	...
   	"scripts": {
      		"build": "babel aa.js -o aa.out.jss",
      		"start": "node aa.out.js",
      		"watch" :"babel aa.js -w -o bmi.out.js"
     },
     ...
   }
   ```

   실행하기

   ```
   npm run watch
   ```

### 바벨의 다양한 기능 

#### 변환 결과를 dest(특정 디렉터리)에 저장하려면

a.js / b.js 

```
babel src -d dest // 실행 
//결과 
src/a.js -> det/a.js
src/b.js -> det/b.js
```



#### 주석 제거하여 간결하게 만드려면

`--conpact=true`라는 옵션을 추가

```
babel src --conpact=true -d dest
```



#### 디버깅 편리하게 하기

**소스맵** 기능 지원 

바벨로 변환하기 전의 소스 위치를 빠르게 파악할 수 있음 

`--source-maps` 옵션을 붙인다.

```
babel aa.js -o aa.out.js --source-maps
```



## 모듈 구조 이해

1. require 이해 

   라이브러리로 정의할 모듈에서 `module.exports라는 변수 내부에 공개하고 싶은 객체를 지정 . 그리고라이브러리를 사용하는 메인프로그램에서 require()를 통해 모듈로 정의한 객체를 읽어들이는 구조

   calaculator_module.js

   ```
   funcation add(a,b){
   	reutrn a+b
   }
   function mul(a,b){
   	return a*b
   }
   
   //외부에 공개
   module.exports = {
   	'add';add,
   	'mul':mul
   }
   ```

   main.js

   ```
   const calculator = require('./calculator_module.js')
   console.log(calculator.add(3,5))
   ```

2. es5의 import , export기능 

   ```
   import {add,mul} from './calculator_module.js'
   ```

   

# 리액트입문

### 리액트 프로젝트 만들기

https://reactjs-kr.firebaseapp.com/tutorial/tutorial.html 참조

1. 설치된 [`Node.js`](https://nodejs.org/en/)가 최신 버전인지 확인해보세요.
2. 새로운 프로젝트를 생성하기 위해 [설치 방법](https://reactjs-kr.firebaseapp.com/docs/installation.html#creating-a-new-application)을 따르세요.

```
$ npm install -g create-react-app
$ create-react-app my-app
```

1. 새 프로젝트의 `src/` 폴더에 있는 모든 파일들을 삭제해주세요. (폴더 안의 내용만 삭제하되 폴더는 삭제하지 마세요)

```
$ cd my-app
$ rm -f src/*
```

1. [이 CSS 코드](https://codepen.io/gaearon/pen/oWWQNa?editors=0100)를 `src/` 폴더에 `index.css` 파일로 추가해주세요.
2. [이 JS 코드](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)를 `src/` 폴더에 `index.js` 파일로 추가해주세요.
3. `src/` 폴더에 있는 `index.js`의 최상단에 아래 세 줄을 추가해주세요.

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
```

이제 프로젝트 폴더에서 `npm start` 명령어를 실행하고 브라우저에서 `http://localhost:3000`를 여세요. 빈 틱택토 필드를 볼 수 있습니다.

-----------------------

--이전에 

### 리액트 기본적인 사용방법

html로 실행해보기 

index.html

```react
<!DOCTYPE html><html>
<head>
    <meta charset="utf-8"> 
    <!--(1)-->
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script> 
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
</head>
</html><body>
    <!--(2)-->
<div id = "root"></div>
    <!--(3)-->
<script type="text/babel">
ReactDOM.render(
    <h1> hello.world </h1>,
    document.getElementById('root')
)
</script>
</body>

```

**(1)**

리액트/바벨 라이브러리 읽어들이고 있음 

**(2)**

id =root를 사용해 자바스크립트에서 쉽게 참조할 수 있게 만듦

**(3**)

자바스크립트 정의

- JSX라는 자바스크립트 확장언어를 사용 

- text/javascript 대신 text/babel이라고 지정 > 이처럼 사용하면 바벨을 사용해 스크립트를 변환할 것이다 라는 의미 , 실행될때 자바스크립트 코드로 변환된다. 
- DOM 출력 
  - 리액트에서 DOM출력할때는 ReactDOM.render()메서드를 사용한다. 
  - 첫번째 매개변수에는 `    <h1> hello.world </h1>,` 랜더링할 내용을 넣고 / 두번재 매개변수에 출력대상 DOM요소를 지정한다. >> 이걸 랜더링 이라고함 



## 리액트와 JSX의 관계

### 태그 내부에 변수를 넣는 법 

```react
<tag>..{value} ... </tag>
```

```react
<!DOCTYPE html><html>
<head>
    <meta charset="utf-8"> 
    <!--(1)-->
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script> 
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
</head>
</html><body>
<div id = "root"></div>
<script type="text/babel">

const item = "SD카드"
const value = 12000
const msg = <h1> {item} - {value}원</h1>
const elm = document.getElementById("root")
ReactDOM.render(msg, elm)
</script>
</body>
```



### 태그의 속성값에 변수를 넣는 법 

```react
<tag attr={value}...</tag>
```

### JSX 주의사항 

```react
function getDom(){
	return
	<div><p>안녕하세요</p></div>
} // 오류발생한다. 제대로 HTML태그 인식 못함 
```

```react
function getDom(){
	return(
	<div><p>안녕하세요</p></div>
	)
} // 범위를 소괄호로 감싸서 명시적으로 지정해준다. 
//** 연속적으로 작성못함 하나의 dom요소만 적어야한다.
```



```react
<!DOCTYPE html><html>
<head>
    <meta charset="utf-8"> 
    <!--(1)-->
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script> 
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
</head>
</html><body>
<div id = "root"></div>
<script type="text/babel">


ReactDOM.render(
    getDOM(),
    document.getElementById('root')
)

function getDOM(){
    return (
        <div>
            <p>안녕하세요</p>
            <p>저는 지은입니다</p> 
        </div>
    )
}
</script>
</body>

```



### JSX로 스타일 속성 지정

아래처럼 **객체**로 지정한다.

```react
const obj = { prop1:value1, prop2:value2, prop3:value3...}
const dom = <tag style={obj}> ... </tag>
```



```react
<!DOCTYPE html><html>
<head>
    <meta charset="utf-8"> 
    <!--(1)-->
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script> 
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
</head>
</html><body>
<div id = "root"></div>
<script type="text/babel">


ReactDOM.render(
    getDOM(),
    document.getElementById('root')
)

function getDOM(){

    const css1 = {
        "color": 'red',
        "background-color": '#f0f0ff',
        "font-size": '2em"'
    }

    const css2 = {
        "color": 'blue',
        "background-color": '#fff0f0',
        "font-size": '2em"'
    }

    return(
        <div>
            <p style={css1}> 안녕하세요</p>
            <p style={css2}> 안녕하세요</p>
        </div>
    )
}
</script>
</body>
```



### 변수 값은 자동으로 이스케이프 처리

"<", ">" 는  &lt , &gt 로 자동으로 변환된다.

> 보안문제 (XSS)를 방지할 수 있다. 



## 가상 DOM

### 가상DOM이란 ?

DOM의 상태를 메모리위에 올려두고 DOM변경이 있을 때만 해당 변경을 반영한다.

```react
<!DOCTYPE html><html>
<head>
    <meta charset="utf-8"> 
    <!--(1)-->
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script> 
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
</head>
</html><body>
<div id = "root"></div>
<script type="text/babel">

setInterval(showClock, 1000)
function showClock() {
    const d = new Date()
    const hour = d.getHours()
    const min =d.getMinutes()
    const sec = d.getSeconds();
    const elem = <div> {hour} : {min} : {sec} </div>
    const root = document.getElementById('root')
    ReactDOM.render(elem,root);
}

</script>
</body>
```

Dom의 일부만 변경됨 

![image](https://user-images.githubusercontent.com/36434665/116775600-c2854280-aa9e-11eb-92ce-6c40b0f52cee.png)

전체를 변경하는 것이 아닌 변경할 부분을 찾아 일부만 변경한다. 따라서 화면 처리속도가 비약적으로 빠르다.



## 컴포넌트 만들기(기초)

컴포넌트는 특정 기능을 가진 범용적인 부품을 나타내는 용어. 범용적인 컴포넌트를 만들어 재사용 가능하게 한다. 



### 리액트를 이용해 컴포넌트를 만드는과정

JSX를 반환하는 함수를 정의하기만 하면 된다. 

ex> Hello 라는 컴포넌트를 정의한다. 매개변수로 전달받은 props의 props.type을 `<h1>` 태그로 감싸서 출력하는 예 

```react
function Hello(props){
   // ..중간에 필요한 기능을 넣어도 된다.
	return <h1>{props.type}</h1>
}
```

 한번 이렇게 컴포넌트를 정의하면 JSX태그처럼 사용할 수 있다. 

```react
//Hello컴포넌트 사용하기
const dom = <div>
	<Hello type = "good morning" />
	<Hello type = "good afternoon" />
	<Hello type = "good evening" />
</div>
     
ReactDOM.render(dom.document.ElementById('root'))
```

![image](https://user-images.githubusercontent.com/36434665/116775966-037e5680-aaa1-11eb-9573-81b1ddfb955c.png)

요래된다.

이 props.type  , props.from 으로 포인트를 확장 할 수 있다. 이때 첫번째 매개변수는 객체 자료형이며, 해당 객체의 프로퍼티가 태그의 속성을 나타낸다. 

```react
<Hello type = "hello" from = "jieun" />
Hello({"type" : "hello", "from" : "jieun"}) 
//위 아래가 같은 의미 
```



### 조금 더 복잡한 컴포넌트의 경우 

복잡한 컴포넌트를 정의할 때 함수 하나만으로는 어려울때가 있다. 리액트는 복잡한 타입의 컴포넌트를 정의할때 ES5에 추가된 class구문을 사용 

```react
<!DOCTYPE html><html>
<head>
    <meta charset="utf-8"> 
    <!--(1)-->
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script> 
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
</head>
</html><body>
<div id = "root"></div>
<script type="text/babel">
// 클래스로 컴포넌트를 정의 
class Hello extends React.Component {
    render(){
        return <h1>{this.props.type}</h1>
    }
}
// function Hello(props){
// 	return <h1>{props.type}</h1>
// }

const dom = <div>
	<Hello type = "good morning" />
	<Hello type = "good afternoon" />
	<Hello type = "good evening" />
</div>
     
ReactDOM.render(dom,document.getElementById("root"))
</script>
</body>

```

1. **React.Component**라는 리액트의 기본적인 컴포넌트 클래스를 상속받는 부분이 제일 중요한 부분! 

2. **render()**메서드를 정의했는데, render() 메서드의 반환값이 컴포넌트의 출력내용이된다. 

3. 컴포넌트를 사용할때의 태그 요소는 **this.props**라는 객체 자료형에 들어있다. (this.props.type)

### 리스트 컴포넌트 만들기 

**ui li**요소를 사용해 리스트를 표현한다. 

```
<!DOCTYPE html><html>
<head>
    <meta charset="utf-8"> 
    <!--(1)-->
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script> 
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
</head>
</html><body>
<div id = "root"></div>
<script type="text/babel">

class RList extends React.Component {
    render() {
        const items = this.props.items.split(",")
        const itemsObj = items.map(
            (e) => {
                return <li>{e}</li>
            })
            let title = this.props.title
            if(!title) title = "LIST"

            return (<div>
                <h3> {title} </h3>
                <ul> {itemsObj} </ul>
                </div>)
    }
}
const dom = <RList title = "Colors" items = "Red,Green,Blue,White" /> 
ReactDOM.render( dom,document.getElementById("root"))
</script>
</body>

```

![image](https://user-images.githubusercontent.com/36434665/116777111-90c4a980-aaa7-11eb-9bc0-bc7babcb2684.png)

이렇게 쉽게 목록을 만들 수있음 

### 화살표 함수로 컴포넌트 정의

```react
const Test = (props) => (
	<div>
		<h1>{props.title}</h1>
	<div>
)
```



## 컴포넌트 만들기

### 컴포넌트 상태 관리하기 

기초에서 배운 것은 상태를 가지지않는 stateless컴포넌트였음 

우리는 그것에서 더 나아가 상태를 가지거나 외관상 크게 변화하는 컴포넌트의 경우 상태를 갖고 관리해야한다.

상태를 가지게 하려면 ? > 값을 기억해야함 **state 객체** 가 값을 기억한다.

**state 특징 및 사용하기**

state는 한번 값을 설정한 이후 값을 변경할때 setState()메서드를 사용해야 변경된다.

초기화하기

```react
class <컴포넌트의 이름> extends React.Component {
    constructor(props) {
        this.state = {<초깃값>}
    }
 ....
 
```

값 변경하기 

```react
this.setState({<이름> : <새로운값>})
```

ex> 시계 컴포넌트 만들기 

```react
<!DOCTYPE html><html>
<head>
    <meta charset="utf-8"> 
    <!--(1)-->
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script> 
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
</head>
</html><body>
<div id = "root"></div>
<script type="text/babel">

class SClock extends React.Component {
    constructor(props) {
        super(props)
        this.state ={
            now:(new Date())
        }
        setInterval(e=>{
            this.setState({now: (new Date())})
        }, 1000)
    }
    render() {
        const now = this.state.now
        const hh = this.fmt(now.getHours())
        const mm = this.fmt(now.getMinutes())
        const ss = this.fmt(now.getSeconds())
        return (<div>{hh}:{mm}:{ss}</div>)
    }

    fmt(v){
        const s = "00" + v
        return s.substr(s.length - 2 , 2)
    }
}
const dom = <div><SClock /></div>
ReactDOM.render( dom,document.getElementById("root"))
</script>
</body>

```

state 상태를 매 시간마다 바꾼다. setstate()를 통해서 



## 이벤드 구조와 구현 

### 클릭이벤트 

```react
<div onClick={clickHandler}> Clicke Me </div>

//clickHandle 이거에 대한 이벤트 정의하면됨 
```

### 클릭했을때 클래스 메서드 호출

클릭했을때 this를 바인드해야 인식 가능하다. 

```
 this.clickHandler = this.clickeHandler.bind(this)
```



### render 메서드에서 이벤트 정의

```react
class <컴포넌트 이름> extends React.component {
	render(){
		const handeler = (e) => alert('hello')
		return <button onClick={handler}>Click</button>
	}
}
```



## 리액트 도구를 사용한 자동빌드

지금까지는 자바스크립트 라이브러리를 읽어드렸지만 컴파일하는데 시간이걸림 

그래서 컴파일 해두는 방법이 있다. 



### create-react-app 설치

```
npm install -g create-react-app
//-g옵션 > 전역모듈 
create-react-app 내프로젝트이름 
cd 내프로젝트이름 
npm start 
```

## 프로젝트 실행 

해당 디렉터리 내부에 파일이 압축되어 생성 

```
npm run build
```

빌드가 제대로 되었는지 확인하려면 웹서버가 필요함 서버 설치 

```
npm install -g serve 
```

웹서버 실행 

```
server -s build
```



## 웹팩으로 리소스 파일 변환하기

### 웹팩이란? 

자바스크립트 또는 css등의 리소스 파일을 하나로 합쳐주거나 , jsx로 작성된 파일을 변환하는 도구 

최적의 형태로 변환해준다. 



### 웹팩설치

```
npm install -g webpack
```

#### 사용예시 

```
webpack aa.js out/aa.js 
#웹팩으로 말기 
node out/aa.js
#실행보변 파일이 변환되어있다. 
```

### 설정파일 만들기

`webpack.config.js`라는 설정파일 만들고 작업 지정을 한다. 

```
module.exports = {
	entry : '/main.js',
	output: {
		filename : 'out/aa/js'
	}
}
```

```
webpack
#웹팹 실행 
node out/aa.js
#결과 확인 
```

```
webpack --config webpack.config.js 
# 옵션 붙여서 설정파일 지정할 수 있다.
```



# 리액트_컴포넌트만들기





# 리액트네이티브

리액트 네이티브는 스마트폰 선능을 고려해서 os네이티브로 제공되는 요소들을 사용해 UI를 구성한다.

## 안드로이드 개발 설정 

- 안드로이드 스튜디오 설치 

- SDK 설정 
- 리액트 네이티브는 안드로이드 6.0 이상의 SDK가 설치되어있어야 한다. 
- 안드로이드 개발자옵션 디버그 활성화 한 뒤 usb안드로이드 장치와 컴퓨터 연결 
- 안드로이드 기기를 연결한 뒤 디버그를 할 수 있게 명령어 실행 adb 

**vscode**

```
npm install -g react-native-cli
```



```
react-native init 만들어질프로젝트이름
```

필요한 리액트 네이티브 앱 개발 요소들 설치 

**안드로이드 스튜디오** 

1. 내가 프로젝트의 android에 들어가기

![image](https://user-images.githubusercontent.com/36434665/117105994-0dae9680-adba-11eb-9c9b-1b37c958363d.png)

2. 우린 이버전의 sdk를 깔아야한다. 

   ![image](https://user-images.githubusercontent.com/36434665/117106098-39ca1780-adba-11eb-97b4-958ab80040a5.png)

3. sdk 매니저에서 경로 확인 후 환경변수 설정 

   ![image](https://user-images.githubusercontent.com/36434665/117106586-16539c80-adbb-11eb-91b7-ea00c31fab9e.png)

   ![image](https://user-images.githubusercontent.com/36434665/117106768-629edc80-adbb-11eb-864d-0dc597d28c5c.png)

4. 애뮬레이터, 디바이스 연결하기

   애뮬레이터 api버전이 sdk버전하고 맞아야한다. api 29로 깔기 

   ![image](https://user-images.githubusercontent.com/36434665/117107907-5c116480-adbd-11eb-8948-c04182815029.png)

avd 에 들어가 애뮬레이터 실행 or 실제 안드로이드 연결 

5. 실행하기 

   **vscode**

   ```
   react-native run-android
   ```

   sdk 버전이 맞아야한다. 

6. 계속 오류가 난다.

![1620203279586](https://user-images.githubusercontent.com/36434665/118133958-5ad6dc00-b43c-11eb-90ba-515e5acd3698.png)

```
> Task :app:processDebugMainManifest FAILED
11 actionable tasks: 3 executed, 8 up-to-date

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:processDebugMainManifest'.
> com.android.manifmerger.ManifestMerger2$MergeFailureException: java.io.FileNotFoundException: D:\workspace_react\saessak\android\app\build\intermediates\navigation_json\debug\navigation.json (������ ������ ã�� �� �����ϴ�)

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 21s

error Failed to install the app. Make sure you have the Android development environment set up: https://reactnative.dev/docs/environment-setup.
Error: Command failed: gradlew.bat app:installDebug -PreactNativeDevServerPort=8081

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:processDebugMainManifest'.
> com.android.manifmerger.ManifestMerger2$MergeFailureException: java.io.FileNotFoundException: D:\workspace_react\saessak\android\app\build\intermediates\navigation_json\debug\navigation.json (������ ������ ã�� �� �����ϴ�)

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 21s
```

gradle문제인가 /  에뮬레이터도 새로 다시 깔아봄 /  node.js도 다시깔아봄  >> 안됨 

삽집 + 구글링 하다가 알아내서 성공했다 

https://stackoverflow.com/questions/64333649/what-is-navigation-json-in-android-studio-4-1

참고 

```

Deprecated Gradle features were used in this build, making it incompatible with Gradle 7.0.
Use '--warning-mode all' to show the individual deprecation warnings.
See https://docs.gradle.org/6.4.1/userguide/command_line_interface.html#sec:command_line_warnings

BUILD SUCCESSFUL in 2m 32s
25 actionable tasks: 25 executed
info Connecting to the development server...
8081
info Starting the app on "emulator-5554"...
Starting: Intent { cmp=com.saessak/.MainActivity }
PS D:\workspace_react\saessak> 

```

**gradle-wrapper.properties 수정**

```
distributionUrl=https\://services.gradle.org/distributions/gradle-6.4.1-all.zip
```

**build.gradle 수정**

```
   dependencies {
        classpath("com.android.tools.build:gradle:4.0.2")
    }
```

**애뮬레이터에서 오류가 난다면? **

```
react-native start
```

실행해보기 



7. 성공

![image](https://user-images.githubusercontent.com/36434665/117120825-c7affd80-adce-11eb-98a0-c24f21958c61.png)

### 실시간 로딩 

hot reloading 을 사용하기 위해서는 명령어를 입력 해야 한다.

```
adb devices //기기 이름 확인 
adb -s <device name> reverse tcp:8081 tcp:8081 
```







## 바코드 스캔하기 

### react-native-camera-kit 라이브러리 설치

```
npm install react-native-camera-kit --save
```

https://www.toptal.com/react-native/react-native-camera-tutorial

###  카메라 권한 허용 

veganVapp > android > app > src > main > `AndroidMnifest.xml`

`AndroidMnifest.xml` 에 아래 코드를 추가.

```bash
+    <uses-permission android:name="android.permission.CAMERA" />
+    <uses-permission android:name="android.permission.RECORD_AUDIO"/>
+    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
+    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```



build.gradle 에 추가

```react
defaultConfig {
    ...
    missingDimensionStrategy 'react-native-camera', 'general'
    ...
 }
```

필요 라이브러리 설치

```
npm add @react-navigation/native

npm add @react-navigation/stack

npm add react-native-reanimated react-native-gesture-handler react-native-screens react-native-safe-area-context @react-native-community/masked-view
```



 **앱 실행 되고 Solved: Unable to load script from assets ‘index.android.bundle’ 오류** 

```react

//D:\workspace_react\saessak\android 에서 
./gradlew clean

//루트에서 
react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/ index.android.bundle --assets-dest android/app/src/main/res
```



### RNCamera의 종속성 설치

설정에는 최소 JDK 버전 1.7 (사용할 가능성이 가장 높음)이 필요하며 Android를 사용하는 `buildToolsVersion`경우 25.0.2보다 최신 버전 이 필요합니다 . (확실히 [문서에 더 자세한 최신 목록이](https://github.com/react-native-community/react-native-camera#requirements) 있습니다.)



App.js

```react
import 'react-native-gesture-handler';
import * as React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import { Home, BarcodeScanner} from './src/screen'


const navOptionHandler = () => ({
  headerShown: false
})


const StackApp = createStackNavigator();


export default function App() {
  return (
    <NavigationContainer>
      <StackApp.Navigator initialRouteName="Home">       
        <StackApp.Screen name="Home" component={Home} options={navOptionHandler} />
        <StackApp.Screen name="BarcodeScanner" component={BarcodeScanner} options={navOptionHandler} />
      </StackApp.Navigator>
    </NavigationContainer>
  );
}
```

/src/screen/index.js

```
export * from "./Home"
export * from "./BarcodeScanner"
```

/src/screen/Home.js

```
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 *
 * @format
 * @flow strict-local
 */

import React, { Component } from 'react';
import { Button, Alert, View, SafeAreaView, PermissionsAndroid, Platform } from 'react-native';


//default는 App.js에서만 사용해야 하는 듯 
export class Home extends Component {
    /**
 * 바코드 스캔
 */
    scanBarcode = () => {

        var that = this;
        //To Start Scanning
        if (Platform.OS === 'android') {
            async function requestCameraPermission() {
                try {
                    const granted = await PermissionsAndroid.request(
                        PermissionsAndroid.PERMISSIONS.CAMERA, {
                        'title': '카메라 권한 요청',
                        'message': '바코드를 스캔하기 위해 카메라 권한을 허용해주세요.'
                    }
                    )
                    if (granted === PermissionsAndroid.RESULTS.GRANTED) {
                        //If CAMERA Permission is granted

                        //TODO BarcodeScanner.js를 호출하세요 
                        //this가 아니라 that을 사용해야 함 
                        that.props.navigation.navigate('BarcodeScanner', { onGetBarcode: that.onGetBarcode })
                    } else {
                        alert("카메라 권한을 받지 못했습니다.");
                    }
                } catch (err) {
                    alert("카메라 권한 오류: ", err);
                    console.warn(err);
                }
            }
            //Calling the camera permission function
            requestCameraPermission();
        } else {
            that.props.navigation.navigate('BarcodeScanner', { onGetBarcode: that.onGetBarcode })
        }
    }

    onGetBarcode = (barcodeValue) => {
        console.log("barcode value: ", barcodeValue);
        //아래 함수의 파라미터로 문자열만 넘길 수 있음. barcodeValue가 문자열처럼 보이지만 문자열이 아닌 듯. String()는 작동하지 않음. JSON.stringify()는 작동함 
        Alert.alert("barcode value: ", barcodeValue);
    };


    render() {
        return (
            <View style={{ flex: 1 }}>
                <SafeAreaView style={{ flex: 1, justifyContent: "center",  alignItems: "center"}}>
                    <Button
                        title="바코드 스캔"
                        onPress={() => this.scanBarcode()}
                        />
                </SafeAreaView>
            </View>
        );

    }

}
```

/src/screen/BarcodeScanner.js

```
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 *
 * @format
 * @flow strict-local
 */

import React, { Component } from 'react';
import { View, PermissionsAndroid, Platform } from 'react-native';
import { CameraKitCameraScreen, } from 'react-native-camera-kit';

var isFirstGet = true;
//default는 App.js에서만 사용해야 하는 듯 
export class BarcodeScanner extends Component {

  constructor(props) {
    super(props);
  };


  componentDidMount() {
    //isFirstGet의 이전 값이 남아 있어서 다시 실행할 때 true를 할당해야 함 
    isFirstGet = true;
  }

  componentWillUnmount() {

  }


  /**
 * 바코드 스캔
 */

  onBarcodeScan(barcodeValue) {
    console.log("onBarcodeScan")
    if (!isFirstGet) {      
      return
    }

    isFirstGet = false
    this.props.route.params.onGetBarcode(barcodeValue);
    //TODO 필요한 부분 구현하세요
    this.props.navigation.navigate('Home')
    
    //called after te successful scanning of QRCode/Barcode
    console.log("scanned barcode value: " + barcodeValue)
  }

  //TODO Home.js로 이동시키세요 
  checkCameraPermission() {

  }


  render() {
    return (
      <View style={{ flex: 1 }}>
        <CameraKitCameraScreen
          showFrame={true}
          //Show/hide scan frame
          scanBarcode={true}
          //Can restrict for the QR Code only
          laserColor={'blue'}
          //Color can be of your choice
          frameColor={'yellow'}
          //If frame is visible then frame color
          colorForScannerFrame={'black'}
          //Scanner Frame color
          onReadCode={event =>
            this.onBarcodeScan(event.nativeEvent.codeStringValue)
          }
        />
      </View>
    );
  }
}

```

**오류 해결** 

1. 캐시 재설정 

   ```
   rm -rf node_modules/ 
   npm cache clean && npm install && 
   npm start -- --reset-cache
    
    react-native start --reset-cache
   ```

2. npm install react-native-webview --save

3. build.gradle의 compileSdkVersion을 29로 편집하고 buildToolsVersion을 "29.0.3"으로 편집합니다.

4. cd android && gradlew clean && gradlew 빌드

5. 반응 네이티브 실행 Android로 실행



## 카메라 찍기 

### 설치

```
npm install react-native-camera --save
```









## firebase연동 

### 설치

react-native-firebase 패키지에서 제공하는

- react-native-firebase/auth
- react-native-firebase/firestore
- react-native-firebase/storage
  등을 사용하려면
  react-native-firebase/app 모듈 설치가 되어있어야한다.

```
# Using npm
npm install --save @react-native-firebase/app
```



### firebase

​	**안드로이드 설정**

1. firebase 콘솔에서 android 앱 추가
   firebase console > project settings > General > Your apps > 안드로이드 아이콘 클릭

   packagename 입력(`android/app/src/main/AndroidManifest.xml` 에 package에 있음 )

   ![image](https://user-images.githubusercontent.com/36434665/118136431-1436b100-b43f-11eb-90ac-39dd090cb1c0.png)

2. `google-services.json` 다운
   `android/app`에 다운받은 `google-services.json`를 넣기

   `android/app/google-services.json`  .gitignore에 추가 

   ![image](https://user-images.githubusercontent.com/36434665/118136753-68da2c00-b43f-11eb-8f5d-4d3e2dab46fa.png)

3. `android/build.gradle` 에 추가

   ```
   buildscript {
     repositories {
       // Check that you have the following line (if not, add it):
       google()  // Google's Maven repository
     }
     dependencies {
       ...
       // Add this line
       classpath 'com.google.gms:google-services:4.3.6' // 추가
     }
   }
   ```

   

4. `android/app/build.gradle` 추가 

   ```
   apply plugin: 'com.android.application'
   // Add this line
   apply plugin: 'com.google.gms.google-services'
   
   dependencies {
     // Import the Firebase BoM
     implementation platform('com.google.firebase:firebase-bom:28.0.0')
   
     // Add the dependency for the Firebase SDK for Google Analytics
     // When using the BoM, don't specify versions in Firebase dependencies
     implementation 'com.google.firebase:firebase-analytics'
   
     // Add the dependencies for any other desired Firebase products
     // https://firebase.google.com/docs/android/setup#available-libraries
   }
   ```

5. 설정 후 동기화 

   ```
   gradlew clean
   ```

   오류남 (node_modules에 firebase가 없는듯?)

   ```
   Error: Unable to resolve module react-native-firebase from D:\workspace_react\saessak\src\screen\CameraRoll.js: react-native-firebase could not be found within the project or in these directories:
     node_modules
   
   If you are sure themodule exists, try these steps:
    1. Clear watchman watches: watchman watch-del-all
    2. Delete node_modules(rm -rf  node_modules/) and run npm install
    3. Reset Metro's cache: npm start --reset-cache
    4. Remove the cache: rm -rf /tmp/metro-*
   ```

   

### storage, database 사용

설치 

```
# Install the storage module
npm add @react-native-firebase/storage
# Install the database module
npm add @react-native-firebase/database
```



스토리지 규칙이다. auth된 사용자만 써야한다는 규칙 

```
Cloud Storage 위치 설정
기본적으로 이 규칙은 인증된 사용자의 모든 읽기 및 쓰기를 허용합니다.

데이터 구조를 정의한 후 데이터에 보안을 적용하는 규칙을 작성해야 합니다.자세히 알아보기

service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

테스트를 하기위해 잠시 그 규칙 해제 >>> **돌려놓기**

```
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read, write
    }
  }
}
```

한국은 asia-northeast3라고 한다. 설정 

![image](https://user-images.githubusercontent.com/36434665/118230481-b484e800-b4c8-11eb-83b1-d9525a041945.png)



```
import firebase from '@react-native-firebase/storage'
```

나는 `import firebase from 'react-native-firebase` 이렇게 하면 오류남 .. ? 이유는 모름 

그래서 따로 storage를 지정



```

  const uploadImage = (source, imageUri) => {
    const ext = imageUri.split('.').pop(); // Extract image extension
    const filename = `${uuid()}.${ext}`; // Generate unique name
    const imgRef = firebase.storage().ref(`saessak/${filename}`);
    const unsubscribe = imgRef.putFile(imageUri)
      .on(
        firebase.storage.TaskEvent.STATE_CHANGED,
        async snapshot => {
          let state = {};
          state = {
            ...state,
            progress: (snapshot.bytesTransferred / snapshot.totalBytes) * 100 // Calculate progress percentage
          };
          if (snapshot.state === firebase.storage.TaskState.SUCCESS) {
            console.log('upload success');
            // unsubscribe the event
            unsubscribe();
            // update the image url
            let url;
            await imgRef.getDownloadURL()
            .then((response) => {
              console.log('get url response', response);
              url = response;
            })
            .catch(error => {
              console.log('Failed to get url', error);
            })
            // update user info, avatar, and name
            console.log('user avatar url', url);
            updateAvatarState({ userId, avatarUrl: url });
            // refresh the screen
            setAvatarUrl(url);
          }
        },
        error => {
          console.log('AccountEditScreen uploading error', error);
          // alert for failure to upload avatar
          Alert.alert(
            t('AccountEditScreen.updateErrorTitle'),
            t('AccountEditScreen.updateError'),
            [
              { text: t('confirm') }
            ],
            { cancelable: true },
          );
        }
      );
  };
```

- Storage의 reference를 가져오는 부분은 Firestore와 동일합니다.
  `const imgRef = firebase.storage().ref(`avatar/${filename}`);`
  위 Storage구조를 보면 최상위 디렉터리 밑에 `avatar`라는 폴더가 있습니다. `imgRef`는 그 폴더 밑에 임의로 생성한 이미지 이름을 가리키게 됩니다.
- `putPile`함수를 이용하여 이미지를 Storage에 저장합니다.
- 이미지를 Storage에 저장만 하고 끝나는게 아닙니다. 사용자별로 저장된 이미지의 위치를 DB에 기록해서 필요할 때마다 불러와야 합니다. 그래서 putFile이 이미지 업로드할 때까지 기다립니다.
- `firebase.storage.TaskState.SUCCESS`부분에서 업로드가 성공적이면, Storage에 저장된 이미지의 다운로드 경로를 가져옵니다. `imgRef.getDownloadURL()`
- 마지막으로 이미지 경로를 제대로 가져오면 사용자 정보(DB)에 저장된 아바타 이미지 경로를 저장합니다.

```
import database from '@react-native-firebase/database';
async function data(params) {
  const ref = database().ref();
  let data = await (await fetch(ref + params + '.json')).json();
  return data;
}

export default data;
```





### imagePicker

```
npm install --save react-native-image-picker
```

카메라를 이용해 사진을 찍거나 카메라 롤에 저장된 사진에 접근할 수 있다. 

- Github: [react-native-image-picker-example](https://github.com/dev-yakuza/react-native-image-picker-example)

  깃헙 소스에 있음 

#### 사용법 

```
import ImagePicker from 'react-native-image-picker';
```





















