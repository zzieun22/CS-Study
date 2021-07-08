[nvm사용](nvm사용)

[vue-CLI](vue-CLI)

[ESlint](ESlint)

[Router](Router)

[환경 변수](환경변수)

[API구현](API구현)

[에러처리](에러처리)

[PROMISE](PROMISE)



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
mode: 'history', // url 에 #이 없어진다. 'http://localhost:8080/#/'
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





## API구현

### API공통화

axios 를 공통으로 사용하기위해 create 하여 빼보기 

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





## 에러처리

```vue
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



2021-06-28

`v-bind` 속성은 뷰 인스턴스의 데이터 속성을 해당 HTML 요소에 연결할 때 사용 

`v-on` 속성은 해당 HTML요소의 이벤트를 뷰 인스턴스 로직과 연결할때 사용

`v-model`은 위에 둘다 기능의 조합으로 동작함 





## PROMISE

자바스크립트 비동기 처리에 사용되는 객체 



보통 서버에서 받아온 데이터를 화면에 표시할 때 사용 

```
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

  ```
  return new Promise(function(resolve,reject)){
  	resolve(); // 실행하면 이행 상태가 된다.
  });
  ```

- Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태

  ```
  return new Promise(function(resolve,reject)){
  	......
  	reject(new Error("Request is failed"));
  });
  ```



### Promise chaining

`then()`으로 여러개 프로미스 사용할 수 있음 

```
..()
.then(function(data){

})
.then(function(){

});
....

```



```
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









