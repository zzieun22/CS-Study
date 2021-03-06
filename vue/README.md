[nvm사용](nvm사용)

[vue-CLI](vue-CLI)

[ESlint](ESlint)

[Router](Router)

[환경 변수](환경변수)

[API구현](API구현)

[PROMISE](PROMISE)

[vuex](vuex)

[에러처리](에러처리)

[Eventbus](Eventbus)

[하이오더컴포넌트](하이오더컴포넌트)

[믹스인](믹스인)

[외부라이브러리모듈화 ](외부라이브러리모듈화 )

[단위테스트](단위테스트)

## nvm사용

https://github.com/nvm-sh/nvm

에서 설치 

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
```

vscode 에서 bash 로 바꾼 후 설치 



` vi ~/.bashrc` 로 들어가서 

```
# vi로 연 .bashrc 파일에 "i" 키를 입력하여 쓰기 모드로 진입합니다.
# 그리고 나서 아래 내용을 추가하고 ":"를 입력한 다음 "wq"를 입력하여 저장 후 종료합니다.
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm

```

입력 후 저장 

```
$ nvm install 10.16.3
```

입력하면 버전 변경된다. 



### new Project

새 프로젝트 만들기 

```
vue create

..
npm run serve 
```



src/App.vue

```
  created(){
   var a = 10;
  }
```

로 테스트 해보면

eslint 규칙으로 인해 오류가 난다. 

> 무시하고 앱 개발할 수 있게 설정 



1. 새파일만들고 vue.config.js (vue 설정파일)

   ```
   module.exports = {
       devServer: {
           overlay: false
       }
   }
   ```

   웹팩 데브서버에서 제공하는 오버레이 속성을 껐음 



## vue-CLI

```
npm i -g @vue/cli@3.2.1
```

cli 최신버전 설치 

3.2.1설치할거임 (현재 가장최신은 4.5.x이다.)

```
vue create vue-news
```

> 2.xx설치할때 `vue init webpack-simple vue-news   `요래썼었음 

 default 선택

```
npm run serve
```

로 실행해 보기 



### 3.xx와 2.xx의 차이점 

1. 명령어

   - 2.x : `vue init 템플릿이름 파일위치` 로 생성
   - 3.x : `vue create 플젝이름` 로 생성

2. 웹팩 설정 파일 

   - 2.x : `webpack.config.js` 를  노출함
   - 3.x : `webpack.config.js` 를 노출 안함 (라이브러리에서 알아서 처리) 별도의 내용으로 추가해야한다. 

3. 프로젝트구성

   - 2.x : 생성할때 node_modules 가 같이 설치 안됨 

     ​     `npm install`로 추가해줘야한다. 

     ​     깃헙에 있는 템플릿 그대로 다운로드 되는것 

   - 3.x :  생성할때 node_modules 가 같이 설치됨 

     ​        플러그인 기반으로 기능이 추가가 됨

4. ES6 

   - 2.x :  웬만하면 이해할수있음 
   - 3.x : 많이 이해하고 있어야한다. 축약문법 등등 

   

## ESlint

### ESlint 설정을 끄는 방법 

1. `/* eslint-disable */`를 컴포넌트 마다 넣어주는것 

   - 각 컴포넌트 마다 넣어주는건 비효율적임 ! 

2. `vue.config.js` 생성

   ```javascript
   module.exports = {
       lintOnSave: false //설정함
   }
   ```

   https://cli.vuejs.org/config/#lintonsave 참고





조건에 맞지않으면 error를 출력해라  

```
  "preittier/prettier": ['error', {
      printWidth: 80
    }]
```



### jsconfig.json

```
{
    "compilerOptions": {
      "baseUrl": ".",
      "paths": {
        "~/*": [
          "./*"
        ],
        "@/*": [
          "./src/*"
        ],
      }
    },
    "exclude": [
      "node_modules",
      "dist"
    ]
  }
