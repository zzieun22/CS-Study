# 자바스크립트 es6



## 리스트 순회

**기존** 

```
for(var i =0;i< str.length;i++){
 	...
}
```

**es6**

```
for(const a of list){
 ... 
}
```

간결하게 변경 되었음 



## 이터러블/이터레이터 

### Array , Set, Map  

```
const arr = [1,2,3];
for(const a of arr){

}
const set = new Set([1,2,3]);
for(const a of set){

}

const map = new Map(['a',1], ['b',2] , ['c',3]);
for(const a of map){

}

```

array 는 arr[0] , arr[1] 이렇게 해서 값을 찾을 수 있지만 

Set과 Map은 불가능함 



### 어떻게 for  of문에서 동작이 되는가? 

`Symbol.iterator` es6에 추가된 symbol 은 어떤 객체의 key로 사용될 수 있음 



#### 이터러블/이터레이터 프로토콜이랑? 

-  이터러블 : 이터레이터를 리턴하는 `[Symbol.iterator]()`를 가진 값 

- 이터레이터 :{ value , done} 객체를 리턴하는`next()`를 가진 값 

  ```javascript
  let iterator = arr[Symbol.iterator]();
  iterator.next();
   /// {value : 1 ,done : false } 값을 가진다
  ```

- 이터러블/이터레이터 프로토콜 : 이터러블은 for ... of 전개 연산자 등과 함께 동작하도록 규약



**Array**는 `let iterator = arr[Symbol.iterator]();`를 실행한 iterator를 계속해서 순회하면서 value로 떨어지는 값을 순회하는것 



```javascript
let iterator = set[Symbol.iterator]();
iterator.next();
 /// {value : 1 ,done : false } 값을 가진다
 iterator.next();
 /// {value : 2 ,done : false } 값을 가진다
 iterator.next();
 /// {value : 3 ,done : false } 값을 가진다
 
 
let iterator = map[Symbol.iterator]();
iterator.next();
 /// {value : Array(2) ,done : false } 값을 가진다
 /// Array(2) ::: value ["a" , 1] 
```

Set,Map도 마찬가지로 `let iterator = arr[Symbol.iterator]();`를 실행한 iterator를 계속해서 순회하면서 value로 떨어지는 값을 순회하는것 



map.keys()는 iterator를 리턴한다

```javascript
var a = map.keys();
a.next();
 /// {value : "a" ,done : false } 값을 가진다
```

 :: value에 key만 남게 된다. 

 :: key만 뽑을 수 있다는것 

keys() 뿐만 아니라 values(), entries() 도 가능 



```javascript
let iter = arr[Symbol.iterator]();
log(iter[Symbol.iterator]() == iter2) // true
```

iterator함수를 부른 값도 이터러블이다.

iterator함수는 자기 자신을 리턴한다. 



### 전개 연산자

```javascript
const a = [1,2];
log(...a) // 1,2출력
log([...a], ...[3,4]); //1,2,3,4 출력
log(...a, ...arr, ...set, ...map.keys()]); //모든 값이 추가됨 
```

```javascript
a[Symbol.iterator] = null; 
 //오류 생김
```

전개 연산자 역시 이터러블 프로토콜을 따르고 있다. 





## 제너레이터와 이터레이터

: 이터레이터이자 이터러블을 생성하는 함수

: 순회 할 수 있는 값을 만들 수 있다. 제너레이터를 통해 조작 할 수 있음 

```javascript
funcation *gen(){
	yield 1;
	if(false) yield 2;
	yield 3;
    //마지막에 리턴값을 만들수 있음 
    return 100; //done 이 true일 때 출력 but 순회할때(for)는 안나온다.
}
let iter = gen();
log(iter[Symbol.iterator]() === iter ) // true
log(iter.next());
```



### Odds 

```javascript
   function *odd(l){
        for(let i = 0;i<l; i++){
            if(i % 2) yield i;
        }
    }
    let iter2 = odd(10);
    console.log(iter2.next());
    console.log(iter2.next());
    console.log(iter2.next());
    console.log(iter2.next());
    console.log(iter2.next());
    console.log(iter2.next());
    console.log(iter2.next());
```

