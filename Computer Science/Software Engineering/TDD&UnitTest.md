// 2022.09.19 Rookie

### **TDD(Test Driven Development) : 테스트 주도 개발**

테스트 주도 개발은 말 그대로 개발을 하는데에 있어서 테스트가 주가 된다는 하나의 개발 방법론이다. 먼저 테스트를 하면서 코드를 작성하고 그 후에 본 코드를 구현하는 방식이다. 테스트를 거친 후에 코드를 작성한다면 추후에 신경 써줘야할 많은 부분들에 대해서 해결을 하면서 코드를 작성할 수 있겠다

<img width="744" alt="image" src="https://user-images.githubusercontent.com/103009135/190972184-db8678f1-d6a1-4f4e-871d-12e823f2aaec.png">


문서를 잘 작성하는 방법은 검토와 고쳐쓰기라고 생각한다
 어떤 책에서 개발자는 “컴퓨터가 잘 알아듣는 문서를 작성하는 사람” 이라는 문구를 본적이 있다. 그리고 개인적으로 저는 여기에 아주 동감…

따라서 좋은 코드를 만들기위해 반복적으로 코드를 검사하고 다시 고치는 방식으로 소프트웨어를 개발하는 방법을 고안해낸 것을 **TDD 라고 한다!** 

 앱을 몇번 개발해보면 나중에 이거는 어떻게 고쳐야하나… 처음부터 잘 짤걸하는 깨달음을 얻은 적이 있으실 텐데요… 그런것들을 방지할 수 있는 방법론입니다.

### 장점

1. 작업과 동시에 테스트를 진행하면서 실시간으로 오류 파악이 가능함 ( 시스템 결함 방지 )

2. 짧은 개발 주기를 통해 고객의 요구사항 빠르게 수용 가능. 피드백이 가능하고 진행 상황 파악이 쉬움

3. 자동화 도구를 이용한 TDD 테스트케이스를 단위 테스트로 사용이 가능함

(자바는 JUnit, C와 C++은 CppUnit 등)

개발자가 기대하는 앱의 동작에 관한 문서를 테스트가 제공해줌 <br>
또한 이 테스트 케이스는 코드와 함께 업데이트 되므로 문서 작성과 거리가 먼 개발자에게 매우 좋다고 한다!

### 단점

1. 기존 개발 프로세스에 테스트케이스 설계가 추가되므로 생산 비용 증가

2. 테스트의 방향성, 프로젝트 성격에 따른 테스트 프레임워크 선택 등 추가로 고려할 부분의 증가



#### 아니 근데,,, 상식적으로 테스트를 할려면 뭘 만들어야 테스트 할 수 있는 거아님?? 작업과 테스트를 동시에 진행한다는게 무슨 말일까?? 그래서 제가 한번 찾아봤습니다.. 

#### xCode는 UnitTest라는 기능을 사용해서 TDD를 주도할 수 있습니다.

#### 다음 예시를 따라가보면서 어떤식으로 TDD를 한다는건지 알아봅시다


## TDD 실습
#### Xcode 프로젝트 생성시 Include Tests를 사용해서 TDD를 진행할 수 있다. 
<img width="500" alt="image" src="https://user-images.githubusercontent.com/103009135/190954516-bea744a7-169a-4fbb-bf41-98d1e2d62f07.png">

### 혹은 
#### 하단 툴바에서 + 버튼을 눌러 UnitTest 번들을 추가할 수 있다.
<img width="500" alt="image" src="https://user-images.githubusercontent.com/103009135/190954953-dcd933e3-0553-4417-b83b-3c7bd23cf57b.png">

## Objective
10진수를 넣으면 소수점 뒷 자리까지 잘 표기해주는 텍스트 포매팅 함수 기능을 TDD 방식으로 개발해보자

## Test Setting
<img width="800" alt="image" src="https://user-images.githubusercontent.com/103009135/190955296-84f7de3c-7083-4b9c-9966-d8377b47a7f6.png">

swift 파일안에는 test를 위한 클래스와 메소드들이 내장되어있는데, 빌드를 하면 다음과 같은 함수의 실행여부를 체크해준다. 그리고 저 체크박스를 클릭하면, 개별적인 함수의 수행여부도 테스트할 수 있음

## Customize
#### Test 케이스를 커스텀하기 위해서는 일단 UnitTest Class 파일을 만들어여한다.
<img width="600" alt="image" src="https://user-images.githubusercontent.com/103009135/190955552-327f9c65-f77d-4d49-8bd1-d7a79cfd6409.png">