```





## Router

###  라우터 구성 

1. **라이브러리 설치**

   ```
   > npm i vue-router --save
   ```

   ##### (TIP!!) package.json

   ```
     "dependencies": {
       "core-js": "^3.6.5",
       "vue": "^2.6.11",
       "vue-router": "^3.5.2"
     },
   ```

   - 웹을 실행시키는데 필요한 비즈니스 로직 또는 앱의 동작을 담당한다. 

   - 배포할때도 포함해야하는 라이브러리



2. **vue 설정** 

   `main.js`

   ```
   import Vue from 'vue'
   import App from './App.vue'
   import VueRouter from 'vue-router';
   Vue.config.productionTip = false
   
   Vue.use(VueRouter);
   
   const router = new VueRouter({
     routes : [
   		..
     ]
   })
   new Vue({
     render: h => h(App),
     router,
   }).$mount('#app')
   
   ```

   요래 생성할 수  있지만  정보가 많아졌을때 main.js 가 router 편향적인 설정파일이 될 수 있다. 

   **>> main.js**

   main.js는 기본적으로  애플리케이션의 플러그인 라이브러리 등 구조를 파악할 수 있는 것들이 다 들어있음 



3. **src/router/index.js 만들기**

   index.js

   ```javascript
   import Vue from 'vue'
   import VueRouter from 'vue-router';
   
   
   Vue.use(VueRouter);
   
   const router = new VueRouter({
     routes : [
   		{
               // url 주소
               path: '/',
               // url 주소로 갔을 때 표시될 컴포넌트
               component: '',
           },
           {
               path: '',
               component: '',
           },
           {
               path: '',
               component: '',
           },
     ]
   })
   ```

   `Vue.use(VueRouter)`

   vue.use 는 플러그인을 실행,초기화 하기위해서 필요한 코드 

   

   ** src 밑에 <u>views</u>라는 폴더를 만들어 각각 이동하는 페이지 역할을 하는 컴포넌트 구성하기

   >  vetur 플러그인 설치하면 `vue` 까지 입력하면 자동으로 틀이 생김 

   ![1625296876466](https://user-images.githubusercontent.com/36434665/124346613-d6722f80-dc1a-11eb-8a50-42e413335461.png)

   

   ```
   import {} from '../'
   ```

   ```
   import Vue from 'vue'
   import VueRouter from 'vue-router';
   import NewsView from '../views/NewsView.vue'
   import AskView from '../views/AskView.vue'
   import JobsView from '../views/JobsView.vue'
   
   Vue.use(VueRouter);
   
   const router = new VueRouter({
     routes : [
   		{
               // url 주소
               path: '/news',
               // url 주소로 갔을 때 표시될 컴포넌트
               component: NewsView,
           },
           {
               path: '/ask',
               component: AskView,
           },
           {
               path: '/jobs',
               component: JobsView,
           },
     ]
   })
   ```

   추가 완료

   

4. **main.js 로보내기** 

   라우터 폴더에서 main.js로 라우터를 넘겨줘야한다.

   es6의 import , export 를 쓴다. 

   router/index.js에 

   ```
   export const router = new VueRouter({ ....
   ```

   보내주면 

   

   main.js에서 가져올 수있음 

   ```
   import Vue from 'vue'
   import App from './App.vue'
   import { router } from './router/index.js'; // 여기
   Vue.config.productionTip = false
   
   new Vue({
     render: h => h(App),
     router  //여기
   }).$mount('#app')
   
   ```

   

   이렇게도 할 수 있음 

   ```
   export default new VueRouter();
   ```

   export: 라우터 인스턴스가 생성되면서 파일이 밖으로 나가게됨 

   default :  하나의 파일 변수가 나가게된다.

   

   ```
   export default new VueRouter({
       routes:[], //페이지 정보, 라우팅 정보를 담고 있다. 
   });
   ```

   ```
       routes:[
           {
               path: '/login',
               component: LoginPage, //이동했을때 페이지 컴포넌트
           },
           {
               path: '/signup',
               component: SignupPage, 
           }
       ],
   ```

5. **App.vue** 

   ```HTML
   <template>
     <div id="app">
       <router-view></router-view>
     </div>
   </template>
   ```

   `   <router-view></router-view>`는 url이 ask다 그러면 AskView.vue 가 뿌려짐 

   

   ex> 

   ```
   <template>
     <div id="app">
       <AskView></AskView>
     </div>
   </template>
   ```

   이렇게 되는것! 

   ![image](https://user-images.githubusercontent.com/36434665/124347075-6a44fb00-dc1d-11eb-880a-88acf85aceb3.png)




```js

{
      path: '/user/:id', //*****
      component: UserView,
    } //라우터 설정  id 값을 넘어오게 한다. 
```

```html
...
<small>{{ news.time_ago }} by
   <router-link v-bind:to="`/user/${news.user}`">{{ news.user }}</router-link> 
</small>
       ...
```

넘겨 줄 id 는 {news.user} 값

링크를 눌렀을때 

```
http://localhost:8080/user/yewenjie
```

위 url으로 이동하면서 param.id 값이 yewenjie를 가지게 된다. 



### 라우터 트랜지션 

https://vuejs.org/v2/guide/transitions.html

App.vue 에서 

```html
   <transition name = "fade"> 
      <router-view></router-view>
    </transition>
```

아래 style에 추가 

```css
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
```

tansition 태그에서 name 뒤에오는 fade가 css규칙에 prefix가 된다. 

fade 를 다른 값으로 바꿔도 됨 



### 코드 스플리팅 (lazy loading)

화면의 개수가 많아 졌을때 

모든 페이지 로딩은 시간이 많이 걸림 

원하는 페이지만 불러오고 나머지는 이동했을때만 불러오게 만들자!

> 초기에 앱 로딩되는 속도가 줄어든다. 

```
export default new VueRouter({
  routes: [
    {
      path: '/login',
      component: () => import('@/views/LoginPage.vue'), // 이렇게 할용 
      
    },
    {
      path: '/signup',
      component: () => import('@/views/SignupPage.vue'),
    },
  ],
});

```



### 리다이렉트 

**처음 진입 페이지 설정** 

처음 서비스가 실행 될때 특정 페이지로 가고싶다. 

```javascript
  routes: [
    {
        path: '/',
        redirect: '/login', ////요래
    }
    {
      path: '/login',
      component: () => import('@/views/LoginPage.vue'),
    },
    {
      path: '/signup',
      component: () => import('@/views/SignupPage.vue'),
    },
     {
    	path: '*' //위에 글을 제외한 나머지 모든글에 반영된다. 
     	component: () => import('@/views/NotFoundPage.vue'),
    }
  ],
```



**(TIP!!)** 컴포넌트 등록할때는 스크립트 단에는 파스칼방식인데 태그 등록할 때는 케밥 방식을 따른다. 

```
 <tool-bar></tool-bar> 
```

ctrl + alt 누르면 내용 볼 수 있음 (케밥으로 연결했을 때 )



#### 네비게이션 

** 헤더 컴포넌트를 만들어서 라우터 링크를 이용해서 페이지를 네비게이션 할 수 있는 방법 

```
<template>
  <div>
    <router-link to = "/news">News</router-link>
    <router-link to = "/ask">Ask</router-link>
    <router-link to = "/jobs">Jobs</router-link>
    <!-- 자동으로 a 태그로 전환된다. -->
  </div>
</template>

<script>
export default {

}
</script>

<style>

</style>
```



### history

url 에 #이 없어진다.

```
mode: 'history', // url 에 #이 없어진다. //'http://localhost:8080/#/'
//실제 서버에 올릴때 url에 대한 우회, 필터링을 넣어줘야한다. 
routes: [
    {
      path: '/',
      redirect: '/login',
    },
    {
      path: '/login',
      component: () => import('@/views/LoginPage.vue'),
    },
    {
      path: '/signup',
      component: () => import('@/views/SignupPage.vue'),
    },
    {
        path: '*'  
        component: () => import('@/views/NotFoundPage.vue'),
  
    }
  ],
```



#### scoped 

```
<style scoped>

</style>
```

해당 컴포넌트에만 적용되는 스타일 속성을 의미한다.



**헤더에 특정 라우트링크만 스타일 지정하고 싶을때**

![image](https://user-images.githubusercontent.com/36434665/124871308-dc8f5400-dffe-11eb-8dd6-57d9b8f15d43.png)

```
.header .router-link-exact-active {
  color: #35493e;
}
```



**활성화된 링크 제외 나머지는 다 하얗게 처리** 

```
.header .router-link-exact-active {
  color: #35493e;
}
.header a{
  color:white
}
```





## 환경변수 

.env 

vue-cli 3.0 부터 규칙 지정하면 자동 로드 된다. 

```
VUE_APP_ 
```

접두사가 붙는 변수는 자동 로드 됨 



`env.production ` : npm run build 실행했을때 바라본다.(빌드명령어 입력 시)

`env.development`  로컬에서 실행했을 때 바라본다.

`env` : 위에 2개 다 없으면 디폴트로 바라본다



### 컴포넌트 구성 

**views**컴포넌트는 페이지의 라우팅 관련된 정보만 들어가는게 좋다. 

> 데이터를 패치해오는 것들을 들어가는게 안좋다.

데이터를 불러오는건 별도의 컴포넌트로 관리해야한다. 



 

## API구현

axios 설치

```
 npm i axios --save
```



promise 기반으로 api를 제공한다.

​	`new Promise()`라는 객체를 반환해주고 .then.catch를 쓸수있다.

```
    axios.get('https://api.hnpwa.com/v0/news/1.json')
        .then(response => console.log(response))
        .catch(error => console.log(error))
```



### API공통화

**방법 1. axios 를 공통으로 사용하기위해 create 하여 빼보기** 

```vue
const instance = axios.create({
	baseURL : 'http://localhost:3000/'
})

function registerUser(userData){
	return instance.post('signup',userData);
}
```

로하면 

```
function registerUser(userData){
	const url = 'http://localhost:3000/signup';
	axios.post(url,userData);
}
```

와 같은 효과를 준다.



**방법2. api폴더 밑에 index.js 생성**

api모듈 만들기 

```javascript

//1. HTTP Request & Response 관련된 기본 설정 
const config = {
	baseUrl: ....
}

//2. API 함수들을 정리
function fetchinfoList(){
	return axios.get(`${baseUrl} ... `);
}

//3. 꺼내주기 
export {
	fetchinfoList
}
```

 

**tip !!** import ,export 

```
export {
	abc,
	해줘야 
}

import { abc } from xxx.js 가 가능하다.
```

이런식으로 export한 함수를  import해서 쓸수 있음 

```javascript
import { fetchinfoList } from '../api/index.js';

export default {
  created() {
    fetchinfoList()
      .then(response => console.log(response))
      .catch(error => console.log(error));
  }
}
```

--------------------------

`created` `beforeMount` 

데이터 요청할때 위 2개를 많이 쓴다. 



### this

```javascript
var a = 10;
window.a // 10
this // window 

```

```javascript
function sum(a, b){
	console.log(this); // window 
	return a + b;
}
```

```javascript
function Vue(el) {
	console.log(this); // 'Vue{}' 인스턴스를 정의한 객체 자체 (생성자)
	this.el = el
}

new Vue('#app');

```

```javascript
  console.log(this); // VueComponent{..}
    fetchNews()
      .then(function(response) {
         console.log(this); //undefined
        // 비동기 호출로 인해서 새로운 this가 생김 
      })
      .catch(error => console.log(error));
 ////////////////////////////////////////////////vs
 console.log(this); //VueComponent{..}
    fetchNews()
      .then(response => {
         console.log(this); //VueComponent{..}
        // es6를 사용하면 호출되는 this를 갖고온다.
      })
      .catch(error => console.log(error));
  }
```



## PROMISE

자바스크립트 비동기 처리에 사용되는 객체 



보통 서버에서 받아온 데이터를 화면에 표시할 때 사용 

```javascript
function getData(callback){
	return new Promise(function(resolve,reject)){
   axios.post('~~', param)
       .catch(function (err) {

        }).then(function (rs) {
            resolve(response);
        });
	}
}

getData().then(function(data){
	console.log(data);
});
```



### 프로미스 상태(states)

- Pending(대기) : 비동기 로직이 완료 x

  - `new Promise();` 메서드 호출 할 때 

- Fulfilled(이행) : 비동기 처리 완료되어 프로미스가 결과값 반환 

  ```javascript
  return new Promise(function(resolve,reject)){
  	resolve(); // 실행하면 이행 상태가 된다.
  });
  ```

- Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태

  ```javascript
  return new Promise(function(resolve,reject)){
  	......
  	reject(new Error("Request is failed"));
  });
  ```



### Promise chaining

`then()`으로 여러개 프로미스 사용할 수 있음 

```javascript
..()
.then(function(data){

})
.then(function(){

});
....

