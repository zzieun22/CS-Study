# 운영체제 tip

### synchronization 이란?

멀티 스레드에서 여러 스레드가 하나의 프로세스의 자원을 동시에 접근할 때 (critical region) race condition이 발생할 수 있으므로 스레드간에 동기화가 필요하다.

-> 경쟁 상황으로부터 보호하기 위해 한 순간에 하나의 프로세스만이 공유자료를 조작하도록 보장하는 작업 



### aging 기법이란?

기아현상(starvation) : 스레드에 cpu할당이 평등하게 배부되지 못하고 어떤 스레드드는 무한정 기다리는 현상이 발생함 

-> 에이징 기법: 기아현상을 해결하기 위한 기법으로 대기시간이 경과할 수록 우선순위를 높여주는 방법 -> HRN = SJH +aging 



- Critical Sction : 공용데이터에 접근하는 부분은 Critical Section 혹은 Critical Region이라고 부른다. 따라서 프로세스는 어떤 두 프로세스가 동시에 Critical Region 에 들어가지 않도록 한다면 race condition을 막을 수 있다.

### race condition 이란?

2개 이상의 프로세스가 공유 자원을 동시에 읽거나 쓸 때 발생하는 문제입니다.(프로세스끼리 하나의 자원을 갖기위해 싸우는 것 - 하나의 자원을 동시에 요청)

이 상황이 발생하게 되면 모든 프로세스에 원하는 결과가 발생하는 것을 보장할 수 없으므로 이러한 상황을 반드시 피해야한다.



-Mutual Exclusion : Race condition 을 해결하기 위해서는 **두 개 이상의 프로세스가 공용데이터에 동시에 접근하는 것을 막아야 한다.** 즉, 한 프로세스가 공용데이터를 사용하고 있으면 다른 프로세스가 그 자원을 사용하지 못하도록 막는다면 race condition 을 막을 수 있다.



### semaphore 설명? 구현?

공유자원에 접근할 수 있는 최대 허용치만큼 동시에 사용자가 접근할 수 있게 한다. mutex와 비슷하지만 가장 큰 차이는 **뮤텍스**는 동기화대상이 오직 하나뿐이지만 **세마포어**는 동기화대상이 하나이상일 때 사용한다.



```
int i = 0; //전역변수
i+=10; //스레드에의해 두번실행
```

ex> A,B 두개의 스레드가 동시에 위 코드를 실행한다면?

스레드는 stack을 제외한 영역을 공유한다. 

- 전역변수인 i는 data영영이므로 모든 스레드에 의해 접근가능하다 
- 프로세스는 context switching을 통해 할당시간을 나누는데, 스레드도 마찬가지므로, 동시에 실행하는 것 처럼 보이지만 CPU는 한순간에 하나의 스레드만 실행한다.
- A스레드는 메인메모리에 ` i=10`의 값을 저장한 후, 임시 메모리에 i=10의 값을 옮긴다. 그리고 10을 더하여 임시메모리값을 20으로 만들고 메인메모리에 저장하려고 하는데, 그 전에 할당받은 시간이 끝나 B스레드가 동작한다면? (context switching이 일어난것)
- A스레드는 다시 할당받기 전까지 다른 메모리공간으로 옮겨지고 B스레드가 실행된다.
- B는 위와같은 일을 반복한다. 임시 메모리에 10저장하고 더해서 20만들고 메인메모리 i값에 20을써준다. 
- 이제 메인메모리는 i = 20값이 써있다. 이제 context switching으로 중단되었던 A스레드가 마지막 작업인 임시메모리에 저장된 값을 메인메모리에 써주는 일을 한다. A스레드가 임시메모리에 20을 만들었으므로 A는 20이라는 값을 또 쓰는것 그려면 결과는 ` i= 20 `이된다.

--> context swiching을 연산단위로 하지 않고 시간단위로 나뉘었기 때문에 이런 문제가 발생한다. 



**동기화(synchronization)**매커니즘을 통해서 해결할 수 있다.

