# What you must know 



## 디자인 패턴(Design Pattern) 이란?

소프트웨어 디자인에서 계속 재현되는 문제를 해결하는 재사용 가능한 해결법이다.  

ex> 문제 '특정 클래스가 실행간에 단 한번만 인스턴스화 되어 객체로 이용가능 하여야한다.'를 해결하기 위해 '싱글톤 디자인패턴'을 이용해 볼 수있다'  

또는 특정 클래스의 생성 또는 객체화에 있어 호출당시의 콘텍스트(Context)를 고려하여 클래스를 반환해주는 “팩토리 디자인패턴(Factory Design Pattern)” 을 사용할 수 있다.  

이렇게 디자인 패턴은 디자인(설계)간에 발생하는 문제를 해결해주는 해법 이라고 볼 수 있다. 디자인패턴은 데이터구조, 알고리즘과 다르며 아주 특정한 구조에서 특정한 문제에 한하여 한번만 문제를 해결 할 수 있는 디자인은 "디자인 패턴"이라고 보기 어렵다.(재사용이 가능해야 한다.)    

조금 더 쉽게 말해 디자인 패턴(Design Pattern)은  문제/의도/해결방법이 명시적입니다. 즉 해당 패턴이 사용되는 문제가 “정형화” 되어 있으며, 해당 문제를 접근하는데 어떠한 의도를 가지고 어떻게 해결하는지에 대해서 명시적인 해결 방법 또는 접근 방법을 제안한다.

### Singleton 패턴

``` Singleton패턴 ```이란? 애플리케이션에서 인스턴스를 하나만 만들어 사용하기 위한 패턴이다. 커넥션 풀, 스레드 풀, 디바이스 설정 객체 등의 경우, 인스턴스를 여러 개 만들게 되면 자원을 낭비하게 되거나 버그를 발생시킬 수 있으므로 오직 하나만 생성하고 그 인스턴스를 사용하도록 하는 것이 이 패턴의 목적이다

### 구현

[singleton 패턴 구현](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DesignPattern)

### C++의 디자인 패턴_경량패턴

하나의 클래스당 필요한 데이터가 너무 많고 크기도 클때, 1프레인에 GPU로 모두 전달하기에는 양이 너무 많다.  


class Tree {
private:
Mesh mesh; // 메시     
Texture bark; // 나무껍질 텍스처 
Texture leaves; // 잎사귀 텍스처 
Vector position;
double height;
double thickness;
Color barTint;
Color leafTint;
};

이것을해결하기위해 ->  
객체에 들어있는 데이터 대부분이 인스턴스별로 다르지 않다면?  그 객체를 반으로 쪼개어 명시적으로 모델링 할 수 있다.   

모든 클래스가 다 같이 사용하는 데이터를 뽑아내 새로운 클래스를 만들 수 있다.   


class TreeModel {
private:
Mesh mesh;
Texture bark;
Texture leaves;
};

그럼 이 TreeModel 객체는 하나만 존재하게 된다. 그 이후 각 인스턴스들은 공유객체인 TreeModel을 참조하기만 하면된다. 

class Tree {  
private: 
TreeModel * model;
Vector position; 
double height; 
double thickness; 
Color barkTint; 
Color leafTint; 
}

-----
GPU로 보내는 데이터 양을 최소화하기 위해서는 공유 데이터인 TreeModel을 딱 한 번만 보낼 수 있어야 한다. 그 후 각각 인스턴스마다의 데이터를 전달하고 마지막으로 GPU에 '전체 인스턴스를 그릴 공유데이터를 사용해' 라고 말하면 된다. 

### 경량패턴
이름에서 알 수 있듯이 **경량 패턴은 어떤 객체의 개수가 너무 많아서 좀 더 가볍게 만들고 싶을 때** 사용 한다. 인스턴스 렌더링에서는 메모리 크기보다 렌더링할 나무 데이터를 하나씩 GPU 버스로 보내는 데 걸리는 시간이 중요하지만, 기본 개념은 경량 패턴과 같다.