```



```javascript
//childComponents.vue
<template>
<div class="text" :class="{marquee:showTxt}">
    <div> {{this.firLine}} <br> 이렇게 말해보세요! </div>
    <span>
     	<div>“{{this.callName}},<br>&nbsp; {{this.secLine}}” </div>
    </span>
</div>
</template>
```



### async 

promise 의 .then .catch 와다르게 네트워크 비동기 요청에서만 처리 

일반 try catch 자바스크립트 코드 까지 예외처리 가능 (async 안에 사용 )

```js
import { handleException } from './utils/handler.js'
//....
try{
// ... 
}catch(error) {
	handleException(error);
	
}
```

`/utils/handler.js` 

```js
function handleExceptions(status){
 //..
}
```

로 공통으로 처리 가능 

## vuex

**설치** 

```
npm i vuex
```

vuex 는 **상태관리 도구**이다. 

여러 컴포넌트간에 공유되는 데이터 속성 



<u>store/index.js</u>

vuex는 플러그인 형태로 제공 

```javascript
Vue.use(Vuex); // 로 vuex사용 
```

```javascript
export const store = new Vuex.store({
 // 인스턴스를 내보낸다.
})
```

<u>main.js</u> 에 등록해줌 

```js
import store from './store/index.js';
```

```js
new Vue({
  router,
  store, // store 등록 // 원래 store: store 이지만 앞뒤가 같으니 생략가능 
  render: h => h(App)
}).$mount('#app')