요런 함수 만들어봄 

![image](https://user-images.githubusercontent.com/36434665/124343475-a456d280-dc06-11eb-96b5-05a587e94a91.png)

결과가 나온다.



#### 구조 분해

```
    const [head, ...tail] = odds(5);
    console.log(head);
    console.log(tail);
  
```

![image](https://user-images.githubusercontent.com/36434665/124343573-83db4800-dc07-11eb-8b13-6946cc8bd4ee.png)

```
    const [a,b, ...rest] = odds(10);
    console.log(a);
    console.log(b);
    console.log(rest);
```

![image](https://user-images.githubusercontent.com/36434665/124343589-aec59c00-dc07-11eb-99ff-f12841486093.png)





## map, filter, reduce

```javascript
    const products = [
        {name: '안녕', price: 12000},
        {name: '하세요', price: 15000},
        {name: '저는', price: 20000},
        {name: '지니', price: 25000},
        {name: '입니다', price: 15000}
    ];
```

  

### map

**map  로직**

```javascript
const map = (f, iter) => {//f 라는 함수를 받아서 어떤값을 수집할 것인지 위임한다.(추상화)
        let res = [];
        for (const a of iter) {
            res.push(f(a));
        }
        return res;
    };

```

- 고차함수이다.



```javascript
 /////////////es5 ///////////////

  let names = [];
    for (const p of products) {
      names.push(p.name); // 직접적으로 코딩을 함 
    }
    log(names);

 /////////////es6 ///////////////
///////////위의 내용을 간단하게 작성
    log(map(p => p.name, products));
```

- map 함수의 보조함수를 통해서 products안에 있는 1:1로 매핑되는 값을 전달하겠다는 보조 함수 전달 

  

#### map의 다형성

map 함수는 이터러블 프로토콜을 따르고 있음 

```javascript
    log(map(a => a * a, gen()));

    let m = new Map();
    m.set('a', 10);
    m.set('b', 20);
    log(new Map(map(([k, a]) => [k, a * 2], m)));

```

- 새롭게 map을 받아서 value를 조작할 수 있음 



### Filter

**Filter  로직**

```javascript
 const filter = (f, iter) => {
        let res = [];
        for (const a of iter) {
            if (f(a)) res.push(a);
        }
        return res;
    };
```

 

```javascript
   /////////////////es5/////////////////
   let under20000 = [];
    for (const p of products) {
      if (p.price < 20000) under20000.push(p);
    }
    log(...under20000);

   /////////////////es6/////////////////
    log(...filter(p => p.price < 20000, products));
```



### Reduce 

값을 축약하는 함수 

**Reduce  로직**

```javascript
    const reduce = (f, acc, iter) => {
        if (!iter) {
            iter = acc[Symbol.iterator]();
            acc = iter.next().value;
        }
        for (const a of iter) {
            acc = f(acc, a);
        }
        return acc;
    };
```

```javascript
  const nums = [1, 2, 3, 4, 5];

   /////////////////es5/////////////////
    let total = 0;
    for (const n of nums) {
        total = total + n;
    }

   /////////////////es6/////////////////
     const add = (a, b) => a + b;

    log(reduce(add, 0, [1, 2, 3, 4, 5]));
    // 15

	//위의 내용 실행 하는 순서는 아래와 같다. 재귀적으로 실행
    log(add(add(add(add(add(0, 1), 2), 3), 4), 5));
    // 15

    log(reduce(add, [1, 2, 3, 4, 5])); //시작하는 값 생략
    // 15
```



#### reduce 를 통해 어떻게 축약하나?

 모든 가격 다 더하기

```javascript
reduce((totalprice,product) => total_price + product.price, 0 , products);
```



짬뽕해서 사용해보기

```javascript
const add = (a, b) => a + b;
reduce(
    add, 
    map(p => p.price , 
        filter(p => p.price <23, products)));
```















































