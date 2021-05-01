

# AWS Cloud 개발 핵심 

1day : aws 개발 소개와 기초내용 

2day : aws기반 개발시 데이터베이서 선택과 사용 

3day : 서버리스 기반 개발과 ci/cd이해와 devops

> github; aws 개발 코드 모음 참고 

- free tier 계정을 이용하여 실습 

Day 1

목차 

- aws cloud 관리콘솔과 계정의 이해

- 프로그래밍 언어의 선택과 ide도구 

- aws sdk 와 cdk이해와 솔루션 개발 

## aws cloud 관리콘솔과 계정의 이해

클라우드 컴퓨팅은 획기적인 기능을 더욱 빠르게 개발하고 리소스를 유동적으로 사용하는 동시에 요금을 대폭 절약 할 수 있도록 인터넷을 이용해 컴퓨팅 서비스를 제공하는 방식 

구독 ! 돈을 낸 만 큼 제공 



### 퍼블릭 클라우드

- 클라우스 서비스 또는 호스팅 공급자가 소유 
- 여러 조직과 사용자에게 리소스와 서비스를 제공
- 보안 네트워크 연결을 통해 액세스(일반적으로 인터넷을 통해)

### 프라이빗 클라우드 

- 조직은 조직의 데이터 센터에서 클라우드 환경 
- 조직에게 본인들이 제공하는 서비스를 운영할 책임 
- 조직 외부자는 액세스 불가 

> 가상의 디스크 메모리 네트워크 ,, 회사에 연결해서 가상oo를 쓰는것이다.
>
> 가상화를 통해서 물리적으로 자원을 나눠쓰는 것 (VM, hyperV)

### 하이브리드 클라우드

- 퍼블릭 및 프라이빗 클라우드를 결합하여 애플리케이션이 가장 적절한 위치에서 실행 

  

## 클라우드 서비스 - 목표 영역

### IaaS

클라우드 공급자의 서버, 가상머신, 스토리지 , 네트워크 및 운영체ㅔ를 대여하여 종량제 인프라를 구축 

### PaaS

기본 인프라 관리에 집중하지 않으면서 소프트웨어 애플리케이션을 빌드, 테스트 및 배포 할 수 있는 환경을 제공 

> 코딩만 신경쓰자 

### SaaS

사용자는 인터넷을 통해 마이크로오피스365 전자메일 및 캘린더와 같은 클라우드 기반 앱에 연결하고사용 

### 서버리스 컴퓨팅 

서버리스 컴퓨팅 애플리케이션을 사용하는 클라우드 서비스 공급자는 코드를 실행하는데 필요한 인프라를 자동으로 프로비전, 크기 조정 및 관리 



## AWS 시작하기

### AWS 관리콘솔 

모든서비스를 보면 