```



**store 에 api 저장후에 view에서 불러오기** 

```js
state:{
    news: []
},
mutations: {
    SET_NEWS(state, news) {
       state.news = news;
    }
},
actions : {
    FETCH_NEWS() {
      fetchNews()
      .then(response => {
          console.log(response);
          context.commit('SET_NEWS', response.data); // api를 이용해서 mutation에 데이터를 넘길 수 있다. 
          state.news = response.data 
      })
      .catch(error => {
          console.log(error);
      });
    }
  },
```

1. vuex 에 action 호출하려면 dispatch api를 이용해서 데이터를 호출해야한다.

2. `context.commit`  api를 이용해서 mutation에 데이터를 넘길 수 있다. 

   >  ` context.commit('SET_NEWS', response.data);` SET_NEWS에 response.data를 넘겨주겠다.

   ![vuex](https://vuex.vuejs.org/vuex.png)

​	Actions 에서 commit을 해서 Mutations에 넘길 수 있다. 

3.   Mutations에서 state에 값을 받아와서 데이터를 넘겨줌 

   ```js
   SET_NEWS(state, news) {
          state.news = news;
   }
   ```

4. store를 사용하는 .vue 

   ```js
   this.$store.dispatch('FETCH_NEWS')
   ```

   로 불러와서 

   ```
   <div v-for="item in news">{{ this.$store.state.news }}</div>
   ```

   로 받아서 쓴다. 

   ​						 vuex

   View		   	 actions     <<<<<    API

   View    			mutations				API

   View	   <<<< state                        API

이런느낌?



### mapstate 

모듈화 , 간단하게 바인딩하는것 

```js
import { mapState } from 'vuex';
...mapState({
	ask: state => state.ask
})
```

### getters

더 간단하게!

computed와 동일한 속성 (store에서 사용 가능하다.)

store/index.js

```js
getters: {
	fetchedAsk(state){
        return state.ask
    }
},
```



```js
import { mapgetters } from 'vuex';
....
computed: {
    ...mapGetters({
        fetchedAsk : 'fetchedAsk',
    })
    
    ...mapGetters([]
        'fetchedAsk',
    ]) // 배열로도 가능 
}
```



## 에러처리

```javascript
async submitForm(){
	try{
	//비즈니스 로직
	....
	
	}cathch(error){
		//에러 핸들링할 코드 
		//console.log(error.response.data);//에러 객체 찍어낸다.
		this.logMessage = error.response.data;
	}
}
```

- error.response : axios 로 보내게 되면 response는 무조건 받는다. 

  상세 내용 볼 수 있음 

- this.logMessage라는 화면 만들어서 오류가 났을 때 화면을 data에 맞게 뿌려줌 



#### package.json 

`dependencies` 는 npm run build 배포할때 포함됨

`devDependencies`는 배포할때 포함되지 않음 



2021-06-28 tippppppp**********

`v-bind` 속성은 뷰 인스턴스의 데이터 속성을 해당 HTML 요소에 연결할 때 사용 

`v-on` 속성은 해당 HTML요소의 이벤트를 뷰 인스턴스 로직과 연결할때 사용

`v-model`은 위에 둘다 기능의 조합으로 동작함 







### template 사용

``` html
<template v-if="news.domain">
	....
