

- **작성자** : 박지은
- **최초 작성일** : 21. 03 .17
- **마지막 수정일** : 21. 03. 27

## Spring Boot 목차

[1. Spring Boot 초기 설정](#SpringBoot초기설정)

[2. Annotation](#Annotation)

[3.API동작](#API동작)

[4. jdbc](#jdbc)

[4.JPA](#JPA)



## SpringBoot초기설정

1. JDK 내가 가지고 있는 1.8.0으로 설정 (하고싶다면?)

![1615959392779](https://user-images.githubusercontent.com/36434665/111465516-90758680-8765-11eb-97d3-28a4d20f7ad9.png)

#### RUN 하기 전 

9000포트로 설정 

![1615959461135](https://user-images.githubusercontent.com/36434665/111465564-9e2b0c00-8765-11eb-9488-4bacb6f402c8.png)



gradle 빌드하기 

![1615959765199](https://user-images.githubusercontent.com/36434665/111465568-9ec3a280-8765-11eb-9114-58aac1ea87b4.png)



### 프로젝트 실행 시 오류났을 때

IntelliJ 기본 클래스을 를 찾 거나 로드 할 수 없습니다

오류가 있었음 

![1615966524071](https://user-images.githubusercontent.com/36434665/111465570-9ec3a280-8765-11eb-9e2a-a32684ce9591.png)

여기서 Before Launch 삭제 하면 된다. 



## vue.js와 연동 

```
npm install -g @vue/cli /npm을 이용한 vue cli 전역 설치
vue create my-project // vue 설치 
```

vue.js 프로젝트는 vsCode 로 관리 



```
사용자 ---> localhost :8080 (vue.js web서버) ----> localhost:9000(spring boot was 서버)
```

의 형태 이다. 



#### proxy 설정 

```
npm install request
npm install path 
// 모듈 깔기 
```



1. vue.config.js 생성하여 아래 내용 적어주기

```javascript
module.exports = {
    devServer: {
        proxy: {
            '/api' : {
                target: 'http://localhost:9000',
                ws: true,
                changeOrigin: true
            },
        }
    }
}
```

/api형태로 날리면 로컬호스트 9000번으로 request보낸다는 의미 



2. App.vue 에서 request 날려보기 

![1615970343881](https://user-images.githubusercontent.com/36434665/111465572-9f5c3900-8765-11eb-9b32-a9283d20e1c1.png)



3. 빌드 타깃 디렉토리 생성

보통 그냥 빌드하면 dist 디렉토리가 만들어지고 결과물이 생긴다.

이것을 spring boot의 main/resource/static밑에 바로 생기게 해두면 편해짐 

```
const path = require('path')

module.exports = {
    outputDir: path.resolve(__dirname, "../" + "main/resources/static"),
    
    ...
 }
```

```
 npm run build
```

https://deockstory.tistory.com/26 참고



#### Appliaction class 

프로젝트의 메인이 되는 클래스

#### @SpringBootApplication 

스프링 부트의 자동설정 , Bean 읽기와 생성 자동설정 

1. @SpringBootConfiguration

2. @ComponentScan

3. @EnableAutoConfiguration

   이 세개가 합쳐진것 

#### SpringAppliction.run

내장 WAS 를 실행하는 메서드 



## Annotation

### Bean 이란? 

애플리케이션의 핵심을 이루는 객체 , Spring IoC컨테이너에 의해 인스턴스화 ,관리 생성이 된다. 

애플리케이션의 객체가 지정되면 해당 객체는 **getBean()**메서드를 통해 가져올 수있다.

애플리케이션 구동 시 JVM안에서 스프링이 bean마다 하나의 객체를 생성하는 것을 의미 (**Singleton** : 하나의 Bean 정의에 대해서 Spring IoC Container내에 단 하나의 객체만 존재한다 )



#### 빈 등록

@ComponentScan 어노테이션과 @Component어노테이션을 사용해서 빈을 등록해준다.



스프링 빈 컨테이너가 빈을 생성해줌 , 스프링 빈 컨테이너는 생명 주기를 관리한다. 

컨테이너 종류 **ApplicationContext**, **BeanFactory** 2가지로 나누어짐 



#### ApplicationContext

구현하고 있는 클래스의 객체관리 및 의존성 주입을 가능하게 해줌 

object 생성, 관계설정 ,자동 생성 , 후처리 등등 BeanFactory를 상속받고 있음 



#### ApplicationContext vs BeanFactory

1. 인스턴스화 하는 시점이 다름

   - AppliactionContext : pre-loading
   - BeanFactory : lazy -loading 

2.  AppliactionContext  : 

   - 스프링이 제공하는 Appliation 지원기능
   -  Bean의 생성, 조회, 등록 등을 담당

   - @Configuration어노태이션이 붙은 자바 파일이나, xml로 만든 <beans로 시작하는 appcontext를 설정정보로 등록하고 @Bean이 붙은 메소드의 이름을 가져와 빈 목록을 만듦

3.  BeanFactory: 

   -  빈생성과 제어 관점  
   - 중요 기능인 Bean 생성, 조회, 등록을 그대로 받고 여기에 스프링에 제공하는 부가기능을 추가로 제공



@Controller 

- 빈등록이 된다.

@Autowired 

- 스프링에 등록되어있는에있던 객체를 가져온다. 
- controller <->service 와 연결시켜줘야한다. 

@Service 

- controller <->service 와 연결시켜줘야한다. 

![22](https://user-images.githubusercontent.com/36434665/113475361-160c6c80-94b0-11eb-840f-ea95db1402cc.PNG)



스프링 컨테이너에 빈으로 등록됨 

> 이걸 컴포넌트 스캔이라고 한다. 



!!참고 : 스프링 컨테이너에 스프링 빈을 등록할때, 기본으로 싱글톤으로 등록한다. 유일하게 하나만 공유!  그래서 같은 스플이 빈이면 같은 인스턴스 이다. 



## API동작

#### @ResponseBody 동작

- HTTP의 BODY에 문자 내용을 직접 반환한다.
-  `viewResolver` 대신 `HttpMessageConverter` 가 동작한다.
- 기본 문자처리 `StringHttpMessageConverter`
- 기본 객체처리 `MappingJackson2HttpMessageConverter` > 객체를 제이슨으로 만들어줌 

![test](https://user-images.githubusercontent.com/36434665/113475118-a21d9480-94ae-11eb-845a-9bc7e9228e7c.PNG)





# 스프링 DB 



## JDBC

- jdbc 그레이들 의존성 추가 
- 접속정보 : application.properties > url, driver class 추가 
- h2 database 의손성 및 버전정보 추가 (H2 내장 데이터베이스 사용)

jdbc지원은 jdbcTemplate 클래스 기반을 둔다. 관계형 데이터베이스에 대한 SQL연산을 수행할 수 있는 방법을 제공한다. 



ingredientRepository.interface

```java
public interface IngredientRepository{
	Iterable<Ingreient> findAll();
	Ingredient findByIf(String id);
	Ingredient save(Ingreident ingredient);
}
```

jdbcTemplate를 이용해서 데이터베이스 쿼리에 사용할 수 있도록 Repository 인터페이스 구현 



JdbcIngredientRepository.java

```

..
@Repository
public class JdbcIngredientRepository implement IngredientRepository{
	private JdbcTemplate jdbc;
	
	@Autowired
	public JdbcIngredientRepository(JdbcTemplate jdbc){
		thils.jdbc = jdbc;
	}
	
	@Override
	public Iterable<ingredient> findAll(){
		return jdbc.query("select id,name,type from Ingredient",
			this::mapRowToIngredient)
	}
	
	@Override
	public Ingredient findById(String id){
		return jdbc.queryForObject("select id,name,type from Ingredient where id =?",
			this::mapRowToIngredient)
	}
	
	@Override
	public Ingredient mapRowToIngredient(ResultSet rs, int rowNum)
		throws SQLException {
			return new Ingredient{
				rs.getString("id"),
				rs.getString("name"),
				Ingredient.Type.valueOf(rs.getString("type"));
			}
		}	
}
```

**@Repository 이노테이션이란?** 

스프링 컴포넌트 검색에서 이 클래스를 자동으로 찾아서 스프링 애플리케이션 컨텍스트의 빈을 생성해준다. 

그리고 JdbcIngredientRepository 빈이 생성되면 @Autowired를 통해서 스프링이 해당 빈을 JdbcTemplate에 연결한다. 

JdbcIngredientRepository 생성자는 JdbcTemplate 참조를 인스턴스 변수에 저장한다. 이 변수는 데이터베이스의 데이터 쿼리하고 추가하기위해 다른메서드에서 사용될 것이다. 



findAll , findById 둘다 JdbcTemplate를 사용한다. 객체가 저장된 컬렉션을 반환하는 findAll() 메서드는 JdbcTemplate 의 qeury() 메서드 사용함 , List 형태로 반환한다. 

queryForObject()메서드는 qeury()과 동일하게 실행되지만 객체의 List대신 하나의 객체만 반환된다. 

두 메서드 다 다른 메서드 mapRowToIngredient 를 참조하는데 이는 **람다** 때문 



#### 람다 

**람다함수란?**

람다 함수는 프로그래밍 언어에서 사용되는 개념으로 **익명 함수(Anonymous functions)를 지칭**하는 용어

 람다식으로 선언된 함수는 1급 객체이기 때문에 Stream API의 매개변수로 전달이 가능

**장점**

- 코드의 간결성 - 람다를 사용하면 불필요한 반복문의 삭제가 가능하며 복잡한 식을 단순하게 표현가능 

- 지연연산 수행 - 람다는 지연연상을 수행 함으로써 불필요한 연산을 최소화 

- 병렬처리 가능 - 멀티쓰레디를 활용하여 병렬처리 가능 



**단점**

- 람다 호출 까다로음 

- 람다 stream 사용 시 단순 for문 혹은 while문 사용 시 성능이 떨어짐

- 불필요하게 너무 사용하게 되면 오히려 가독성을 떨어 뜨릴 수 있음

```java
// 기존의 방식
반환티입 메소드명 (매개변수, ...) {
	실행문
}

// 예시
public String hello() {
    return "Hello World!";
}

// 람다 방식
(매개변수, ... ) -> { 실행문 ... }

// 예시
() -> "Hello World!";
```



## JPA

- JPA 기존의 반복코드는 물론 , 기본적인 SQL도 JPA가 처리를 해줌 
- SQL, 데이터 중심 설계에서  객체 중심의 설계로 패러다임 전환 할 수 있음 

- JPA는 표준 인터페이스 / 구현체로 hibernate가 있음
- JPA은 ORM(객체랑 관계형 데이터베이스) 기술

#### 설치 

- gradle 의존성 추가 (~~ data-jpa)

- application.properties 에 jpa 설정 추가  

- ```
  spring.jpa.show-sql=true
  spring.jpa.hibernate.ddl-auto=none
  ```



ex>

```
package com.example.jieundemo.webservice.domain.posts;

import lombok.AccessLevel;
import lombok.Builder;
import lombok.Getter;
import lombok.NoArgsConstructor;
import org.springframework.boot.autoconfigure.domain.EntityScan;
import org.springframework.data.annotation.Id;


import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;

@NoArgsConstructor(access = AccessLevel.PROTECTED)
@Getter
@Entity
public class Posts {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "userName",length = 500, nullable = false)
    private String name;
    
    public void setId(Long id){
    ..
    }
    ...

}
```

DB와 매핑될 자바 클래스를 만든다. 이 자바클래스가 Entity클래스 라고 함

#### JPA 어노테이션

- @Entity
  - 테이블과 링크될 클래스 
  - _ 으로 이름을 매칭함 
  -  이제부터 JPA가 관리하는 엔티티 
- @Id
  - pk필드 
- @GeneratedValue
  - pk생성 규칙
  -  @GeneratedValue(strategy = GenerationType.**IDENTITY**) 
    - insert할 때 db가 id를 자동 생성해줌 >> identity 하고 한다. 이 전략을 취하겠다.
- @Column
  - 테이블 컬럼을 나타내면 굳이 선언하지 않더라고 해당 크래스의 픽드는 모두 컬럼이 된다.
  - 기본값이외에 변경필요한 옵션이 있음 사용함
  - @Column(name = "userName",length = 500, nullable = false)
    - name = 이거 없으면 컬럼명은 그냥 name/ 있으면 컬럼명 userName으로 매핑된다.



```
package com.example.jieundemo.webservice.domain.posts;

import org.springframework.data.jpa.repository.JpaRepository;

public interface PostsRepository extends JpaRepository<Posts, Long> {
	private final EntityManager em;
	
	...
	
	@Override
	public Member save(Member member){
		em.persist(member); 
		return member;
	}
	@Override
	public Optional<Member> findById (Member member){
		Member member = em.find(Member.class, id);
		return Optional.ofNullable(member);
	}
	
	@Override
	public Optional<Member> findByName(Member member){
		return em.createQuery(qlString: "select m from Member m where m.name = :name", Member.class)
		.setParameter(name:"name",name)
		.getResultList();
	}
	
	@Override
	public List<Member> findByAll(Member member){
		return em.createQuery(qlString: "select m from Member m", Member.class)
		.getResultList();
	}
}

```



- `EntityManager` 이란 ?

  JAP는 EntityManager로 모두 동작한다.  application.properties 에 jpa 설정을 했다면 스프링 부트가 자동으로 세팅을 해줌 

- 위와같이 save 함수를 적으면 JPA가 insert 쿼리를 만들어 넣어준다. 

- findById 함수는 조회 (pk)

- findByAll 은 jpql이라는 객체지향 쿼리를 써야한다.

  - 객체 대상으로 쿼리를 날림 
  - Memeber 라는 Entity를 조회함 , 객체 자체를 쓴다.

- **주의사항** : 데이터를 저장하고 변경할때는 항상 @ransactional이 있어야한다. (~Service.class 에 넣어준다)

  

https://jojoldu.tistory.com/251?category=635883 / 김영한의 스프링 (인프런)

​	