![1619577675989](https://user-images.githubusercontent.com/36434665/116689586-471a8700-a9f3-11eb-9614-0d9d2892c240.png)



Cloud9 를 주의깊게 보자 

개발자환경을 만들 수 있다 , aws통합 개발 도구 ,개발환경을 만들어 낼 수 있다. 

**비용 관리** 

![1619577752018](https://user-images.githubusercontent.com/36434665/116689588-471a8700-a9f3-11eb-92cd-56c3cc12c0ee.png)



aws비용관리에서 - aws cost explorer 누르면 비용 관련해서 확인 할 수 있다.



### IAM(계정관리)

AWS의 모든 것을 관리하는 곳 



**aws 속성기반액세스제어** 

- ABAC를 통해서 접근을 제어한다.




**자격증명 공급자** aws single sign-on(sso)

- 구글계정등 으로 로그인하는방법? (SAML2.0)

- 멀티클라우드 이용할때 다른 퍼블릭클라우드와 계정 연결 후 다른 퍼블릭 클라우드 관리할 수 있음 

  azure <> amazon <> google 

  

**IAM 대시보드**

오픈스택 : 클라우스에 대한 내용 확인 ? 

개발을 할때 지켜야할 규칙을 만들어 놓은 것 > 오픈스택에서 정의내린대로 구성이 되어있음 

대시보드 > 오픈스택에서 정의를 해두었음 , 전체적으로 항목을 다 볼수 있도록 해둔 것 



**만들어보기**

park 과 lee를 만들었음 

park: 개발만 접근

lee :  관리/콘솔까지 접근 가능

> lee pw : !@#genieGbox



<u>park 추가</u> 

사용자 추가에서 park을 추가함 

aws액세스 유형 선택 x 

![1619579700075](https://user-images.githubusercontent.com/36434665/116689591-47b31d80-a9f3-11eb-849e-b5061b5de905.png)

<u>lee 추가</u>

사용자 추가에서  lee을 추가함

aws액세스 유형 선택 o

![1619579756464](https://user-images.githubusercontent.com/36434665/116689593-484bb400-a9f3-11eb-8a94-93651651fa72.png)

![1619580006670](https://user-images.githubusercontent.com/36434665/116689601-48e44a80-a9f3-11eb-860e-167c7bcae42f.png)



![1619579869697](https://user-images.githubusercontent.com/36434665/116689597-484bb400-a9f3-11eb-89da-c7c25092c189.png)



**IAM로그인** 

![1619579924733](https://user-images.githubusercontent.com/36434665/116689598-48e44a80-a9f3-11eb-8f3a-ea9b14efe3c7.png)

내 계정 ID가 중요하다.  > 내 루트 계정 



**lee 로 로그인 을 해보자** 

IAM계정으로 로그인 내 계정 ID 하고 lee하고 비번치기 

![1619580006670](https://user-images.githubusercontent.com/36434665/116689601-48e44a80-a9f3-11eb-860e-167c7bcae42f.png)

권한이 없으므로 이렇게 나온다.



![1619584574578](https://user-images.githubusercontent.com/36434665/116689603-497ce100-a9f3-11eb-87bc-2a9400572be8.png)

**액세스 키** : 다른쪽 프로그래밍에서 접근 가능하게 만들어줌 / 관리 / 한개의 계정 당 2개 까지 가능하다.

AKIA4JWTQKAJO5QO7MGY



### 개발자 도구

https://aws.amazon.com/ko/products/developer-tools/

aws에서 제공해주는 상품 

aws cloud 9



#### SDK

software develoment kit 

https://aws.amazon.com/ko/tools/?c=dv&sec=srv

언어/ 개발 플랫폼에 맞추어 선택

> 내가 익숙한 언어

도구 : 오픈소스에 기반을 둔 개발도구는 거의 가능하다. 



## VS CODE 

우리는 자바스크립트; node.js python 으로 실습 

python / java / docker / AWS / kubernetes

확장 프로그램 설치 하기



### AWS 탭에서 프로필 작성하기 

Access Key 값이 중요 (개발도구와 연결시 필요하다)



#### 인증

1. f1(팔레트 실행 명령창) 눌러서 **aws create credentials profile** 입력

2. 입력란에 **ID > KEY** 넣으면 완료

   > key 는 aws 루트 계정에서 참고

   ![1619591166683](https://user-images.githubusercontent.com/36434665/116689607-4a157780-a9f3-11eb-8d50-00a599a2588d.png)

| Access key ID        | Secret access key                        |
| -------------------- | ---------------------------------------- |
| AKIA4JWTQKAJGZC6CO7O | YDCkQvJMSS3IUrO8ExtZA2r0l979MBO++u9cJ/YK |

3. 왼쪽탭에 하나 생김  > region 은 **Asia Pacific (Seoul)** 누름 

![1619590923412](https://user-images.githubusercontent.com/36434665/116689605-4a157780-a9f3-11eb-9818-24843f82f7cd.png)



## amazon CDK 인프라 

https://aws.amazon.com/ko/cdk/

인프라 구성 - 익숙한 프로그래밍 구성,설정 

: 멀티 클라우드 또는 aws 클라우드 인프라를 설정하는 별도의 웹 앱을 만들때 사용한다. 

언어용 aws sdk 설치 > 실제 개발자 해야하는일 



python , node.js  는 

https://aws.amazon.com/ko/sdk-for-node-js/

https://aws.amazon.com/ko/sdk-for-python/

설치해서 사용한다. 



깃헙 

https://github.com/aws/aws-sdk-js





### 권한 추가

![1619593526559](https://user-images.githubusercontent.com/36434665/116689611-4aae0e00-a9f3-11eb-84c4-8e89d4a631ee.png)<u>기존 정책 직접연결</u>에서 ![AWS 관리형 정책](https://console.aws.amazon.com/iam/assets/images/policy_icon.png) [AdministratorAccess](https://console.aws.amazon.com/iam/home?region=ap-northeast-2#/policies/arn%3Aaws%3Aiam%3A%3Aaws%3Apolicy%2FAdministratorAccess)

이거는 전체 권한을 주는거라 조심해야한다.보안상 문제가 될 수 있다.  > 추가해보기

![1619593985755](https://user-images.githubusercontent.com/36434665/116689613-4aae0e00-a9f3-11eb-88d8-27c43d1b8e13.png)

![1619594092208](https://user-images.githubusercontent.com/36434665/116689615-4b46a480-a9f3-11eb-9beb-f1ee9d9dac45.png)

권한이 수정됨 



### 개발자도구 

자동화 프로그램 

Front-end  프로그램 / Back-end 프로그램 

서비스 할때 (시스템 배포) 어느 시스템에 배포? 

 : 서버 < > VPC(VM)

=== >>>> 컨테이너(도커) 로 할수있음 

Zero Trust 참조 





### SDK 설치 

윈도우 환경 

python sdk 설치

 https://www.python.org/downloads/

Docker sdk 설치 

- CE :  오픈소스  / EE : 엔터프라이즈용 돈받고 서비스하는 것 
- 개발용 PC - 가상화 지원? 

작업표시줄 검색에서 msinfo32 쳐서 

![1619596880330](https://user-images.githubusercontent.com/36434665/116689617-4b46a480-a9f3-11eb-9885-cac8eefde602.png)

이거면 가상화 지원하는 컴이다 

window10 home/ pro냐에따라 설치방법이다름 

가상화기술 선택 **Pro** : 로컬에 hyper-V기능 설치

​										virtual box

Docker 설치 

**Home** : virtual box 설치 

​				Docker 설치 

https://www.docker.com/products/docker-desktop

도커 데스크탑 설치 

계정만들기 

도커닷컴에 이미지 넣고 배포하는 연습할거야 



1. python 3.7이상 설치 
2. virtualbox 설치
3. docker desktop설치 및 아이디 로그인 

------------------------------

Day2

목차

- AWS데이터베이스의 이해와 RDS서비스

- S3저장소 데이터 활용과  python프로그래밍

- VPC그룹의 가상머신과 데이터베이스의 활용



우린 프리티어에서 

Amazon RDS  를 사용 할거야 

DB운영: 서버, os/db/ 관리 , 성능/운영 모니터링 

> 가용성 / 고가용성이여야한다. 



접속 : 인터넷을 통한 Database 접속 

vpn/zero trust 확인 

방화벽



우분투 +  MariaDB를 사용한다면 ? 



RDB(관계형 데이터베이스)

- 2가지 선택

  1. IaaS 형식으로 구성해서 직접 DB설치 운영

     기업 내 DB운영자가 있을 경우 

  2. 서비스(상품)를 이용하는 방법

     기업 내 DB운영자가 없을 경우 



### DB생성하기 

![1619658514025](https://user-images.githubusercontent.com/36434665/116689619-4bdf3b00-a9f3-11eb-858a-62d34e3b7f1e.png)



![1619658918741](https://user-images.githubusercontent.com/36434665/116690091-d9bb2600-a9f3-11eb-8803-92d3590fcd4d.png)

MySQㅣ5.7.x  , 프리티어로 체크 **

**pw : !genieGbox**

![1619659182877](https://user-images.githubusercontent.com/36434665/116689621-4bdf3b00-a9f3-11eb-9bf5-3bd3143750dd.png)

![1619659220307](https://user-images.githubusercontent.com/36434665/116689624-4c77d180-a9f3-11eb-8534-a7b778f96e7c.png)

나머지는 다 기본생성 그대로 



완성

![1619659396950](https://user-images.githubusercontent.com/36434665/116689625-4c77d180-a9f3-11eb-9625-49c8783045a3.png)
![1619661206458](https://user-images.githubusercontent.com/36434665/116689629-4d106800-a9f3-11eb-9f82-8f2a16d9a8bd.png)



## VSCODE 에서 실행 

node.js 도 다운받기

https://aws.amazon.com/ko/sdk-for-node-js/ 

web(ngnix)  was(node.js)  db(mysql) 로 구성 

```
npm init 
npm install aws-sdk
 - aws개발 가능 : node.js 
npm intstall -g express -generator
express -e aaaApp
npm install
```

lab01.js 생성 후 작성 

```javascript
var AWS = require("aws-sdk");
AWS.config.loadFromPath("./awsconfig.json");
var s3 = new AWS.S3();

// 버킷 이름은 모든 S3 사용자에게 고유한 것이어야 합니다.

var myBucket = "my.unique.bucket.name";

var myKey = "AKIA4JWTQKAJGZC6CO7O";

s3.createBucket({ Bucket: myBucket }, function (err, data) {
  if (err) {
    console.log(err);
  } else {
    params = { Bucket: myBucket, Key: myKey, Body: "Hello!" };

    s3.putObject(params, function (err, data) {
      if (err) {
        console.log(err);
      } else {
        console.log("Successfully uploaded data to myBucket/myKey");
      }
    });
  }
});
```

아마존 샘플코드 여기에 있음 

https://github.com/aws-samples

aws-sdk 로 검색해서 보면 샘플 코드가 많다

node.js api문서 확인하기**

lab02.js

```javascript
// Load the SDK and UUID
var AWS = require("aws-sdk");
var uuid = require("node-uuid");

// Create an S3 client
var s3 = new AWS.S3();

// Create a bucket and upload something into it
var bucketName = "node-sdk-sample-" + uuid.v4();
var keyName = "AKIA4JWTQKAJGZC6CO7O";

s3.createBucket({ Bucket: bucketName }, function () {
  var params = { Bucket: bucketName, Key: keyName, Body: "Hello World!" };
  s3.putObject(params, function (err, data) {
    if (err) console.log(err);
    else
      console.log(
        "Successfully uploaded data to " + bucketName + "/" + keyName
      );
  });
});

```

샘플코드로 `node lab01.js` 돌리니 안됨 

왜? 

<u>S3버킷 서비스가 없기때문에</u> (자격증명이 없으면 오류가 난다.)



오류 S3버킷이 없음 , key , DB의 경우 접속권한이 필요하다.

https://github.com/awsdocs/aws-doc-sdk-examples/

```
npm install node-uuid
npm install mysql
```

lab03.js

```javascript
var mysql = require("mysql");
var db_info = {
  host: "ktdslab-je.cxmiowlokdbt.ap-northeast-2.rds.amazonaws.com",
  port: "3306",
  user: "lee",
  password: "!@#genieGbox",
  database: "ktdslab-je",
};
module.exports = {
  init: function () {
    return mysql.createConnection(db_info);
  },
  connect: function (conn) {
    conn.connect(function (err) {
      if (err) console.error("mysql connection error : " + err);
      else console.log("mysql is connected successfully!");
    });
  },
};

```



AWS-DOCS웹사이트 깃헙 

예제코드 확인 

AWS에서 정의한 언어의 예제

Javascript V2/V3 차이점 



awsconfig.json 키파일 작성  > 내 정보를 작성해야한다.

```
{
    "accessKeyId": "AKIA4JWTQKAJGZC6CO7O",
    "secretAccessKey": "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",
    "region": "ap-northeast-2" // 지역정보 확인 
}
```

키 위치를 찾고싶다  ? 

C:\Users\jieun\.aws

![1619675141720](https://user-images.githubusercontent.com/36434665/116689630-4d106800-a9f3-11eb-8366-fb71069116a3.png)



#### 버킷만들기

메뉴 > S3  >  버킷만들기 > 이름 (jepark3b)> 버킷만들기 

![1619675313063](https://user-images.githubusercontent.com/36434665/116689631-4da8fe80-a9f3-11eb-9092-8bd5757749d8.png)

vscode 새로고침하면 생긴다. 

![1619675355951](https://user-images.githubusercontent.com/36434665/116689632-4da8fe80-a9f3-11eb-8f44-5083197a71f7.png)



lab01.js 변경

```javascript
var AWS = require("aws-sdk");
AWS.config.loadFromPath("./awsconfig.json");
var s3 = new AWS.S3();

// 버킷 이름은 모든 S3 사용자에게 고유한 것이어야 합니다.

var myBucket = "jepark3b";
//버킷 생성 후 이름 변경

var myKey = "/mydata/mytest.txt";
//버킷 내 파일이름 설정

s3.createBucket({ Bucket: myBucket }, function (err, data) {
  if (err) {
    console.log(err);
  } else {
    params = { Bucket: myBucket, Key: myKey, Body: "Hello!" };

    s3.putObject(params, function (err, data) {
      if (err) {
        console.log(err);
      } else {
        console.log("Successfully uploaded data to myBucket/myKey");
      }
    });
  }
});
```

![1619675589811](https://user-images.githubusercontent.com/36434665/116689635-4e419500-a9f3-11eb-9f62-fcaf09ee8a74.png)

차단으로 되어있어 js가 실행이 안된다. 

퍼블릭 접근을 하면 보안상 위험함 > 특정 IP만 접근해야한다. 



lab02.js  변경

```javascript
var AWS = require("aws-sdk");
var uuid = require("node-uuid");
AWS.config.loadFromPath("./awsconfig.json");
// Create an S3 client
var s3 = new AWS.S3();

// Create a bucket and upload something into it
var bucketName = "node-sdk-sample-" + uuid.v4();
var keyName = "hello_world.txt";

s3.createBucket({ Bucket: bucketName }, function () {
  var params = { Bucket: bucketName, Key: keyName, Body: "Hello World!" };
  s3.putObject(params, function (err, data) {
    if (err) console.log(err);
    else
      console.log(
        "Successfully uploaded data to " + bucketName + "/" + keyName
      );
  });
});
```

변경 후 

```
npm install node-uuid
node lab02.js 
```

돌리면 잘 돌아간다. 왼쪽 AWS탭에서 새로고침하면 **<u>S3이 생성된다</u>**.

![1619676324961](https://user-images.githubusercontent.com/36434665/116689637-4e419500-a9f3-11eb-9af6-61a27efc67e7.png)

![1619676431804](https://user-images.githubusercontent.com/36434665/116689639-4eda2b80-a9f3-11eb-8a39-3b66d9f2b3d8.png)

`createBucket` 메서드 > 버킷하나를 만들겠다. 

UUID `;Successfully uploaded data to node-sdk-sample-c745109c-b49f-4b9f-a383-cdd829ff3ec5/hello_world.txt` 이걸 생성하기위해 쓴다. 



RDS 데이터베이스 > DB 식별자 > 수정버튼> 

![1619677602709](https://user-images.githubusercontent.com/36434665/116689641-4eda2b80-a9f3-11eb-88b8-dcae3f67f6e4.png)

![1619677638366](https://user-images.githubusercontent.com/36434665/116689643-4f72c200-a9f3-11eb-905a-79bc01a7bace.png)

```
node lab03.js
```

퍼블릭 액세스가능 (예)로 변경 > 보안이 뚫리게 된다. 

workbench나 mysql에서 접근 가능하다.



-----

## python 으로 실행하기

https://aws.amazon.com/ko/sdk-for-python/

```
pip install boto3 
```

실행하다가 오류가 나는 경우가 있는데 

>  관리자 권한이 아니여서 생긴 문제 >> vscode에서 오른쪽 마우스누르고 관리자 권한으로 실행해서 진행하기 





```
juso_jb - pymysql.connect(
    user='id',
    passwd="",
    host= "ktdslab-je.cxmiowlokdbt.ap-northeast-2.rds.amazonaws.com",
    db ='',
    charset="utf8"
)

```

호스트 이름을 접근 권장 
DNS 주소 
IPv4 가 아니라 DNS 기반의 호스트 주소 



-------------------------

Day3

## Pass 이해와 구성을 위한 기술 

개발 >> 디버그 >> 테스트 >> 빌드 >> 배포

[예전]배포 : 물리적 서버

​	web/was

[현재] 배포 : 물리적 서버 > 가상머신(가상서버)

​	web/was



[변해야한다] 배포 : 가상머신 --> 격리수준의 가상환경 

​		컨테이더 >> 도커 

​		Microservice 기반개발 



개발 - OOP(객체지향개발)

클래스/메서드/속성(전역변수)

​		람다(프레임워크 활용)

마이크로서비스 기반 개발 : 클래스/메서드 

​															: 메서드는 10개 미만으로 사용 

컨테이너기반의 도커로 개발한다. > 컨테이너로 묶어서 도커의 이미지를 만든다. 

가상머신개념의 아니라 작은가상화이기때문에 쉽게 바꿔치기한다. 

컨테이버 기반의 도커로 배포 (웹서비스 기반 개발 REST기반 개발 궈;ㄴ장)



개발자들을 작은 단위로 쪼개서 도커에 올려놓고 api로 노출 시키면 ? 프론트엔드 개발자가 api가져와서 ux디자이너와 협업해서 화면을 만들어낸다. 

자동화도구 사용 : DevOps툴 

**DevOps란** ? (중재자) 개발자 < -- > 시스템 엔지니어 



ALM : Application Lifecyle Management

CI/CD

![1619745257559](https://user-images.githubusercontent.com/36434665/116689645-4f72c200-a9f3-11eb-9e0d-632f7f93e503.png)





## 도커와 쿠버네티스의 이해

### 도커 

컨테이너 기반의 오픈소스 가상화 플랫폼 

### 컨테이너 

- 격리된 공간에서 프로세스가 동작하는 기술 
- 가상화 기술의 하나
- 기존방식과 차이
- 프로세스를 격리

가상머신위에 가상화를 올렸다. 

![1619746721953](https://user-images.githubusercontent.com/36434665/116689647-500b5880-a9f3-11eb-956c-2517781c8fae.png)

HCI서버 > 가상머신 전용 VM,Docker 할당 

도커 엔진위에 컨테이너별로 올린다. 



ex> 

App 생성	 > 도커 컨테이너 이미지 > 사용 

>  이미지를 업로드 하는곳은 ?  >>  Docker.com -> 다운로드함 

​					> Public Cloud(Aws.Azure) : 도커 컨테이너 이미지를 업로드 & 다운로드 하면 어떨까? 

> 도커 컨테이너 이미지를 클라우드 저장소 저장에 활용하면 어떨까? 

**Public Cloud**

Aws : S3 저장소 / Azure: Blob저장소 에서 다운받아 놓는다. 

도커 컨테이너 이미지를 **객체**로 본다.

Docker.com에서 가져오는 방법 



### 쿠버네티스

- Kubernetes : 컨테이너화된 애플리케이션을 자동으로 배포, 스케일링(확장), 및 관리하는 오픈소스 시스템 (도커를 잘 관리하는것 / 도커이미지 여러개를 놓고 쓸때 스케일 업을 자동으로 해준다. ) 
- 확장성 , 무한 유연성, 호환성 

#### 실제 실무에서의 쿠버네티스 

- 플랫폼의 자유 
- 운영환경에서의 사용가능 : production ready 

퍼블릭 클라우드에서는 스위칭 할 수 있음 > 상태를 변환시킬수있음 



#### AWS 도커

![1619748428962](https://user-images.githubusercontent.com/36434665/116689649-500b5880-a9f3-11eb-8890-7800c4883612.png)

### AWS에서 쿠버네티스 

![1619748825442](https://user-images.githubusercontent.com/36434665/116689651-50a3ef00-a9f3-11eb-9ab8-fe7c16ec9ce6.png)

응용프로그램을 실행할때 클러스터 단위로 묶어서 실행한다. 

![1619748858555](https://user-images.githubusercontent.com/36434665/116689652-50a3ef00-a9f3-11eb-8a5b-91fdedc06fb4.png)

MySQL도 가상머신에서 설치하고 쓰세요! 라고 한것 

ECR : Container Registry , 컨테이너 배포를 위해 컨테이너 이미지를 저장하는 것 (도커를 안 써도된다)

vscode,atom등 개발해서 형상관리 서버에 올리면 나머지는 aws에서 구축

https://aws.amazon.com/ko/devops/

https://aws.amazon.com/ko/docker/



## AWS 컨테이너 서비스 생성

[Amazon ECS](https://ap-northeast-2.console.aws.amazon.com/ecs/home?region=ap-northeast-2#/firstRun)https://ap-northeast-2.console.aws.amazon.com/ecs/home?region=ap-northeast-2#/firstRun)

컨테이너 커스텀해서 만들 수 있다. 

원하는 작업 개수 1

![1619751577400](https://user-images.githubusercontent.com/36434665/116689655-513c8580-a9f3-11eb-8fed-f3bbd1d360ed.png)
![1619751799808](https://user-images.githubusercontent.com/36434665/116689657-51d51c00-a9f3-11eb-937d-45c0995d0c13.png)





![1619753177104](https://user-images.githubusercontent.com/36434665/116689661-526db280-a9f3-11eb-8e81-ff9f1e9bb64c.png)



![1619757263380](https://user-images.githubusercontent.com/36434665/116689664-53064900-a9f3-11eb-925f-fb0112de0276.png)

대상그룹ID를 누르면 대시보드로 간다. 

![1619757600095](https://user-images.githubusercontent.com/36434665/116689671-54377600-a9f3-11eb-893c-52a2b2accf53.png)

보안그룹 탭ECS에 관련된 보안그룹이 있고

![1619757380539](https://user-images.githubusercontent.com/36434665/116689669-539edf80-a9f3-11eb-8e7c-6856e57b2616.png)

로드밸런서 버튼 누르면 아래 내용이 보임 

![1619757321624](https://user-images.githubusercontent.com/36434665/116689667-53064900-a9f3-11eb-94fc-b16d5258c5f6.png)

DNS 복사해서 붙여넣기 하면 저거를 도커에 올리는것

![1619757362658](https://user-images.githubusercontent.com/36434665/116689668-539edf80-a9f3-11eb-9d91-e097192b1539.png)



기존 개발 및 서비스된 프로그램 > AWS컨테이너 서비스

​	배포 -> 서버 변경

​	배포 - > 도커이미지 

​		이미지 사이즈 큰 용량 가능성 

CI/CD : 소스코드를 분리 (세밀하게 분리한다.)

배포 > 도커이미지 / 소스코드를 분리 

배포 > 도커이미지 

AWS 컨테이너 저장소에 저장하고 배포 > AWS 컨테이너에서 적용하면된다. 



ECR은 500메가까지 사용가능 

![1619757767193](https://user-images.githubusercontent.com/36434665/116689672-54377600-a9f3-11eb-9390-861a3daefbf1.png)



이제 우린 이걸만드는 작업을 한다. 



왼쪽 탭에 레퍼지토리 누르면 이게 나온다.

![1619758427687](https://user-images.githubusercontent.com/36434665/116689676-54d00c80-a9f3-11eb-8e8f-8ae723baa403.png)



레퍼지토리 생성 버튼 

![1619758533340](https://user-images.githubusercontent.com/36434665/116689678-54d00c80-a9f3-11eb-9896-5a4cb1ba1f40.png)

생성

![1619758797449](https://user-images.githubusercontent.com/36434665/116689680-5568a300-a9f3-11eb-954a-9ebebe54b91c.png)

<u>푸시명령 보기</u>를 보면 다양한 명령어가 있음 

- Registries탭은 다양한 퍼미션 복제 등을 할 수 있다. 

ECR이 생성되어있는걸 볼수 있음 

![1619758696122](https://user-images.githubusercontent.com/36434665/116689679-5568a300-a9f3-11eb-9184-33201a85b3d2.png)



## VScode에서 수행

registers 에서 connect누르면 로그인할 수 있음 (도커 홈페이지에서 로그인 후 이메일 confirm받아야한다)

![1619765859880](https://user-images.githubusercontent.com/36434665/116689560-41bd3c80-a9f3-11eb-90b3-aa5737d4806d.png)

도커 로그인 



vscode에서 f1 > >docker add docker files to workspace > docker make파일 만들어야한다. 

![1619759232076](https://user-images.githubusercontent.com/36434665/116689681-56013980-a9f3-11eb-9102-e045a874f582.png)

p;ython을 만들거면 선택 (general)

![1619760794269](https://user-images.githubusercontent.com/36434665/116689683-56013980-a9f3-11eb-87d9-6f910184be6f.png)

.py 선택 

yes 누르면 도커파일 생긴다.

![1619762417779](https://user-images.githubusercontent.com/36434665/116690788-dd02e180-a9f4-11eb-92c7-e95e94009b73.png)



도커 메이커 만들고 도커 만든 후 이 명령어 대로 실행야한다. 

powershell명령어 

```
Install-Module -Name AWS.Tools.Installer
//aws인스톨 툴 
Install-Module -Name AWSPowerShell
//파워쉘 명령어
Set-ExecutionPolicy RemoteSigned
//aws 파워쉘 둘다깔면 이슈생길 수 있어서 실행정책을 수정해야한다. 
```



```
(Get-ECRLoginCommand).Password | docker login --username AWS --password-stdin 845478383634.dkr.ecr.ap-northeast-2.amazonaws.com
?? 이건 powershell용 이거안씀 아래꺼씀 

// aws도구를 사용해야한다. 해당되는 명령어를 사용해야한다. 
aws configure 액세스키 비번 입력 하고 접속 
aws ecr get-login-password --region ap-northeast-2 | docker login --username AWS --password-stdin 845478383634.dkr.ecr.ap-northeast-2.amazonaws.com

docker build -t ktdslab-jepark .

docker tag ktdslab-jepark:latest 845478383634.dkr.ecr.ap-northeast-2.amazonaws.com/ktdslab-jepark:latest

docker push 845478383634.dkr.ecr.ap-northeast-2.amazonaws.com/ktdslab-jepark:latest
```

도커 만든 후 이 명령어 대로 실행야한다. 

첨에 로그인 

![1619766050679](https://user-images.githubusercontent.com/36434665/116689564-42ee6980-a9f3-11eb-99dd-4ea7847d230d.png)

이미지 올리기 > 성공 

![1619766019311](https://user-images.githubusercontent.com/36434665/116689561-4255d300-a9f3-11eb-8115-470a04669afd.png)

![1619766101024](https://user-images.githubusercontent.com/36434665/116689565-42ee6980-a9f3-11eb-93db-7e6c1ea303fc.png)

요래 생김 

이렇게 수정할때마다 이미지를 빌드> 배포 하면됨 

![1619766352079](https://user-images.githubusercontent.com/36434665/116689566-43870000-a9f3-11eb-822d-3a0a9e432561.png)

요기에두 생김 

### 서버리스

#### microservice

서버를 사용하지 않는다.

가벼운 가상화: Docker / lamda 

> microservie 기반 개발의 핵심 

![1619765194763](https://user-images.githubusercontent.com/36434665/116689556-4124a600-a9f3-11eb-8582-5125104a1bae.png)



**MVC** 

model :  DB연결처리 (data처리)

conrtol : 중계 m v 중계

> 서버리스는 이 model control을 잘게 쪼게서 api로 만든것 

view : 화면처리 



**주요 이점** : 제품 출기 기간 단축 ,확장성 , 복구능력,  쉬은 배포, 편리한 액세스, 개발성(다중지원)



#### Mircro service 정의와 이해

![1619765491699](https://user-images.githubusercontent.com/36434665/116689558-41bd3c80-a9f3-11eb-8505-46db408dfcf3.png)

요즘엔 nginx를 많이 사용한다. 

![1619765550813](https://user-images.githubusercontent.com/36434665/116689559-41bd3c80-a9f3-11eb-83b0-fc8af216677d.png)

node.js를 조금씩 쪼개서 분할해서 개발 

### 서버리스 lamda만들기 

서버리스 lamda만들때 

CLI application만들었음 

AWS SAM CLI설치해서 >  lamda sam application 생성 

1. 설치 

https://docs.aws.amazon.com/ko_kr/serverless-application-model/latest/developerguide/serverless-sam-cli-install-windows.html

2. vs에서 어플리케이션 만들기 

![1619767327302](https://user-images.githubusercontent.com/36434665/116689568-43870000-a9f3-11eb-8f7e-8e398a8c80ba.png)

![1619767430478](https://user-images.githubusercontent.com/36434665/116689570-441f9680-a9f3-11eb-9e8f-a3c401ebab69.png)

hello world 어쩌구 생성됨 

![1619767525711](https://user-images.githubusercontent.com/36434665/116689571-441f9680-a9f3-11eb-9bcc-8be725338d78.png)

배포 

![1619767574144](https://user-images.githubusercontent.com/36434665/116689572-44b82d00-a9f3-11eb-85d4-26dd71614413.png)

deploy application 

![1619767590193](https://user-images.githubusercontent.com/36434665/116689574-44b82d00-a9f3-11eb-8439-c136f78ea062.png)

서울 지역선택 

![1619767601896](https://user-images.githubusercontent.com/36434665/116689575-4550c380-a9f3-11eb-8395-43486458c479.png)

네이밍 만들고 

순서대로 선택 

![1619767661904](https://user-images.githubusercontent.com/36434665/116689576-4550c380-a9f3-11eb-88bc-9449aeb06eac.png)

뭔가 계속 푸시되는 중 

![1619767720729](https://user-images.githubusercontent.com/36434665/116689578-45e95a00-a9f3-11eb-9c61-d853d12ae2d9.png)

성공

![1619767780817](https://user-images.githubusercontent.com/36434665/116689583-4681f080-a9f3-11eb-956a-03a252c79627.png)

뭔가 만들어짐 

![1619767752157](https://user-images.githubusercontent.com/36434665/116689580-45e95a00-a9f3-11eb-8556-5008a08ca6c2.png)

S3 스토리지 , DCR 내용 

![1619767818649](https://user-images.githubusercontent.com/36434665/116689585-4681f080-a9f3-11eb-8037-db9840665dc0.png)

요기에 이미지 올라옴 