</template>
<template v-else>
	....
</template>
```





tips 

#### default

``` js
export cont bus new Vue()
import { bus } from './bus.js'
//bus만 export/import 가능 

export default new Vue();
import Bus from './bus.js'
//전체다 가능 
```



## Eventbus

빈 이벤트 이벤트 객체를 만들어서 이벤트 객체 통해서 컴포넌트간의 데이터를 전달하는 것 



`bus.js` 

```js
import Vue from 'vue';

export default new Vue();
//빈 이벤트 객체 
```

`특정 vue`

```js
import bus from './utils/bus.js';
....

created(){
	bus.$emit('start:spinner');
}
```

`App.vue`

```vue
import bus from './utils/bus.js';
....
<spinner :loading = "lodingStatus"></spinner>

...
    data(){
        return {
            lodingStatus: false,
        };
    },
    methods: {
        startSpinner(){
            this.loadingStatus = true;
        },
        endSpinner(){
             this.loadingStatus = false;
        }
    }
    created(){
        bus.$on('start:spinner', this.startSpinner);
    },
	beforeDestroy(){
         bus.$off('start:spinner', this.startSpinner);
         bus.$off('start:spinner', this.endSpinner);
	}
```

!! 이벤트 버스는 객체가 계속 쌓이기 때문에 `off`를 해주어야 한다.



## 하이오더컴포넌트



```js
    import createListView from '../views/CreateListView';
    ...
    {
      path: '/jobs',
      name: 'jobs',
      component: createListView('JobsView'),
    },
    {
      path: '/item/:id',
      component: ItemView,
    },
    ...