## 
#### 테스트 할 앱과 테스트 코드는 별개의 파일이므로 테스트 할 앱을 구성하는 코드를 다음 방법으로 가져와야한다.
1. 테스트할 모듈을 import
2. @testable 키워드 붙이기 
<img width="600" alt="image" src="https://user-images.githubusercontent.com/103009135/190957188-f07f6bd1-ea63-4f6b-b3d4-18d9ec4697d6.png">

#### 그리고 XCTest 클래스 안에는 테스트를 위한 여러 메소드들이 내장되어있다. 조건을 입력하고 T/F 에 따라 결과를 반환하는 것과, 두 개의 함수 반환값을 비교해서 성공/실패를 나눌 수 있는 함수등... 
<img width="600" alt="image" src="https://user-images.githubusercontent.com/103009135/190957301-a2a488e8-3bb8-4975-925f-5bd5fd8df6c5.png">

## Test Code

#### 다음과 같이 decimal 타입을 문자열로 반환해주는 함수가 있다. 이 함수의 결과값을 예시로 다음과 같이 비교해서 테스트를 해볼 수 있다
<img width="500" alt="image" src="https://user-images.githubusercontent.com/103009135/190957488-86891424-1a4e-43f7-ad9f-01c99d03a7c0.png">


<img width="500" alt="image" src="https://user-images.githubusercontent.com/103009135/190957533-c9fc5f8b-b65e-4c9d-9626-a911ae2619df.png">

#### 제가 생각하기에 TDD 방식은 퀴즈 같다고 생각해요
내가 이 테스트를 통과하도록 코드를 짜고 싶으면 어떻게 해야하지? 를 먼저 설정해놓고 그에 맞게 돌아가서 코드를 고치는 것입니다.
예를 들어서 위의 테스트를 통과하려면 stirng 함수의 반환값을 "0.00"에 맞춰야합니다. 그럼 MoneyFormatter 파일에 들어가서 그 부분만 고치는 방식입니다. 상당히 목적지향?적이고 

<img width="500" alt="image" src="https://user-images.githubusercontent.com/103009135/190958993-9e3a39c9-a5e2-46a6-a46e-477c83f19f54.png">

### 

다음과 같이 여러 케이스에 대해서 테스트를 진행해서 에러없는 기능을 개발할 수 있습니다. 
<img width="600" alt="image" src="https://user-images.githubusercontent.com/103009135/190960261-b0538b71-417a-4441-8fa0-c951371011c8.png">

### 예시
이렇게 개발했는데 테스트에서는 전부 오류다. 엥 뭐가 문제지? 
<img width="600" alt="image" src="https://user-images.githubusercontent.com/103009135/190960316-fa7a2568-ec90-4a80-a2db-d67d4049779f.png">

#### 함수에서 반환하는 스트링에 빈 문자열이 껴있는 실수를 발견할 수 있었다.

### 고치고 다시해보면.... 
<img width="600" alt="image" src="https://user-images.githubusercontent.com/103009135/190960433-7fc4d3af-b0a2-4268-8c22-a96e05ac40ad.png">

### 잘 빌드되는 모습을 볼 수 있다 
<img width="600" alt="image" src="https://user-images.githubusercontent.com/103009135/190961641-eb93ce59-85a4-4b9a-ac69-188fb50e3c7b.png">

## 테스트 추가, 기능 추가
#### 자 이제 1.1은 1.10이 되도록 변환하는 테스트를 만들어놓고 (목적설정) 그에 맞게 기존 함수를 수정해보자
<img width="600" alt="image" src="https://user-images.githubusercontent.com/103009135/190961720-7f87c712-eb62-4cd3-89e4-8e46cb6b8eb6.png">
### 
<img width="600" alt="image" src="https://user-images.githubusercontent.com/103009135/190961903-8a54ea79-15d2-46a9-8969-0aaf656bfed3.png">
이렇게 끝자리수 조정을 해주면 끝!

## 응용
 내가 만든 계산기에 Unit Test를 시도해봤다. 
###  
<img width="700" alt="image" src="https://user-images.githubusercontent.com/103009135/190970595-72ca1b9c-9093-4608-a8ea-c254fbec0a01.png">

#### 0으로 나눈 값에서는 에러를, 곱셉 연산 예시애서는 통과를 나타내는 것을 볼 수 있다.

## Summary
#### TDD는 개발자가 특정 기능을 구현하는 단계에서 초기부터 에러나 예외사항 없이 꼼꼼한 개발을 도와준다.
#### 꼼꼼한 만큼 정확하겠지만 위에 보는 바와같이 시간이 많이 걸릴 수 밖에 없다 

## Reference
https://www.youtube.com/watch?v=B4yJ85IaTUw&t=836s 
https://github.com/Rookie0031/Swift-Questions/issues/27 
