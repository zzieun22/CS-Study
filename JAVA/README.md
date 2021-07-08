java8

## 람다 표현식



```java
UnaryOpterator<Integer> plus10 = (i) -> i+10;
```

`(i)` 가 인자 `i+10` 이 body 가 된다. 



구현해야하는 추상메서드가 파라미터를 받지 않는다면

```
Supplier<Integer> get10 = () ->  10;
//or
Supplier<Integer> get10 = () -> {
 	return 10;
}
```



인자가 2개인 경우 

```
BinaryOperator<Integer> sum = (a,b) ->  a + b;
```

타입 정의도 가능하고, 안해도된다. 

```
BinaryOperator<Integer> sum = (Integer a,Integer b) ->  a + b;
```



### 변수 캡쳐 

람다를 감싸고있는 영역 local 영역 

```java

public class Foo {
    public static void main(String[] args) {
       Foo foo = new Foo();
       foo.run();
    }

    private void run(){
        final int baseNumber = 10;

        //로컬 클래스
        class LocalClass {
            void printBaseNumer(){
                int baseNumber = 11;
                System.out.println(baseNumber); // 11 (로컬 변수를 가림 )
            }
        }

        //익명 클래스
        Consumer<Integer> integerConsumer = new Consumer<Integer>() {
            @Override
            public void accept(Integer baseNumber){
                System.out.println(baseNumber); // 스코프안에 있는 전달되는 파라미터 가져옴 (10 이아님)
            }
        };

        //람다
        IntConsumer printInt = (i) -> {
            System.out.println(i + baseNumber);
        }; // 로컬변수와 같은 scope이다. 그래서 재정의 안됨 

        printInt.accept(10);
    }

}
```

원래 익명클래스에서 로컬변수 참조 

람다에서 로컨 변수 참조 (스코프 밖에) 가능 



**공통점**

 final 을 참조 할 수 있다. 

final 없지만 더이상 값을 변경하지 않는 경우 셋다 모두 참조 가능함 



**차이점**

<u>scope</u> 

클래스 Foo 안에 메서드 run이있음 그안에 로컬 클래스, 익명 클래스 ,람다가 있다. 

로컬클래스, 익명클래스는 쉐도잉이 된다. 

람다는 쉐도잉이 안됨 



로컬 ,익명클래스에서 선언한 변수가 가려진다. (별도의 scope이기 때문)

but 람다는 scope가 같다. (변수 재정의가 안된다)





## 메소드 레퍼런스

```
package com.example.demo;

import java.util.Arrays;
import java.util.Comparator;
import java.util.function.Function;
import java.util.function.Supplier;
import java.util.function.UnaryOperator;

public class App {
    public static void main(String[] args) {
         UnaryOperator<String> hi = Gretting::hi; //:: 두개 찍혀있으면 메소드 레퍼런스
        //static 레퍼런스 참조 

        Gretting gretting = new Gretting();
        UnaryOperator<String> hello = gretting::hello;
       // System.out.println(hello.apply("aaa"));
        //특정 객체의 인스턴스 참조 

        Supplier<Gretting> newGreeting = Gretting::new;
        newGreeting.get();
        //생성자 참조

        Function<String,Gretting> jeGretting = Gretting::new;
        Gretting jieun = jeGretting.apply("jieun");
        // System.out.println(jieun.getName());
        //입력값 받는 생성자 참조


       String[] names = {"jieun" , "hhihi" , "ttt"};
       Arrays.sort(names, new Comparator<String>() {
           @Override
           public int compare(String o1, String o2) {
               return 0;
           }
       });
        //불특정 다수 인스턴스의 메서드 참조 

        Arrays.sort(names, String::compareToIgnoreCase);
        // 임의의 객체의 인스턴스 메소드 참조 compareToIgnoreCase 인스턴스 메소드 실행된다.
        //위의 내용 람다로 변경
        System.out.println(Arrays.toString(names));
    }
}

```



### 인터페이스 기본 메소드와 스태틱 메소드 