```

` component: createListView('JobsView'),`

view 한단계 위에 `createListView`인 하이오더리스트뷰가 생긴다. 

`createListView.js`

```js
import ListView from './ListView.vue';

export default function createListView(name) {
  return {
    name,
    render(h) {
      return h(ListView);
    },
  };
}
```

<u>**단점**</u>: 컴포넌트 레벨이 깊어진다. 



## 믹스인

 <u>재활용 로직</u> 

상태값을 데이터와 메서드로 가져왔을때 mixin으로 빼게 되면 .vue에서 믹스인으로 해당내용을 주입해서 재사용 할 수 있다. 



`mixins/ListMixin.js`

```js
export default {
  //재사용할 컴포넌트 옵션 & 로직
    created(){
        //....공통 로직
    }
}
```

`NewsView.vue`

```js
import ListMinIn from '../mixins/ListMixin.js'
export default {
  . .... 
 
  mixins : [ListMixIn],
}
```



## 데이터 호출시점 

#### 라우터 네비게이션 가드 

라우터로 특정 url을 접근했을때 접근하기 전에 동작들을 정의하는 로직 (특정 url로 접근하기위한 동작을 정의 하는 속성)

특정 라우터에 진입하기 전에 funcation callback안에 정의하면 next호출했을때 다음동작이 실행된다. 



#### 컴포넌트 라이프 사이클 훅 

`created`

컴포넌트가 생성되자마자 호출되는 로직 

**문제점**

서버가 느릴때 list를 공유하고 있다면 ? 이전 데이터가 보일 수 있다. 

화면상에서 





## 외부라이브러리모듈화 

vue.js 관려 라이브러리가 없을때 일반 라이브러리를 결합할 수 있어야한다. 

차트/ 데이트 피커 /테이블라이브러리 / 스피너 등등 



### chart.js

**설치**

https://www.chartjs.org/docs/latest/

```
npm install chart.js@2.7.0
```

**import 로 App.vue에서 로딩** 

https://www.chartjs.org/docs/latest/getting-started/usage.html

여기에 있는 거 추가 

App.vue

<u>mount() 라이프 사이클 훅에서 차트를 그려야한다.</u>

```js
<template>
  <div>
    <h1>Chart.js</h1>
    <canvas id ="myChart" width="400" height= "400"></canvas>
  </div>
</template>

<script>
import Chart from 'chart.js'

export default {
  //컴포넌트 속성 , 인스턴스 옵션 
  
  mounted(){
    var ctx = document.getElementById('myChart');
    var myChart = new Chart(ctx, {
        type: 'bar',
        data: {
            labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
            datasets: [{
                label: '# of Votes',
                data: [12, 19, 3, 5, 2, 3],
                backgroundColor: [
                    'rgba(255, 99, 132, 0.2)',
                    'rgba(54, 162, 235, 0.2)',
                    'rgba(255, 206, 86, 0.2)',
                    'rgba(75, 192, 192, 0.2)',
                    'rgba(153, 102, 255, 0.2)',
                    'rgba(255, 159, 64, 0.2)'
                ],
                borderColor: [
                    'rgba(255, 99, 132, 1)',
                    'rgba(54, 162, 235, 1)',
                    'rgba(255, 206, 86, 1)',
                    'rgba(75, 192, 192, 1)',
                    'rgba(153, 102, 255, 1)',
                    'rgba(255, 159, 64, 1)'
                ],
                borderWidth: 1
            }]
        },
        options: {
            scales: {
                y: {
                    beginAtZero: true
                }
            }
        }
    });
    console.log(myChart);
  }
}
</script>