1. 공유된 메모리에 둘 이상의 스레드가 동시에 접근할때 생기는 문제점 (하나가 접근하는 동안 다른하나는 접근못하도록 막아줌)
2. 스레드 실행순서를 control  ex> A, B 스레드가 있을때, A는 데이터를 가져다놓는 스레드 B는 데이터를 가져가는 스레드라고 할때, 반드시 A스레드가 실행 된 후 B스레드가 실행되도록하여 실행순서를 제어하는 방법을 사용하면 된다.

이때 동기화하는데 있어서 **뮤텍스, 세마포어**를 사용한다.

뮤텍스

```
 #include<stdio.h>

   #include<unistd.h>
   #include<stdlib.h>
   #include<pthread.h> // 쓰레드,뮤텍스관련
  
   void * thread_increment(void * arg);
   char thread1[] = "A thread";
   char thread2[] = "B thread";
  
  pthread_mutex_t mutx;
  //전역변수 number선언
  int number=0;
 
  int main(int argc, char **argv){
      pthread_t t1,t2;
      void *thread_result;
      int state;
 
      //뮤텍스를 초기화 합니다.
      state = pthread_mutex_init(&mutx,NULL);
      if(state) puts("Error mutex initialization");
 
      //2개의 쓰레드를 생성합니다.
      pthread_create(&t1,NULL,thread_increment,&thread1);
      pthread_create(&t2,NULL,thread_increment,&thread2);
 
      //프로세스가 쓰레드 종료후 종료되도록 하는것
      pthread_join(t1,&thread_result);
      pthread_join(t2,&thread_result);
 
      printf("최종 number : %d\n",number);
      pthread_mutex_destroy(&mutx); //뮤텍스 종료함수입니다.
      return 0;
  }
 
  //쓰레드에 의해 실행되는 루틴
  void *thread_increment(void *arg){
      int i;
      for(i=0;i<5;i++){ //여기 for문을 critical section이라고 할수있다!
         pthread_mutex_lock(&mutx);//임계영역 들어가기전 뮤텍스를 걸어줌
         sleep(1); // 없어도됨
         number++;
         printf("실행 : %s, number : %d\n",(char *)arg,number);
         pthread_mutex_unlock(&mutx);//임계영역 나가며 뮤텍스 풀어줌
     }
 }
```



세마포어

```
 #include<stdio.h>

   #include<unistd.h>
   #include<stdlib.h>
   #include<pthread.h>
   #include<semaphore.h>
  
   void * thread_snd(void *arg);
   void * thread_rcv(void *arg);
 
  sem_t bin_sem; //세마포어~~
  int number = 0; //전역변수, 모든쓰레드 접근가능
 
  //세 개의 쓰레드
  //여기서 A쓰레드는 number를 1로만들고, B,C는 number를 0으로 만듭니다.
  char thread1[] = "A thread";
  char thread2[] = "B thread";
  char thread3[] = "C thread";
 
  int main(int argc, char **argv)
  {
      pthread_t t1,t2,t3;
      void * thread_result;
      int state;
 
      state = sem_init(&bin_sem,0,0); //초기화, 처음에 0으로설정
      if(state != 0) puts("Error semaphore initialization");
 
      //쓰레드를 생성합니다.
      pthread_create(&t1,NULL,thread_snd,&thread1);
      pthread_create(&t2,NULL,thread_rcv,&thread2);
      pthread_create(&t3,NULL,thread_rcv,&thread3);
 
      //프로세스가 먼저 종료되어 쓰레드가 중간에 종료되지않도록합니다.
      pthread_join(t1,&thread_result);
      pthread_join(t2,&thread_result);
      pthread_join(t3,&thread_result);
 
      printf("최종 number : %d \n",number);
      sem_destroy(&bin_sem); //세마포어 소멸
      return 0;
  }
 
  void * thread_snd(void * arg){
      int i;
      for(i=0;i<4;i++){
          while(number != 0) //만일 number가 0이 아니라면
              sleep(1); // number=0이될때까지 기다립니다.
          number++;
          printf("실행 : %s, number : %d\n",(char *)arg, number);
          sem_post(&bin_sem); //세마포어를 1로 만드는것!!
      }
  }
 
  void * thread_rcv(void * arg){
      int i;
      for(i=0;i<2;i++){
          sem_wait(&bin_sem); //세마포어를 0으로 만드는것!!
          number--;
          printf("실행 : %s, number : %d\n",(char *)arg, number);
     }
  }

 
```

