- [자료구조](#자료구조)

- [데이터베이스](#데이터베이스)

- [운영체제](#운영체제)

- [네트워크](#네트워크)

- [JAVA,JS](#JAVA,JS)

- [Ios][#Ios]

- [Spring](#Spring)

- [Front-End](#Front-End)

- [etc](#etc)

- 

- ## 자료구조

- - **스택 큐 무엇인지??**

  - **스택 왜 나뉘어져있음?**

  - **lru cache 메모리 하기위한 자료구조중 무엇을 쓸까요?**

  - **LRU Cache Replacement > 한정된 메모리에서 캐시 저장하는거 캐시공간 다찼을때 고려함 버릴때 어떤걸 선택함??** 

     **\>>> 가장오랫동안 사용하지않는것 우선순위 버려야하는거 자료구조로 뭘 택해서 할지 말해라**

  - **재귀함수 1~n더하는거짜보기**

  - **스택오버플로우가 뭐냐**

  - **1011 과 not 1101 xor 하면?**

  - **해쉬 맵 트리맵 차이**

  - - 해시맵> 해시를 이용해서 저장 (저장순서        보장x ) O(1)
    - 저장은 느리고 검색은 빠름 
    - 트리맵> 엔트리를 트리 형태로        저장하여 저장할때 키 값을 기준으로 자동정렬(key값이 기준)되어 저장        (트리구조 특성상 엔트리에 접근하기위해서는 O(logN)) 
    - 저장은 빠르고 검색은 느림 

  - **해쉬  맵 구현할때 충돌발생** 

  - **해시맵이 뭔가?**

  - - KEY , VALUE를 갖는 자료구조 >        효율적인 검색시 사용 
    - (key) 중복안됨 / (value) 중복가능 ,        null 가능 

  - **해시가 뭔가?**

  - - key라는 값을 연산을 통해 해시값을 만든다. 그        해당 key는 해시 값을 가지고 있는데 그 매핑해놓은 것을 해시맵 이라고 한다. 
    - 해시 함수**(hash function)는 임의의 길이의 데이터를 고정된 길이의 데이터로 매핑하는 함수이다. 해시 함수에        의해 얻어지는 값은** 해시 값**,** 해시 코드**, 해시 체크섬 또는 간단하게** 해시라고 한다. 

  - **해시 테이블이란?**

  - - 키에 결과값 value를 저장하는 자료구조 (최소        O(1) , 최대 O(n)) 
    - 스레드 동기화를 지원함(hashmap은 동기화를        지원하지않음 )
    - 데이터를 테이블 형식으로 구성함 
    - 키와값에 null을 허용하지 않는다.

  - **해쉬맵에서       데이터 가져오는 get o(n) ,set o(1) 시간복잡도** 

  - **입력과 삭제에 대해       시간복잡도가 O(1)인 자료구조**

  - **해쉬/힙/구현 정렬 구현** 

  - **후위탐색**

  - **최대힙**

  - **완전이진트리 결과**

  - **페이징 계산**

  - **인덱스 특징, 부동소숫점**

  - **disk  in page** 

  - **재귀  (2의 n제곱이 되어가는 (n = 1~9)) 함수 구현** 

  - **stack, queue 중 push pop 할때 가장적게걸리는 것?**

  - **hash, table,B-Tree, array, linked list ,그래프 중 시간복잡도 탐색(검색)/ push pop 중 적게걸리는 것** 

  - **배열과 백터와 리스트의 차이**

  - - 벡터 

    - - 연속적인 메모리, 공간을 원하는만큼 요구함         O(n)이 든다 > 동적배열 
      - 데이터 순차적 저장 > 검색속도 빠르지않음
      - 데이터 위치를 알면 배열처럼 쉽게 접근가능 

    - 배열 

    - - 다수의 데이터를 그룹핑해서 효율적으로 관리         가능한 자료형으로 데이터에 접근하기위해 인덱스 존재
      - 인덱스로 조회하는 속도가 빠르다 
      - 데이터 낭비가 있음 (한번 확보된 배열         크키조절이 어려움 )

    - 리스트

    - - 비연속적인 메모리 , 메모리를 선할당 하지 않음         
      - 인덱스 장점을 버리고 빈틈없이 데이터를 적재하는         장점을 취한 자료형 
      - 중간값 삭제가 용이함
      - 순차접근이라 검색이 느림

    - 링크드리스트

    - - 역시 순서가 있는 값들을 순서대로         보존. 그러나 값 하나하나가 **노드**(node)를 이루고 있으며, 각 노드는 자신의 다음 노드를 가리키고 있음         다음 노드라는 건 다음 값을 가지고 있는 노드입니다. 만약 다음 노드가 없다면 포인터가 null 포인터 
                         이렇게 기본적으로 각 노드는 **①자신이 보존 중인 값**과 **②다음 노드를 가리키는 포인터**, 2개의 멤버 변수를 가진다.

  - **맨 앞의 데이터를 지울 경우 백터와 리스트의 시간복잡도는 어떻게 되나?**

  - **테이블에서 충돌이  발생하면 어떻게 해결하나?**

  - **해시 값이 한곳에 몰릴 경우 어떻게 효율적으로 처리할 수 있나?**

  - **알고리즘 풀 때 메모리 사용량을 줄이기 위해 사용한 방법이 있나?**

  - **부동소수점의 오류?**

  - **리팩토링의 정의와 자바코드주고 2개 주고 리팩토링 하는거**

-  

-  

- ## 데이터베이스

- - **데이터 select하고, update할때 계산복잡도**

  -  **미니sns서비스 피드가 뜨게 만들때 DB구조 어떻게 짤건가요? (ERD다이어그램으로)**

  -  **관계형 테이블에서 성능을 높이려면 어떻게 해야하는가?** 

  -  **관계형 디비 조인 줄이면 어떻게 db를 어떻게 읽어야함?** 

  - **인덱스란?**

  - **인덱스에서 삽입,삭제가 많으면 왜 불리한가?**

  - **Nosql 기반** 

  - 단 : 중복 조인어려움

  - 장 :바로바로 찾아서 쓰기 편함 데이터삽입 쉬움

  - **데이터 베이스의 키 종류** 

  - - 기본키

    - - 릴레이션에서 튜플을 구별할 수 있는 키 

    - 외래키

    - - 관계를 맺고 있는 릴레이션을 참조하는 릴레이션 속성 

    - 후보키 

    - - 기본키로 사용할 수 있는 속성들

    - 대체키

    - - 후보키가 2이상일때 기본키는 제외한 나머지 후보         

  - **공개키와 대칭키에 대해 설명해 봐라.**

  - - 대칭키

    - - 하나의 비밀키를 양쪽 모두 같이 사용한다.
      - 공개키와 비밀키를 별도로 가지는 것과         구별되는데, 이와 비교하면 계산속도가 빠르다.
      - 비밀키 알아내면 암호 해독가능 

    - 공개키

    - - 공개키 비밀키 두개 공개
      - 공개키 암호를 구성하는 알고리즘을 대칭키 암호         방식과 비교하여 비대칭 암호라고 불림
      - 암호화와 복호화에 사용하는 키가 서로 다름
      - 암호화할 때의 키는 공개키(public         key), 복호화할 때의 키는 개인키(private key)
      - 공개키는 누구나 알 수 있지만, 그에 대응하는         비밀키는 키의 소유자만이 알 수 있어서
      - 특정한 비밀키를 가지는 사용자만이 내용을 열어볼         수 있도록 하는 방식.

  - **inner join (실제로 테이블 조인하기)**

- ----------------

- 

- ## 운영체제

- - **어떤경우 스택에 할당되고 어떤 경우힙에 할당됨??**

  - **스레드에 왜 개별적인 메모리공간이 필요하나?**

  - **프로세스란?? 프로세스 스레드 차이** 

  - **스레드가 더 빠른이유?**

  - **스레드는 왜 static 공유함?? 스택에 어떤 데이터 들어감???**

  - **Static 모든 스레드 다 공유하지않음??**

  - **스레드 자원공유시 문제점? 해결법 어떻게 해야함?**

  - **운영체제 동기화**

  - **cpu스케줄링에 대한 설명**

  - - 프로세스 구동하려면 다양한 시스템 자원이 필요하다. 프로세스에 얼마나 할당하는지 정책을 만드는 것을 cpu스케줄링 이라고한다. 
    - CPU가 어떤 프로세스에 의해 점유중일때 우선순위가 높은 프로세스가 CPU를 차지할 수 있음 (선점스케줄링)
    - 선점 : SRT(짧은시간 순서), 라운드로빈(같은크기 할당), 다단계큐(ready큐를 여러개 사용하는 방법) 
    - 비선점 : HRN(수행시간 길이, 대기시간 길이 고려) , SJF(수행시간이 짧은 것), 우선순위(우선순위정적 동적으로 부여), FIFO(도착한 순서)

  - **cpu 스케줄링중 주로 뭐가 가장 많이 사용된다고 생각하나?**

  - **쓰레드를 생성할 때는 시스템콜이 안 일어나냐**

  - - 시스템 콜은 이러한 커널 영역의 기능을 사용자        모드가 사용 가능하게, 즉 프로세스가 하드웨어에 직접 접근해서 필요한 기능을 사용할 수 있게 해준다. 

  - **동기화에 대해 설명하고 코드로 작성해봐라**

  - **노드에서  멀티 프로세스를 돌리려면?** 

  - **단일 쓰레드 기반의 노드에서 많은 데이터를 처리하려면 멀티프로세스 구현 즉, js파일을 여러 번 실행시킨다. 한 번 실행될때마다 프로세스 하나씩       생성된다.**

  - **언제 멀티 프로세스를 쓰는 것이 유리한가?** 

  - **프로세스와 쓰레드의 차이**

  - - <https://devuna.tistory.com/21>
    - <https://github.com/jieunpark247/jieunpark247.github.io/tree/master/OS>

  - - **프로세스** 

    - - 운영체제가 프로그램에메모리를 할당하여 실행하면         이를 프로세스
      - 프로세스는 메모리에 적재되어 실행되고 있는         프로그램 
      - 프로세스는 커널에의해 직접 관리됨> 커널         메모리안에는 각 프로세스마다 관리하고 있는 프로세스에 대한 데이터들이 있음 이정보는 PCB라고하는 자료구조안에있는데 프로세스를         제어하는데 필요한 정보들이 담겨있음 

  - - **스레드**

    - - 스레드는 프로세스의 실행단 한프로세스 내에서         동작되는 여러 실행흐름으로 프로세스내의 주소공간이나 자원을 공유할 수 있음 
      - 한 프로세스 내에서 동작되는 여러         실행의 흐름으로 프로세스 하나에 자원을 공유하면서 일련의 과정을 여러 개를 동시에 실행시킬 수 있는 것을 말합니다.

  - **멀티 프로세스와 멀티 쓰레드의 차이**

  - - 실핼할 수 있는 파일이 프로그램> 프로그램이 돌아가고 있는 상태를 프로세스 

    - 한프로세스 안에도 여러갈래 작업이 동시에 진행된다. 이 갈래는 스레드로 불림 

    - 컴터는 프로세스마다 자원을 분할해서 할당한다. 

    - 스레드는 프로세스마다 주어진 전체 자원을 함께 사용한다. 

    - 멀티 스레딩의 장점

    - - 프로세스를 이용하여 동시에 처리하던 일을 스레드로 구현할 경우 메모리 공간과 시스템 자원 소모가 줄어들게 된다. 스레드 간의 통신이 필요한 경우에도 별도의 자원을 이용하는 것이 아니라 전역 변수의 공간 또는 동적으로 할당된 공간인 Heap 영역을 이용하여 데이터를 주고받을 수 있다. 그렇기 때문에 프로세스 간 통신 방법에 비해 스레드 간의 통신 방법이 훨씬 간단하다. 심지어 스레드의 context switch는 프로세스 context switch 와는 달리 캐시 메모리를 비울 필요가 없기 때문에 더 빠르다. 따라서 시스템의 throughtput 이 향상되고 자원 소모가 줄어들며 자연스럽게 프로그램의 응답 시간이 단축된다. 이러한 장점 때문에 여러프로세스로 할 수 있는 작업들을 하나의 프로세스에서 스레드로 나눠 수행하는 것이다.

    - 멀티 스레딩의 문제점

    - - 멀티 프로세스 기반으로 프로그래밍할 때는 프로세스 간 공유하는 자원이 없기 때문에 동일한 자원에 동시에 접근하는 일이 없었지만 멀티 스레딩을 기반으로 프로그래밍할 때는 이 부분을 신경써줘야 한다. 서로 다른 스레드가 데이터와 힙 영역을 공유하기 때문에 어떤 스레드가 다른 스레드에서 사용중인 변수나 자료구조에 접근하여 엉뚱한 값을 읽어오거나 수정할 수 있다.
      - 그렇기 때문에 멀티스레딩 환경에서는 동기화 작업이 필요하다. 동기화를 통해 작업 처리 순서를 컨트롤 하고 공유 자원에 대한 접근을 컨트롤 하는 것이다. 하지만 이로 인해 병목현상이 발생하여 성능이 저하될 가능성이 높다. 그러므로 과도한 락으로 인한 병목현상을 줄여야 한다.

    - 멀티 스레드 vs 멀티 프로세스

    - - 멀티 스레드는 멀티 프로세스보다 적은 메모리 공간을 차지하고 문맥 전환이 빠르다는 장점이 있지만, 오류로 인해 하나의 스레드가 종료되면 전체 스레드가 종료될 수 있다는 점과 동기화 문제를 안고 있다. 반면 멀티 프로세스 방식은 하나의 프로세스가 죽더라도 다른 프로세스에는 영향을 끼치지 않고 정상적으로 수행된다는 장점이 있지만, 멀티 스레드보다 많은 메모리 공간과 CPU 시간을 차지한다는 단점이 존재한다. 이 두 가지는 동시에 여러 작업을 수행한다는 점에서 같지만 적용해야 하는 시스템에 따라 적합/부적합이 구분된다. 따라서 대상 시스템의 특징에 따라         적합한 동작 방식을 선택하고 적용해야 한다.

    - 멀티 프로세스 

    - - 부모-자식 관계라고 해도 자신만의 메모리 영역을 가지게 된다.
      - 환경변수와 프로세스 핸들 테이블이 상속 가능할 뿐 결국 독립적인 관계이다.
      - fork를 통해 프로세스를 복사한다.
      - 유닉스 계열에서 ps 명령어로 현재 수행되고         있는 프로세스를 확인할 수 있다.
      - 프로세스 간의 통신을 하려면 IPC(InterProcess Communication; 세마포어, 큐, 공유메모리)를 통해야 한다.
      - 멀티 스레드
      - 하나의 프로세스가 다수 개의 작업을 각각 스레드를 이용하여 동시에 작동 시킬 수 있다.
      - 스레드는 다음과 같은 공유 메모리를 가진다.

- -----------------------

- 

- ## 네트워크

- - http1.1 http2 뭐가다름 ? 뭐가 추가됨 ?
  - 웹소켓?
  -  3핸드쉐이크란? 저거 왜하는거야? 소켓같은거 어쩌구 ?
  - 트래픽 너무 들어왔을때
  - 캐시머임? 캐시는 빨리사라짐?? 잠시동안저장?? 그게 캐시??
    왜잠시동안저장?? 캐시는 서버에 저장안되나요? 서버에 저장하면 안되나?
  - 서버에 저장하는건 뭐야?
  - OSI 계층 설명 이것은 무엇인가? 라우터 ,,등등을 쓰는 계층 ?

- 

- ## JAVA,JS

- - **Implement,       extends 차이**

  - - **extends : 부모로부터 상속** 
    - **implements :조언자로부터 상속**
    - **implement : 다중 상속을 통해 해결 가능함 / 그러나 interface로 정의되어 있어야함** 
    - **extends :  클래스를 확장하기 위한 것( 클래스는 선언과 내용이 들어가 있는 것 )**
    - **implements : 인터페이스를 구현하기 위해 생긴 것. ( 인터페이스는 선언만 되어 있는 것 )**

  - **intertace ,abstract , extends**

  - - intertace : 한자식이 두 부모로 부터 상속받을 수 있음 (그자체로 객체를 만들 수 없음 ) implements로 상속해서 객체를 만들 수 있음. 인터페이스의 함수를 필수적으로 장착해야함 
    - abstract 는 자식이 부모의 것을 쓸때 공통적인것들을 사용하기 위해 추상적으로 틀+기능을 구현해 놓은것 >> 자식이 해당 클래스를 상속받아 자유롭게 extends 하여 override해서 쓸 수 있음 
    - extends 부모로부터 물려받는것 
    - 상속은 물려받는것 , 인터페이스는 장착하는것

- - **일반 자바에 비교해서 스프링의 장점?**

  - **Xml과 json의 장단점이 뭔가?**

  - 1. JSON은 종료 태그를 사용x
    2. JSON의 구문이 XML의 구문보다 더 짧음
    3. JSON 데이터가 XML 데이터보다 더 빨리 읽고 쓸 수 있음.
    4. XML은 배열을 사용할 수 없지만, JSON은 배열을 사용할 수 있음
    5. XML은 XML 파서로 파싱되며, JSON은 자바스크립트 표준 함수인 eval() 함수로 파싱됨

  - **자바구조**

  - - static : 메모리 할당을 한번만 하게 해줌 (값이 공유된다)
    - final : 값이 변경되지 않음 
    - 싱글톤 패턴 :단 하나의 객체만을 생성하게 강제하는 패턴 
      -  클래스를 통해 생성할 수 있는 객체는 한개만 되도록 만드는것 
        한번 세팅을 해놓으면 다른데서도 같은걸 사용해야 할 때 
        tatic으로 생성 : 정적요소로 딱 한개만 생성됨 
        static으로 선언한 후 setting == null로 만듦 getSetting 함수에서 setting        ==  null이면 객체선언하고 아니면 바로 리턴해줌 
    - 스테리지 패턴 (인터페이스)
      - 프로그램 실행중 모드가 바뀔때마다 검색(전략)이 수정됨 
        객체마다 모드 하나하나를 모듈로 분리해서 실행될 모듈을 갈아끼워주는 방식 
    - 커맨드 패턴
       커멘드패턴은 스테리지랑 비슷하지만 하는 방식이 다르다. 
      다른 명령어를 짤수 있음 (추상, 상속 )
    - 어댑터 패턴 
      형식이 다른 두사이에서 호환될 수 있도록 해주는것 
      인터페이스 이름, 메소드명이 다를때 어댑터로 임플리먼트함 
    - 프록시 패턴
      대리인 역할을 두어서 가벼운일은 비서가 처리하고 무거운작업을할때는 실제클래스로 생성 

  - **jvm** 

  - - 컴파일된 코드를 실행시켜주는 가상의 컴퓨터 
      - JAVA 는 test.java 를 통해 -> test.class (바이트코드) -> cpu
        -> 바이트 코드는 머신코드가 아니다. 그래서 cpu상에서 바로 실행할 수 없다. 기계어 코드가 아니고 기계어 소스코드 중간에 있는 바이트 코드이다. 그래서 실제로 실행하려면 머신코드로 변환되는 과정을 거쳐야 한다. 
        이 작업을 JVM이 함!!! (Java Virtual Machine)
         library 가 필요함 => API (기능들을 만들어서 제공)
        JVM+API를 합해서 => JRE라고 한다.
         JRE + 자바 개발 Tool을 합해서 => JDK라고 한다.
        --> JAVA 는 플랫폼에 독립적이다. JVM은 자바프로그램 실행에 관련된 대부분을 관리(control)한다.
        - stack
          - 힙에 생성된 객체 참조값 
          - 원시 타입 데이터 할당 -> 스레드 하나당stack 하나씩 할당된다. 
          - 다른 스레드의 stack에 접급 할 수 없다. 
          - 함수가 종료되면 stack 에있는 원시타입은 다 pop 된다.
        - heap 
          - 긴 생명주기를 가진 데이터가 저장 
          - 모든 메모리 중 stack 에 있는 데이터를 제외한 부분 
          - 모든 객체 타입 ,스레드 개수 상관 없이 단하나의 heap 존재

- ![public class Main  public static  int port  void main(String[] args) {  aeøø;  String host  - "localhost"; ](data:image/png;base64,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)

-  

- ![Port = 4000  Stack  Stack 에 port 라는 썬수.멸 할당 되어 소리에 쌓임  host  ort 4000  Stack  Str•ng  IQ쮀hp와 ](data:image/png;base64,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)

- - **MVC 패턴이란  이 패턴의 장점? 구현해본 경험**

  - - view 는 눈에보이는것 html css 등으로, 데이터를 보여주는것 model 은 상태저장 ,데이터 형식등등 에 관련된것 controller 데이터를 읽고쓰고 지우도록 동작을하는 것 

  - **라이브러리 ,프레임워크**

  - - 라이브러리는 개별적인 기능들, 프레임 워크는기초적인 제품 골격을 가진 상태 
    - 가져다쓰는게 라이브러리, 기본틀로 삼아서 그위에 덧붙이는게 프레임워크 

  - **가비지컬렉션이란?**

  - - C나 C++ 에서는 OS레벨의 메모리에 직접 접근하기 때문에 메모리를 명시적으로 해제해주어야한다. 그렇지 않으면 메모리누수가 생김. 반면 자바는 OS메모리 영역에 직접 접근하지 않고 JVM가상머신을 이용해 간접적으로 접근함 오브젝트가 필요해지지않는 시점에서 알아서 free()를 수행해서 메모리를 확보함. 이런 메모리 관리를 자바 가상머신에게 맡기는것 
                     <https://yaboong.github.io/java/2018/06/09/java-garbage-collection/>

  - **가비지컬렉테는 메모리를 안쓰는 놈을 자동 해제시키는데 그럼 내부적으로 메모리를 안쓰는지 어떻게 판단할 건가?**

  - - GC는 unreachable object(stack에서 도달할 수 없는 heap영역의 객체) 를 우선적으로 메모리에서 제거하여 메모리 공간확보를 한다. 

    ![1603082770900](C:\Users\jieun\AppData\Roaming\Typora\typora-user-images\1603082770900.png)

  ![1603082803951](C:\Users\jieun\AppData\Roaming\Typora\typora-user-images\1603082803951.png)

  - **Node와 자바 구조 차이 ( 이벤트루프 구조와 쓰레드풀 구조의 차이)**
  - - 스레드 풀 > 스레드를 제한된 개수만큼        정해놓고 작업 큐에 들어오는 작업을 하나씩 쓰레드가 맡아서 처리함 
  - **JAVA로 서버를 구현했을때와 node로 구현했을 때 차이점이 뭔가?**
  - **node.js의 기본구조?**
  - - Node.JS 는  웹브라우저에 종속적인 자바스크립트에서 외부에서 실행할 수 있는 Runtime 환경을 Chrome V8 엔진을 제공하여 여러 OS 환경에서 실행할 수 있는 환경을 제공하게 됩니다. 이것을 Node.JS 라고 정의할 수 있습니다.
    -  Node.js로 구성된 서버의 특징은 단일 스레드만 사용하여 요청을 처리하며 응답속도가 빠른점이며, 자바스크립트처럼 이벤트 루프방식을 통해 해당 일을 수행하는 방식으로 된 점도 특징이라 할 수 있다.
    -  java로 이루어진 서버는 오래전부터 사용된 언어로, 1990년대부터 현재까지 사용중에 있다. 엄격한 문법체계가        특징이며 다른 인터프린터 언어와는 달리 컴파일언어인 점도 특징이라 할 수 있다. 또한 요청이 들어오면 스레드풀에서 스레드를 꺼내어해당 일을 처리하게 구성되어있다.
                     <https://lts0606.tistory.com/91>
  - **Nodejs의 구조가 비동기 단일쓰레드이다. 그런데, 멀티 쓰레드(spring)보다 이게 왜빠른가?**
  - - Node.js가 완전한 비동기-논블러킹 방식의 I/O 작업을 수용하기 때문이다.상대적으로 긴 시간이 소요되는 I/O작업을 기다리지 않고client의 요청과 응답만을 담당하기 때문에 더 적은 자원으로도 높은 성능을 기대할 수 있음.
    - 일반적인 웹은 멀티스레드 방식이다 : 점점 더 많은 동시에 발생하는 클라이언트 요청을 처리하기 어려움 > 많은 메모리를 사용하게됨 ,, 이런 사용가능한 스레드가 요청처리할때 까지 기다려야 할 수 있음, Blocking I/O작업으로 인해 시간이 낭비된다. 
    - 반면 node.js는 제한된 스레드 풀을 내부적으로 관히라여 클라이언트의 요청에 서비스를 제공한다. 요청을 이벤트큐에 배치한다. node.js는 이벤트루프라 불리는 컴포넌트를 가지는데 (요청받아들이고 처리하는 것이 무한루프를 사용하기 때문) 이벤트 루프는 싱글 스레드를 사용함 
    - 이것이 많이 동시에        발생하는 클라이언트 요청 처리하는게 쉽다. 동시에 클라이언트 요청이 증가해도 이벤트 루프를 이용하기 때문에 많은 스레드를 이용하지 않음 > 자원소모가 적음 
                     <https://siyoon210.tistory.com/164>
  - **콜백헬이 뭔지아냐? 프로미스 내부적으로는 어떻게 구현되었을것 같나?**
  - - 콜백이 수번 나타나서 생기는 문제 , 가독성이떨어짐 , 실수위험 디버깅위험하다.
    - 프로미스 es6>프로미스 객체로 받아서 첫번째인자에는 수행작업 두번째인자로는 결과물이 콜백함수에 들어간다. .then인 체이닝 방식으로 순차적으로 처리 가능하다.  직관적이지만 polyf? 라이브러리없이는 익스플로러등에서 돌아가지않음 
    - es7에는 async await 라는 직관적인 언어로 사용 가능 함수앞에 async 함수를 붙이고 await을 달면 진행 멈추고 그다음작업이 수행됨 
  - **Node.js가 뭐지?** 
  - - Node.JS 는 구글 크롬의 자바스크립트 엔진 (V8 Engine) 에 기반해 만들어진 서버 사이드 플랫폼입니다.
  - **Websocket**
  - - WebSocket 은 ws 프로토콜 기반 > 클라이언트와 서버 사이에 지속적인 양방향 언결 스트림을 만들어 주는 기술! 
    -  WebSocket을 사용하면 클라이언트와 서버가 메세지를 자유롭게 주고 받을 수 있다

- 

- ### 자바와 c의 차이점

- - **C언어** 

  - - C같은 경우는 리눅스용, 윈도우 , 맥용        실행파일을 따로 따로 만들어 내야한다. 
    - 각각의 플랫폼에 따라서 실행파일을 만들어내야한다.
    - C는 실행파일에 종속적이다
    - C는 절차지향 
    - 상대적으로 빠름 
    - 직접 메모리를 제어해야함 

  - **JAVA**

  - - 상대적으로 느림
    - java 는 객체지향 
    - java는 jvm이 제어해줌 

- - **C++**

  - - C++ 도 객체지향 
    - 소스코드를 기계어로 번역 > 이를 운영체제가 실행됨 

- - **c++ ->       동작방식 /문법 설명(ex> 깊은복사 얕은복사 ,포인터 )**
  - **c++에서 소멸자를       쓰지 않고 어떻게 메모리를 해제할 수 있나**

-  

- ## Ios

- ### swift

-  

- - **ios 생명주기** 

- viewDidLoad : ViewController가 처음 호출 될 때  viewWillAppear : ViewController가 화면에 나타나기 직전에 호출 viewDidAppear :  ViewController가 화면에 나타난 직후에 호출 viewWillDisappear : ViewController가 화면에 사라지기  직전에 호출 viewDidDisappear : ViewController가 화면에 사라진 직후에 호출

- 

- ![Not  Running  Suspended  Launch Screen UI  Inactive  Background  App UI  Active  Inactive ](data:image/png;base64,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)

- 출처: [[https://medium.com/@jgj455/%EC%98%A4%EB%8A%98%EC%9D%98-swift-%EC%83%81%EC%8B%9D-%EC%95%B1-%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0-878dfe51d182](https://medium.com/@jgj455/오늘의-swift-상식-앱-생명주기-878dfe51d182)  ](mailto:[https://medium.com/@jgj455/오늘의-swift-상식-앱-생명주기-878dfe51d182](https://medium.com/@jgj455/오늘의-swift-상식-앱-생명주기-878dfe51d182))

- - **UIApplication , AppDelegate** 

  - - UIApplication 앱이 해야할 중요하고 핵심적인 일, 앱의 생명주기 관리나 이벤트 처리 같은 것들을 담당하고 AppDelegate 는 커스텀코드를 처리함 
      - @UIApplication 어노테이션을 찾아 해당하는 클래스 실행 이때 AppDelegate 클래스에 작성된        application(_:didFinishLaunchingWithOptions:)메소드가 시스템에 의해 자동으로 호출됨 

- ---------------------

- 

-  ## Spring

- 1. **Spring ioc에 대해 아는대로 설명해라**

- 2. **MVC 패턴에대해 설명해라**

- 3. **http protocol의 작동 원리에대해 설명해라**

- 4. **Rest API란 무엇인지 설명해라**

- 5. **ResT API를 개발할 때 어떻게 개발하면 좋을지?**

- 6. **maven의 장점**

- 7. **Http method 설명**

- 8. **통신 오류 코드**

- 9. **Java Main method에서 static의 의미**
  10. **Java 8의 장점**

- 11. **Spring boot 실행 원**

- 12. **Truncate**

  13. **pk가 왜 테이블당 하나만 생성 가능한지?**

      

- ## Front-End

- - **웹페이지란?**
  - **웹이란?**

- - **html5란?**

  - **css3란?**

  - **html/css/javascript란?**

  - **html에서       자주쓰이는 tag, 각 tag의 기본 속성**

  - **form tag란?**

  - **웹페이지에서 입력양식 > 로그인 창이나 회원입 폼이 해당된다.**

  - **html에서 link  / script/meta/body/header/title tag들 알기**

  - **tag에서 id,       class,,, event과 attribute 들 파악**

  - **기본 html       template**

  - **selector에 대해서**

  - **css의 기본적인       문법**

  - **css/less/sass차이알기**

  - **css의 box       model**

  - **css에서       position/block/z-index에 대해서**

  - **z-index 쌓임맥락**

  - **css 명명규칙**

  - **javascript의       기본 타입들**

  - **js가 다른 언어랑       다른 점 / 장점 / 단점 / 특성**

  - **js의 event       특징 (버블링, 캡쳐링)**

  - **click /       focus 같은 event 동작원리**

  - **js event       listener 등록, 해제 방법**

  - **js에서 레퍼런스       참조 상관관계**

  - **js에서 this란?       this의 상대성**

  - **js 호이스팅 / 클로저 (**[**https://m.blog.naver.com/jaemin-jeong/221877574892**](https://m.blog.naver.com/jaemin-jeong/221877574892)**)**

  - - 클로저: 어떤 외부 수가 특정 내부함수를 포함하고 있을때, 외부함수보다 내부함수가 더 오래 살아있을 경우에는 외부 함수 밖에서 내부함수를 호출해도 외부함수의 지역변수에 접근가능하다.
    - 호이스팅: 끌어올리기> 변수(함수) 선언 및 초기화시 변수가 유효 범위의 최상단으로 올려져 해석됨 >>> 변수는 var로 선언되었을 때만 가능 , 함수는 함수선언문일 경우에만 가능 

  - **key event와       mouse event 란?**

  - **callback / promise / async, await 란? 차이는?** ([https://techlog.io/Javascript/General/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EB%B9%84%EB%8F%99%EA%B8%B0%ED%86%B5%EC%8B%A0-callback-promise-async-await-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0/](https://techlog.io/Javascript/General/자바스크립트-비동기통신-callback-promise-async-await-이해하기/))

  - - Callback: 함수,int,string 등등으로 받아 인자로 받아들인 함수를 다시 호출하는 기능 
    - Promise : promise 는 작업이 끝난 후 실행할 함수를 제공하는 것이 아니라 promise 자체 메소드인 .then()을 호출함 .then()을 연속적으로 사용가능 하기 때문에 콜백지옥에서 벗어날 수 있음 
    - Async/await : promise 보다 쉽게 비동기적 상황 표현가능함 async안에서만 await 키워드 사용가능. > await는 함수작업이 끝나고 결과값 반환할 때까지 대기하고 결과값 리턴하면 다음작업으로 넘어감 

  - **es5, es6 문법 차이? 개념?**

  - **chrome  inspector로 디버깅 하는 방법 (console.log 제외)**

  - **vue.js /angular / react / jquery의 차이점**

  - - Vue : 상대적으로 배우기 쉽고 component 같은 기능을 채하여 사용하고 있음 ,
    - Angular : app개발에 필요한 모든 것을 제공 
    - React : guide문서 잘되어있음, 완전한 프레임워크가 아니라 third-party라이브러리 필요

  - **ajax?  axios?**

  - - Ajax : jQuery 포함되어있을때
    - Axios 는 더쉽게 사용할 수 있음 

  - **로컬서버 / 웹서버 / WAS / 톰캣 / 아파치 차이?**

  - - 아파치 : http 웹서버 > 
    - Web server : 클라이언트 요청을 기다리고 요청에 대한 데이터를 만들어서 응답하는 역할을 함 , 데이터는 정적인 데이터 한정 
    - 톰캣 : 일반적이고 많이 사용되는 was 
    - Was 서버 : 웹서버, 웹컨테이너 결합으로 다양한 기능을 컨테이너에 구현하여 다양한 역할수행. 동적인 데이터 처리 (DB연결 ,데이터 조작)
    - 웹컨테이너를 사용하면 톰캣사용 

  - **웹앱 / 웹페이지 /앱 / 하이브리드 웹앱 이란? 그들의 차이?**

  - - 네이티브앱 : 어플리케이션 , 안드로이드sdk, ios기반sdk 를 이용해 만드는 앱
    - 성능이 좋음 , 네이티브api호출로 플랫폼과 밀착
    - 하이브리드앱 : 네이티브앱 + 웹앱 ,네이티브웹에 웹view 띄움, 양쪽api 모두 사용가능 
    - 모바일 웹앱 : 모바일웹 네이티브앱 결합한 웹기술로 개발되고 모바일 브라우저에서 실행 됨 
    - 플랫폼 api를 사용할 수 없고 오로지 브라우저 api만 사용가능 

  - **SPA / MPA 란?선**

  - - SPA : 서버로 처음에만 페이지를 받아오고 그이후에는 동적으로 페이지를 구성해서 새로운 페이지를 받아오지 않는 웹 어플리케이션 (빠르고 단순함, 디버깅 쉬움,보안취약)        >뷰등등
    - MPA : 서버로부터 완전한 페이지를 받아오고, 이후에 데이터 수정하거나 조회할때 다른 완전한 페이지로 이동 (화면전환). 전통적인 어플리케이션 방식.

  - **webkit관련하여  MDM 보는 방법**

  - **webpack /babel 이 무엇인지? 어떨때 사용하는지?**

  - - webpack : 모듈 번들러 > 하나의 파일을 모아 하나의 js 파일로 만들어줌 보통 bundle.js
    - Babel : es6문법을 es5로 변환해주는 트렌스파일러 

  - - <https://beomi.github.io/2017/10/18/Setup-Babel-with-webpack/>

  - **로드벨런싱이란?**

  - **로드벨런싱으로 서버를 여러대로 분리해 놓으면 로그인과 같은 session, cookie를 이용할 때 서로 데이터 공유는 어떻게 하나요?**

  - **http에 대해 설명해봐라**

  - - 텍스트 기반의 통신규약 > 인터넷에서 데이터를 주고받는 프로토콜 
    - 클라이언트가 브라우저를 통해서 url을 통하거나 다른것을 통해 request를 하면 서버는 해당 요청사항과 맞는 결과를 찾아서 사용자에게 응답하는 형태로 동작한다. 
    - 연결상태 유지 x , 비연결성 프로토콜 > 단점해결하기 위해 쿠키 세션이 등장함 

  - **http의 연결을 유지시켜주는 방법이 있나?**

  - **세션관리는 어떻게 했나?**

  - **웹 페이지를 껏다 켜도 로그인이 안풀리게 하려면 어떻게 해야되나?**

  - - 로컬 세션 , 쿠키 사용 

- **쿠키와 세션에 대해 설명해봐라.**

  - 쿠키 : 서버에서 클라이언트에게 어떤 정보 저장시킴 (xss csrf공격에 취약함 ) > 클라이언트에 저장
  - 세션 : 서버에 저장 , 서버에서 세션ID발행하여 관리 , 보안적인 측면에서 우수함 
  - 캐시 : 요청에 대한 응답리소스의 복사본을 저장함        
  - 쿠키는 자신의 컴퓨터에 있는데 결국 다른사람한테 노출되지 않는거 아니냐?
  - 세션 사용 

- **http 매소드 get, post, put, delete 각각의 특징에 대해 말해봐라**

  - get 자료요청(url담아 전송, 길이제한 ,주소창 노출 ) , post 자료 생성 요청(body에 담아서 전송 , 길이제한 없음 , 주소입력창에 노출 안됨 ,수정 혹은        삭제에 사용 ) , put 자료 수정 , delete 자료 삭제

- **typescript의  철학은 무엇이며 왜 나왔는가?**

- **react와 vue는 어떤 차이점이 있는가?**

- **react를 왜 사용하는가?**

- **react  component의 생명주기에 대해 설명해봐라**

- **react  component의 리렌더링을 최대한 회피하는 방법은 무엇인가?**

- **let과 const의 차이는 무엇인가?**

- **왜 const를 자주 사용해야 하는가?**

- ## etc

- - 어플리케이션 레벨에서  성능 좋아지게하려면? >힌트 :  스토리지 하드디스크 특성 있음 > 하드디스크에서 읽을때 메모리에서 읽을때 

  - 현재 웹앱서비스 뭐함 ?? 구조 그려보세요

  - 뭐하고있나요?? api플로우 등을 설명하세요

    현재 진행하고 있는 일 > 스프링부트가 어느 모듈에해당되나 어떻게 구성되어있나? DB같은거라던지 api라던지 

    왜 웹앱으로 갔나?

  - **앱을 개발했으면       클라이어느는 JAVA로 했고 WAS 는 node, 디비는 mysql을 썻고 db에있는 데이터를 웹페이지에 json형태로 출력한다음       파싱해서 앱에 출력했다.**

  - **AWS S3사용해서       파일저장했다고했는데 S3내부구조가 어떻게 되있을거 같나? 그리고 node.js사용했다고했는데 node.js의 동작방식이 어떻게       되는지? 자바랑 차이는 뭔지?? php,루비,java등 cgi언어는 많은데 왜 굳이 node를 사용했는지? 테이블 디비 설계할때       인덱스관련해서 저는 기본키만 지정해줬는데 인덱스왜 지정안해줬나?**

  - **주로 오류가 발생했을       때 어떻게 해결했나?**

  - **형상관리 툴       써본거있나? (git, sourceTree)**

  - **s3 내부구조?**

  - **기술적으로 자신있는       부분은?**

  - **worker는 어떤       방식으로 콜백을 호출하나?**

  - **개발해보고 싶은       프로젝트가 있나?**

  - **md5에 대해       설명해봐라**

  - **md5의****c**       **hash값을 알면 원본값을 복원할 수 있나?**

  - **왜 웹 개발자가 되려고 결심했는가?**

  - **개발에서 불변성이 왜    중요한가?**

  - **가장 최근 기억에       남는 시각화 기술은 무엇인가?**

  - **프로젝트에 사용한       기술 스택은 무엇인가?**

  - **부스트캠프는 몇       명이서 진행했으며, 팀원 간 트러블은 없었는가?**

  - **프로젝트를 진행하면서       기억에 남는 외부 라이브러리는?**

  - **monaco       editor를 사용할 때 불편했던 점이 있었나?**

  - **에디터에서 텍스트의       양이 많을 때 일어날 수 있는 문제점은 무엇인가?**

  - **웹 접근성의       국제표준이 무엇인가?**

  - **자신이 어떤 특색을가진 FE 개발자라고 생각하는가? (진짜 제일 어려웠던 질문)**

  - **분산 시스템에 대해서 공부해본 적 있는가?**