<style>

</style>

```



**차트를 컴포넌트화**

![image](https://user-images.githubusercontent.com/36434665/127730462-d562995d-e088-49da-8d48-efd56279ffa4.png)

`BarChart.vue` 생성 해서 chart 로직 갖다 넣고 

`App.vue` 에 컴포넌트 등록해주기 

```
<template>
  <div>
    <h1>Chart.js</h1>
    <bar-chart></bar-chart>
  </div>
</template>

<script>
import BarChart from './components/BarChart.vue'

export default {
  components: { BarChart },
  //컴포넌트 속성 , 인스턴스 옵션 
 component :{
   BarChart,
 },
}
</script>

<style>

</style>

```



!tip 다른 컴포넌트에서 같은 id 값을(getElementById) 쓰면 마지막에 렌더링 된 애를 바라보게 된다. 

**vue 레퍼런스 속성**

```vue
<div id ="app">hello</div>
//..
document.getElementById('app');
document.querySelector('app');
$('#app');
```

를 대신해서 vue에서는 어떻게 쓰냐 ? 

```vue
<div ref ="app" id ="app">hello</div>
//..
this.$refs.app; 
```

레퍼런스로 사용  > 컴포넌트에서만 접근 가능하기 떄문에 같은 ref 값을 사용해도 상관 없다. 



**차트 플러그인**

 https://vuejs.org/v2/guide/plugins.html#ad

에 플러그인 관련된 내용 있음 

`plugins/ChartPlugin.js` 생성 

인스턴스가 생성되었을때 모든 컴포넌트에서 사용하고 싶은 기능을 정의하는 것 

```js
export default {
    install(Vue){j
        console.log('chart plugin loaded');
        
    }
}
```



`main.js` 에서 등록 

```js
import Vue from 'vue'
import App from './App.vue'
import ChartPlugin from './plugins/ChartPlugin.js'  //!
Vue.config.productionTip = false

Vue.use(ChartPlugin); //!
//ChartPlugin.js 의 install 이 실행된다. 

new Vue({
  render: h => h(App),
}).$mount('#app')

```

`ChartPlugin.js `

```js
import Chart from 'chart.js' 
export default {
    install(Vue){
        console.log('chart plugin loaded');
        Vue.prototype.$_Chart = Chart;
		//차트를 플러그인에서 로딩해서 다른곳에서 쓸수 있게 함 
        
   
    }
}
```

` this.$_Chart` 다른 곳에서 이렇게 불러와서 쓸 수 있다. 

`$_` vue.js에서 권고하는 플러그인 prefix



`BarChart.vue`

`import` 제거 , `new Chart` 를 `this.$_Chart` 로 수정 

```vue
<template>
    <canvas ref ="barChart" id ="barChart" width="400" height= "400"></canvas>
</template>
<script>

export default {     
  mounted(){
    var ctx = this.$refs.barChart;
    var myChart = new this.$_Chart(ctx, {
        type: 'bar',
        data: {
            labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
            datasets: [{
                label: '# of Votes',
                data: [12, 19, 3, 5, 2, 3],
                backgroundColor: [
                    'rgba(255, 99, 132, 0.2)',
                    'rgba(54, 162, 235, 0.2)',
                    'rgba(255, 206, 86, 0.2)',
                    'rgba(75, 192, 192, 0.2)',
                    'rgba(153, 102, 255, 0.2)',
                    'rgba(255, 159, 64, 0.2)'
                ],
                borderColor: [
                    'rgba(255, 99, 132, 1)',
                    'rgba(54, 162, 235, 1)',
                    'rgba(255, 206, 86, 1)',
                    'rgba(75, 192, 192, 1)',
                    'rgba(153, 102, 255, 1)',
                    'rgba(255, 159, 64, 1)'
                ],
                borderWidth: 1
            }]
        },
        options: {
            scales: {
                y: {
                    beginAtZero: true
                }
            }
        }
    });
    console.log(myChart);
  }
}
</script>
<style>