경량 패턴은 객체 데이터를 두 종류로 나눈다. 먼저 모든 객체의 데이터 값이 같아서 공유할 수 있는 데이터를 모은다. 이런 데이터를 GoF는 고유 상태 또는 자유 문맥 상태라고 부른다. 예제에서는 나무 형태나 텍스처가 이에 해당한다.  
나머지 데이터는 인스턴스별로 값이 다른 외부 상태에 해당한다. 예제에서는 나무의 위치, 크기, 색 등이 이에 해당한다.

[경량패턴](http://boycoding.tistory.com/106)



## Map/HashMap/TreeMap/Hashtable 등의 차이점

### 해쉬 맵 트리맵 차이



**Map**

Map은 key와 value를 가진 집합이며, 중복을 허용하지 않는다.  

즉, 한개의 key에 한개의 value가 매칭된다.  

java.util 패키지에 여러 집합들을 사용하기 위한 여러 interface와 class 들이 정의되어 있다.



**HashMap**

HashMap은 Map interface를 implements 한 클래스로서 중복을 허용하지 않는다.  Map의 특징인 key와 value의 쌍으로 이루어지며, key 또는 value 값으로써 null을 허용한다. 

내부적으로 Entry<K,V>[] Entry 의 array 로 되어 있다. 해당 array 에 index 는 내부 해쉬 함수를 통해 계산된다.

String 은 sun.misc.Hashing.stringHash32 함수를 사용하고 일반 Object는 내부 hashcode 함수와 비트연산으로 계산되어진다.

1 Map<String, String> map = Maps.newHashMap();

2 map.put("c", "1");

3 map.put("a", "1");

4 map.put("b", "1");

5 map.put("k", "1");

6 for (String s : map.keySet()) {

7     System.out.println(s);

8 }

9 // b, c, a, k 출력

내부 hash 값에 따라서 키순서가 정해지므로 특정 규칙없이 출력됨!

```
public class HashMapTest 
{ 
    public static void main(String argv[]) 
    { 
        HashMap hm = new HashMap(); 
        System.out.println(hm.put("aaa", "111")); 
        System.out.println(hm.put("bbb", "222")); 
        System.out.println(hm.put("aaa", "444")); 
        System.out.println(hm.put("ccc", "333"));     
        System.out.println(hm.put("ccc", null));        
         
        System.out.println("HashMap size : " + hm.size()); 
         
        Set set = hm.keySet(); 
        Object []hmKeys = set.toArray(); 
        for(int i = 0; i < hmKeys.length; i++) 
        { 
            String key = (String)hmKeys[i];    
            System.out.print(key); 
            System.out.print(" - "); 
            System.out.println((String)hm.get(key)); 
        } 
    } 
} 
/*
실행:java HashMapTest 
결과: 
null 
null 
111 
null 
333 
HashMap size : 3 
ccc - null 
bbb - 222 
aaa - 444 
*/
```



**Hashtable**

 Hashtable Map interface를 implements 한 클래스로서 중복을 허용하지 않는다.  Map의 특징인 key와 value의 쌍으로 이루어지며, key 또는 value 값으로써 null을 허용하지 않는다.(HashMap과의 차이점)   아래의 예는 HashTable을 사용한 간단한 예제이다. 

```
public class HashtableTest 
{ 
    public static void main(String argv[]) 
    { 
        Hashtable ht = new Hashtable(); 
        System.out.println(ht.put("aaa", "111")); 
        System.out.println(ht.put("bbb", "222")); 
        System.out.println(ht.put("aaa", "444")); 
        System.out.println(ht.put("ccc", "333"));     
         
        System.out.println("Hashtable size : " + ht.size()); 
         
        System.out.println("aaa value : " + (String)ht.get("aaa"); 
         
    } 
} 
/** 
실행:java HashMapTest 
결과: 
null 
null 
111 
null 
Hashtable size : 3 
aaa value : 444 
*/    
```

| 기능                          | HashMap | HashTable |
| ----------------------------- | ------- | --------- |
| 키나 값에 null 저장 가능 여부 | O       | X         |
| 여러 쓰레드 안전 여부         | X       | O         |



**TreeMap**

TreeMap역시 중복을 허용하지 않으며, key와 value의 쌍으로 이루어져 있다.   HashMap과 다른 점은 SortedMap을 implements 하였으므로, key 값들에 대한 정렬이 이루어진다는 점이다.  

내부적으로 RedBlack Tree로 저장됨, 키값에 대한 Compartor 구현으로 정렬 순서를 바꿀수 있다.

1 Map<String, String> map = Maps.newTreeMap();

2 map.put("c", "1");

3 map.put("a", "1");

4 map.put("b", "1");

5 map.put("k", "1");

6 for (String s : map.keySet()) {

7     System.out.println(s);

8 }

9 // a, b, c, k 출력

키값이 알파벳 순서대로 정렬된다. 트리에 저장되므로 키값은 일정 기준으로 정렬된 상태로 출력된다.

```
import java.util.*; 

public class Freq { 
    private static final Integer ONE = new Integer(1); 

    public static void main(String args[]) { 
        Map m = new TreeMap(); 

        // Initialize frequency table from command line 
        for (int i=0; i < args.length; i++) { 
            Integer freq = (Integer) m.get(args[i]); 
            m.put(args[i], (freq==null ? ONE : 
                            new Integer(freq.intValue() + 1))); 
        } 

        System.out.println(m.size()+" distinct words detected:"); 
        System.out.println(m); 
    } 
} 
/** 
실행:java Freq if it is to be it is up to me to delegate 
결과: 
8 distinct words detected: 
{be=1, delegate=1, if=1, is=2, it=2, me=1, to=3, up=1} 
*/    
  
```



**LinkedHashMap**

링크드 리스트로 저장됨

1 Map<String, String> map = Maps.newLinkedHashMap();

2 map.put("c", "1");

3 map.put("a", "1");

4 map.put("b", "1");

5 map.put("k", "1");

6 for (String s : map.keySet()) {

7     System.out.println(s);

8 }

9 // c, a, b, k 출력

키값은 입력 순서대로 출력되어서 나온다.



**HashMap과 TreeMap의 주요 차이점 **

1. HashMap은 어떤 순서도 유지하지 않습니다. 즉, HashMap는, 최초로 삽입 된 요소가 최초로 인쇄되는 것을 보증하지 않습니다. TreeSet와 같이, TreeMap 요소도 요소의 자연 순서 부에 따라 소트됩니다
2. 내부 HashMap 구현은 Hashing을 사용하고 TreeMap은 Red-Black 트리 구현을 내부적으로 사용합니다.
3. HashMap은 하나의 null 키와 많은 null values를 저장할 수 있습니다. TreeMap은 null 키를 포함 할 수 없지만 많은 null 값을 포함 할 수 있습니다.
4. HashMap은 O (1)과 같은 get과 put 같은 기본 연산에 대해 일정한 시간 성능을 나타냅니다. 오라클 문서에 따르면 TreeMap은 get 및 put 메소드에 대한 log (n) 시간 보장 비용을 제공합니다.
5. HashMap의 성능 시간은 대부분의 작업에서 TreeMap에 대해 일정하므로 HashMap은 TreeMap보다 훨씬 빠릅니다.
6. HashMap은 비교에서 equals () 메소드를 사용하지만 TreeMap은 ordering을 유지하기 위해 compareTo () 메소드를 사용합니다.
7. HashMap은 Map 인터페이스를 구현하고 TreeMap은 NavigableMap 인터페이스를 구현합니다.



**HashMap**

1. `HashMap` 에는 키를 기반으로하는 값이 들어 있습니다.

2. 고유 한 요소 만 포함합니다.

3. 하나의 널 (null) 키와 복수의 널 값을 가질 수 있습니다.

4. 그것은 **순서를** 유지 **하지 않습니다** .

   `public class HashMap<K,V> extends AbstractMap<K,V> implements Map<K,V>, Cloneable, Serializable`

**LinkedHashMap**

1. `LinkedHashMap` 에는 키를 기반으로 한 값이 들어 있습니다.

2. 고유 한 요소 만 포함합니다.

3. 하나의 널 (null) 키와 복수의 널 값을 가질 수 있습니다.

4. 대신 **삽입 순서** 를 유지 관리하는 HashMap과 동일합니다. *// 아래 클래스 감속을 참조하십시오.*

   `public class LinkedHashMap<K,V> extends HashMap<K,V> implements Map<K,V>`

**TreeMap**

1. `TreeMap` 에는 키를 기반으로 한 값이 들어 있습니다. NavigableMap 인터페이스를 구현하고 AbstractMap 클래스를 확장합니다.

2. 고유 한 요소 만 포함합니다.

3. null 키는 가질 수 없지만 복수의 널 값을 가질 수 있습니다.

4. 그것은 `HashMap` 과 마찬가지로 **오름차순** 을 유지합니다 (키의 자연 순서를 사용하여 정렬 됨).

   `public class TreeMap<K,V> extends AbstractMap<K,V> implements NavigableMap<K,V>, Cloneable, Serializable`

**Hashtable**

1. Hashtable은 목록의 배열입니다. 각 목록을 버킷이라고합니다. 버킷의 위치는 hashcode () 메소드를 호출하여 식별됩니다. Hashtable에는 키를 기반으로하는 값이 들어 있습니다.
2. 고유 한 요소 만 포함합니다.
3. null 키나 값이없는 경우가 있습니다.
4. 그것은 **동기화** 됩니다.
5. 그것은 레거시 수업입니다.



**결론**

- 특별한 이유가 없다면 검색 성능이 좋은(O(1)) HashMap 을 사용하자
- 키값이 일정한 수준대로 iterate 하려고 한다면 TreeMap 을 사용하자.  하지만 랜덤 접근에 대해서는 O(logn) 성능을 지니므로 많은 데이터를 넣을경우 좋지 않은 성능이 나올수 있다.
- 입력 순서가 의미있다면 LinkedHashMap 을 사용하자. 랜덤 접근에 대해 O(n) 성능을 지니므로 많은 데이터를 입력할 경우 사용하지 않는것이 좋겠다.



#### 해시테이블 

탐색은 O(1) 이 걸린다. 단번에 찾을 수 있다.

key value 가 쌍을 이룬다.

좋은 해쉬 함수는 키의 일부분을 참조하여 해쉬 값을 만들지 않고 , 키 전체를 참조하여 해쉬 값을 만들어 낸다 



### 해쉬 맵 구현할때 충돌발생(해시 충돌)

해시 함수를 사용해 해시값으로 특정 자료를 분류하는데 있어 -> 충돌에 대한 이슈가 있다.



해시맵에서 키로 사용되는 각종 자료형들에 대해 완벽한 해시 함수를 제공할 수 없고, 32비트 정수자료형으로 완전한 자료 해시 함수를 만들 수 없다.

`int index = X.hashCode() % M;`

객체에 대한 해시코드의 나머지 값을 해시 버킷 인덱스 값으로 사용한다.

-> 이런 방식은 서로 다른 객체가 1/M의 확률로 같은 해시 버킷을 사용하게 된다. 이것이 자바의 해시충돌 문데이다. 해시 함수 구현상의 문제가 아닌 또다른 종류의 해시충돌이다.



**회피방법**

Key - value 데이터를 안정적으로 저장하고 조회할 수 있도록 하는 2가지 방법이 있다

![img](http://d2.naver.com/content/images/2015/06/helloworld-831311-4.png)

첫 번째로 Open Addressing은 해시 충돌이 발생하면 다른 해시버킷에 해당 자료를 삽입하는 방식이다. 

두 번째인 Separate Chaining은 충돌 시 해당 버킷값을 첫 부분으로 하는 링크드 리스트로 해결한다.

 첫 번째인 Open Addressing은 데이터 개수가 적다면 Separate chaining보다 더 성능이 좋다. 하지만 배열의 크기가 커질수록(M값) 연속된 공간에 데이터를 저장하여 캐시효율이 높다는 장점이 사라지게 되어 Separate chaining을 사용하는 것이 더 현명 해 보인다.

**해시 테이블 충돌시 Open Addressing**

- <u>선형조사법</u> : 옆자리 보고 비었나 확인하고 그자리에 대신 저장함 -> BUT **클러스터** (데이터가 특정영역에만 집중되는 현상) 가 발생할 수 있다.
- <u>이차조사법</u> : N(2)(제곱) 칸 옆의 슬롯을 검사한다 조금 더 멀리서 빈 공간을 찾으려는 노력이 들어있음 



또한 remove()호출 빈도에 따라 효율이 달라진다. 삭제 처리 시 효율이 높은 linked list방식인 Separate chaining이 open addressing보다 remove() 메소드 호출이 잦은 HashMap에서 더 좋은 효율을 보인다.

 



### 해쉬맵 시간복잡도

-  get(검색) :  o(1)  ~ **최악 o(n)**  
- set:  **o(1)**  

###  

### 해쉬 , 힙구현, 정렬  구현



#### 힙 O(long(2)n



힙소트는 선택정렬군중 하나로써, 비교기반 정렬 알고리즘이다. 선형시간탐색을 이용하는 기본적인 Selection Sort 보다 로그시간 복잡도를 가지는 우선순위 큐를 이용함으로써 성능면에서 낫다고 볼 수 있다. 퀵 소트보다는 느리지만, 최악의 경우에도 O(nlogn)의 성능을 보장한다는 점에서 퀵소트보다 낫다. but stable 하지는 않다

힙은 이진트리이되 **완전이진트리**이다. 그리고 모든 노드에 저장된 값은 자식 노드에 저장된 값보다 크거나 같아야 한다. 즉 루트 노드에 저장된 값이 가장 커야 한다. 

![img](https://i0.wp.com/upload.wikimedia.org/wikipedia/commons/6/69/Min-heap.png?w=1920) 

```
#define MAX_ELEMENT 200 // 힙 안에 저장된 요소의 개수

typedef struct{
  int key;
} element;

typedef struct{
  element heap[MAX_ELEMENT];
  int heap_size;
} HeapType;

# 힙의 생성
HeapType heap1;

```

힙을 이용해서 -> 우선순위 큐를 구현할 수 있다.

우선순위 큐 성능 : 

배열기반 저장 시간복잡도 : O(n)

배열기반 시간 시간복잡도 : O(1)

연결리스트 기반 저장 시간복잡도 : O(n)

연결리스트 기반 시간 시간복잡도 : O(1)

*힙기반 저장 시간복잡도 : O(long(2)n)*

*힙기반 시간 시간복잡도 : O(long(2)n)*



#### 이진 탐색 트리 : O( log(2)n)

이진 탐색 트리의 조건 

- 이진 탐색 트리의 노드에 저장된 키는 유일하다
- 루트 노드의 키가 왼쪽 서브 트리를 구성하느 어떠한 노트의 키보다 크다
- 루트 노드의 키가 오른쪽 서브트리를 구성하는 어떠한 노드의 키보다 작다
- 왼쪽과 오른쪽 서브트리도 탐색트리이다.

왼쪽 자식노드 키 < 부모노드 키 < 오른쪽 자식노트의 키

Insert 함수 구현

```
void BSTInsert(BTree nodeef ** pRoot, BSTData data){
    BTreeNode * pNode = Null; // parent
    BTreeNode * cNode = *pRoot; // current
    BTreeNode * nNode = Null; // newnode
    
    //새 노드가 추가될 위치를 찾는다
    while(cNode != Null){
        if (data == GetData(cNode))
        	return; //중복 허용하지 않는다.
        pNode = cNode;
        if(GetData(cNode))> data)
        	cNode = GetLeftSubTreee(cNode);
        else 
        	cNode = GetRightSubTree(cNode)
    }
    
    //pnode 의 자식 노드로 추가할 새 노드 생성
    nNode = MakeBTreeNode();// 새 노드 생성
    SetData(nNode, data); // 새노드에 데이터 저장
    
    //pNoed의 자식 노드로 새 노드 추가
    if(pNode != Null){
        if(data < GetData(pNode))
        	MakeLeftSubTree(pNode, nNode);
       	else
       		MakeRightSubTree(pNode, nNode);
    }else{
        *pRoot = nNode;
    }
    
}
```









## NoSQL기반

**장점**: 바로바로 찾아서 쓰기 편함 데이터삽입 쉬움

1. **가변적인 구조로 데이터를 저장할 수 있다** : 서버의 확장성을 위해서 데이터 중복이 생기더라도 가급적 테이블을 쪼개지 않고 하나의 큰 테이블에 모두 담아서 저장함 -> 한 테이블을 여러 서버에 나누어 저장하는 Sharding이 쉬워진다. Key->value (map방식)
2. **NoSQL에서는 많은 서버로 확장(Sclae-out)이 가능하다 **: NoSQL은 RDBMS의 이런 단점을 극복하고 Scale Out(많은 서버로 확장)이 잘 될 수 있도록 설계되었으므로 많은 서버로 확장하는 것이 가능하다.

**단점**: 중복  조인어려움 

1. **NoSQL에서는 다양하고 복잡한 데이터 쿼리는 불가능하다**: 여러 테이블간에 Join이 불가능하다. 또 테이블 내의 어떤 값에 대해서 Indexing하는 것 도 어렵다. NoSQL에서 데이터 쿼리는 Key값을 기준으로 value를 read하거나 write하는 단순한 방식이며, RDBMS처럼 복잡한 쿼리는 불가능하다.

-> update가 발생한 경우, NoSQL은 중복 저장된 모든 서버들에 해당 업데이트가 다 될 때까지는 조금 시간이 걸린다. 

2. **일관성이 항상 보장되지 않는다** : NoSQL에서는 lock을 하게될 경우 전체 속도가 너무 느려지게 되므로 RDBMS와 같은 lock을 하지 않는다. 따라서 NoSQL의 일부 서버에서는 아주 잠시 동안은 old data가 제공될 수 있다. 

 



## spin lock, semaphore , monitor, test and set 방식에 대한 설명 





## 멀티프로세스 동기화 코드 주고 수정하는 방법

- ```
  int x;
  func(....func_A);
  func(....func_B);
  
  func_A {
  
  int y;
  for(x =0; x<1000; x++) {
  
  		y = x + 1;
  	}
  }
  
  func_B {
  
  int y;
  for(x =0; x<1000; x++) {
  
  	y = x + 1;
  	}
  } //고쳐보기 
  ```

   -> 뮤텍스 쓰면 된다 동기화 변수가 1개이기 때문에 



## 가비지 컬랙션

**가비지 실행 프로그램인 JVM과 메모리**

메모리는 OS가 관리하는데 모든 프로그램은 OS위에서 돌아간다. 그리고 프로그램이 돌아가려면 메모리가있어야 한다. 때문에 프로그램들은 OS에게 메모리를 주라고 요청하게 된다. 자바의 실행 프로그램인 JVM도 예외는 아니다. 메모리가 필요하면 OS에게 요청해야 한다. 그런데 첨부터 OS가 자기가 가진 메모리를 모두 줘버리면 다른 프로그램들에게 줄 메모리가 없게 된다. 때문에 각 프로그램에게 메모리의 일정부분만 빌려주는 방식으로 관리가 된다. 

|   0~100   | 101~200 |  201~300  | ..   | ..   |
| :-------: | :-----: | :-------: | ---- | ---- |
| A프로그램 |   JVM   | B프로그램 | ...  | ...  |

그런데 JVM이 메모리를 쓰다가 OS가 준 메모리용량이 턱없이 부족하다면?

JVM은 실행하다가 메모리가 부족하면 OS에게 메모리를 더 달라고 요청한다. 그러면 OS가 메모리를 더 빌려준다. (메모리 주소를 할당 )

JVM이 받은 메모리 절대주소는 101~200 ,301~400이지만 상대주소는 0~200 이라는 뜻이다. 이말은 즉 OS로부터 부여받은 메모리는 물리적으로 분리 되어있을 수 있지만 , 논리적으로는 하나의 메모리 처럼 동작한다. 

**가비지란?**

**가비지** 는 정리되지 않은 메모리, 유효하지 않은 메모리 주소 를 말한다. 기존에 array가 가리키고있던 int 타입의 메모리를 사용하다가 새로운 String 타입의 배열을 만들어서 array가 새로만든 배열을 가리키게 할때 int형 array는 주소를 잃버려 또 사용할 수 없다. 

이것이 **주소를 잃어버려서 사용할 수없는 메모리** 인 정리되지 않은 메모리이다.

**가비지 컬렉터란?**

메모리가 부족할 때 이런 가비지들을 정리해주는 프로그램이 **가비지 컬렉터**라고 한다. <u>가비지들이 다른 용도로 사용할 수 있게 **메모리 해제**를 시키는 프로그램이다.</u> 

**언제 실행?**

메모리가 부족해지는 순간이올때 OS에게 추가적인 메모리를 요청한다. 바로 이때 메모리를 더 달라고 요청할 때 **가비지 컬렉터**가 실행된다.