</style>
```



## 단위테스트

테스트 코드는 일일이 기능을 손으로 확인하는 시작을 줄여준다.

### Jest

`LoginForm.spec.js` 만들기

```js
import { sum } form './math'
describe('math.js', () => {
	test('10 + 20 + 30', () => {
		const result = sum(10,20);
        expect(result).toBe(30);
        //expect(result).not.toBe(30);
	});
});
```

`describe()` : 연관된 테스트 케이스를 그룹화하는 API

`test()` : 하나의 테스트 케이스를 검증하는 API

` expect()` 결과값 기대되는 값 ? 

**실행해보기** 

```
npm t
```



ESlint 에서 적용하기 

.eslintrc.js 에서 

```js
//..
env :{
 node : true
 jest : true //추가해주기
}
//..
```



### 뷰 컴포넌트 테스트 

```js
import { LoginForm } form './LoginForm.vue'
import Vue from 'vue';

describe('LoginForm.vue', () => {
	test('컴포넌트가 마운팅 되면 username이 존재하고 초기 값으로 설정 되어 있어야 한다. ', () => {
		const instance = new Vue(LoginForm).$mount(); 
       	console.log(instance.username); // test하면 잘 보임 
        expect(instance.username).toBe('');
	});
});
```

인스턴스가 생성될때 엘리먼트 지정  vs 인스턴스가 생성되고 나서 엘리먼트 지정 

(el )                                                                (mount)



### 뷰 테스트 유틸 라이브러리 

https://vue-test-utils.vuejs.org/guides/

**라이브러리 가져오기** 

#### shallowMount

```js
import { shallowMount } from '@vue/test-utils' // 플러그인 
import { LoginForm } form './LoginForm.vue'

describe('LoginForm.vue', () => {
	test('컴포넌트가 마운팅 되면 username이 존재하고 초기 값으로 설정 되어 있어야 한다. ', () => {
		const wrapper = shallowMount(LoginForm);
        expect(wrapper.vm.username).toBe('');
	});
});
```

 `shallowMount` 특정 컴포넌트를 마운트 할수있음 

`wrapper.vm` instance랑 동일 



#### find

wrapper의 `find()` 태그 특정 html요소를 쫓아갈수있다. 

css 선택자로도 가능 

```js
import { shallowMount } from '@vue/test-utils' // 플러그인 
import { LoginForm } form './LoginForm.vue'

describe('LoginForm.vue', () => {
	test('ID는 이메일 형식이여야한다.', () => {
		const wrapper = shallowMount(LoginForm, {
            data(){
                return {
                    username: 'test@abc.com',
                }
            }
        });
        const idInput = wrapper.find('#username');
 		console.log(idInput.element.value); // html태그의 value값을 확인할 수 있다. 
        console.log(wrapper.vm.isUsernameValid); //true
        
	});
});
```

 내가 저 username 의 값을 저장된 test@abc.com을 넣으면? `console.log(wrapper.vm.isUsernameValid)` 값은 true 가 된다. 

> compute 기능 
>



### 사용자 관점의 테스트 코드 

틀렸을때 동작하는 방법 

```js
import { shallowMount } from '@vue/test-utils' // 플러그인 
import { LoginForm } form './LoginForm.vue'

describe('LoginForm.vue', () => {
	test('ID가 이메일 형식이 아니면 경고 메세지가 출력된다.', () => {
		const wrapper = shallowMount(LoginForm, {
            data(){
                return {
                    username: 'test',
                }
            }
        });
       const wraningText = wrapper.find('.warning') 
       console.log(warningText.html()); // .warning 해당하는 html 이나옴 
        expect(wraningText.exits()).toBeTruthy();
	});
});
```

이벤트에 의해서 어떻게 처리해야하는지에 대한 검증하는 코드가 들어가야 한다. 



```js
test('ID와 PW가 입력되지 않으면 로그인 버튼이 비활성화 된다.', () => {
		const wrapper = shallowMount(LoginForm, {
            data(){
                return {
                    username: '',
                    password: '',
                }
            }
        });
        const button = wrapper.find('button');
        expect(button.element.disabled).toBeTruthy();
	});
});
```

테스트 코드가 잘 작성되었는지 확인하려면 반대값을 넣어보면 된다. 



-----------------------------------

vue.js 끝장내기 









