//2022.08.28 Noel

<br/>
<br/>
<br/>


# ❤️OSI 7계층

<br/>

## 🧡 OSI 7계층이란?

> OSI (Open Systems Interconnection Reference Model)

- OSI 7계층은 네트워크에서 통신이 일어나는 과정을 **7단계**로 나눈 것
- 다양한 컴퓨터 시스템이 **표준 프로토콜**을 사용하여 통신 할 수 있도록 국제 표준화 기구(ISO)에서 만든 개념 모델
- OSI 표준 모형은 7계층으로 이루어져 있음, 계층별로 **역할을 분리**해서 각 계층이 **독립적**으로 기능을 수행하고 계층간의 **통신**을 통해 전체 통신 프로세스를 가능하게 함

**OSI 7단계로 정의한 이유**

- 통신이 일어나는 과정을 단계별로 파악하기 위함
- 통신 과정 중에 **특정한 곳에 이상**이 생길 경우 다른 단계의 장비 및 소프트웨어 등을 건드리지 않고 **통신 장애를 일으킨 단계에서 해결** 할 수 있기 때문

```예시

 <문제상황>
 PC방에서 오버워치를 하는데 연결이 끊겼다.
 어디에 문제가 있는지 확인하기 위해서는

 
 ① 모든 PC가 문제가 있다면
 라우터의 문제(3계층 네트워크 계층)이거나 
 광랜을 제공하는 회사의 회선 문제(1계층 물리 계층)


 ② 한 PC만 문제가 있고  
 오버워치 소프트웨어에 문제가 있다면(7계층 어플리케이션 계층)
 오버워치 소프트웨어에 문제가 없고, 스위치에 문제가 있으면(2계층 데이터링크 계층)
 
 이렇게 판단해 다른 계층에 있는 장비나 소프트웨어를 건들이지 않을 수 있음
```



- 아래 그림처럼 **1계층(물리계층) ~ 7계층(응용 계층)**으로 구성
- 각 계층을 지날 때마다 각 계층에서 **Header가 붙게되고, 수신측은 역순으로 헤더를 분석**

<img width="793" alt="image" src="https://user-images.githubusercontent.com/103012104/187397696-17790af9-601c-4b39-a998-7e8794a0bdda.png">

<br/>
<br/>

## 🧡 OSI 7계층 구조

<img width="730" alt="image" src="https://user-images.githubusercontent.com/103012104/187397828-0312a5ce-8158-4814-9e4f-2700d2ebd32d.png">

#### TCP/IP 모델

<img width="817" alt="image" src="https://user-images.githubusercontent.com/103012104/187397903-baa5a9a1-4935-43a7-b2ad-ffd884860126.png">

- 참고!! 현대의 인터넷은 OSI 모델이 아닌 `TCP/IP` 모델을 따르고 있음!!!!
- TCP/IP 모델
  - 5,6,7 layer이 Application Layer로 합쳐져있음
  - 3계층 Network Layer -> Internet Layer로 이름 바뀌어있음 

``` 요약
1. 물리 계층
- 데이터를 전기적인 신호로 변환해 주고 받는 기능을 진행하는 공간

2. 데이터 링크
- 물리계층으로 송/수신되는 정보를 확인하고 오류없는 통신을 위해 여러 역할을 수행
- Mac 주소를 통해 통신

3. 네트워크
- 데이터를 목적지 까지 가장 안전하고 빠르게 전달하는 기능
- 라우터를 통해 경로를 선택 해 IP 주소를 지정하고 경로에 따라 패킷을 전달

4. 전송
- 두 호스트 시스템에서 발생하는 데이터의 흐름을 제공

5. 세션
- 통신 시스템 사용자간의 연결을 유지 및 설정

6. 표현
- 세션 계층 간의 주고받은 인터페이스를 일관성 있게 제공

7. 응용
- 사용자가 네트워크에 접근할 수 있도록 서비스를 제공
```

```요약
🤩이해를 위한 예시!!!

EX) 미국에 있는 친구에게 편지를 보낸다.
	🖤 응용(Layer7) : 편지를 씀
	💜 표현(Layer6) : 한글로 작성한 편지를 미국 친구가 알아볼 수 있게 변역
	💙 세션(Layer5) : 미국 친구의 집주소를 기입
	💚 전송(Layer4) : 우체국에 편지를 접수시키기 위한 절차, 즉 배 또는 비행기 등의 운송수단 결정
	💛 네트워크(Layer3) : 우체국에 있는 여러 편지들을 같은 목적지로 분류
	🧡 데이터 링크(Layer2) : 해당되는 목적지, 운송방법에 따라 분류,
												직접연결이 되지않는 경우 중간 경유지를 선택하여 분류하는 작업
	❤️물리계층(Layer1) : 실제적으로 편지가 배, 비행기 등의 운송수단에 의해 운송되는것을 의미
	
	

EX) 이메일 전송을 한다.
	🖤 응용(Layer7) : 이메일 프로그램을 통해 이메일을 작성
	💜 표현(Layer6) : 공통된 표현 형식으로 데이터를 변환하거나 암호화, 압축울 수행
	💙 세션(Layer5) : 데이터의 동기화를 위해 일정한 길이마다 sync를 삽입하여 전송 계층으로 데이터를 전달
	💚 전송(Layer4) : 발신지와 목적지의 주소를 지정하고, 연결방식, 흐름제어, 오류제어를 함 그리고 데이터를 전송할 수 있는 세그먼트 단위로 나눔
	💛 네트워크(Layer3) : 발신지와 목적지의 주소가 아닌 라우티에 필요한 논리주소를 설정하고, 패킷에 대한 라우팅 정보를 삽입
	🧡 데이터 링크(Layer2) : 프레임 단위로 데이터를 나눈 후 Mac 주소를 지정하고, 양 끝단의 속도 차이에 대해 원할하게 해주기 위한 흐름제어를 함 또한 데이터의 오류를 막기위해 데이터 오류검사를 위한 설정을 함
	❤️물리계층(Layer1) : 전송 매체가 일반 케이블인지, 광케이블인지 등을 설정. 그리고 전송방식을 데이터의 회선으로 보내기 위한 전기적인 변환을 담당
	

```

<br/>

<br/>

<hr/>

### 💚 1계층 물리 계층 (Physical Layer) <br/>

> **두 대의 컴퓨터가 통신하려면?**
>
> 모든 파일과 프로그램은 0과 1의 나열, 따라서 0과 1을 주고 받을 수 있으면 됨

- **데이터를 전기적인 신호로 변환해서 주고받는 기능을 진행하는 계층**

- 인터넷 케이블. 라우터 스위치 등의 전기적 신호가 **물리적인 장치에 의해 왔다 갔다(통신)** 하는 계층

- 단지 데이터를 전달만 함 

  - 전송하려는 또는 받으려는 데이터가 무엇이고 어떤 에러가 있는지 전혀 신경 쓰지 않음<br/>

- 데이터 단위 및 대표 장치

  - 통신 단위 : 0과 1의 비트열, 즉 On, Off  전기적 신호 상태로 구성<br/>

  - 대표적 장비 : 통신 케이블, 리피터, 허브 등<br/>

    <img width="657" alt="image" src="https://user-images.githubusercontent.com/103012104/187398015-12150ba2-4206-46f5-b373-1b8c75396b20.png">

```요약
🤓 1계층 물리 계층 요약
👉encoding과 decoding 과정을 통해 
물리적으로 연결된 두 대의 컴퓨터가 0,1의 나열을 주고 받을 수 있게 해주는 모듈

*encoding : 송신측에서 0과 1의 나열을 전기적 신호(아날로그 신호)로 바꾸어 전선으로 흘려보냄
*decoding : 수신측에서 encoding 전기적 신호가 들어오면 0과 1의 나열로 해석함

👉 1계층 모듈은 하드웨어적으로 구현되어 있음

👉 1계층으로는 여러 대의 컴퓨터가 통신 할 수 없음 (모든 컴을 전선으로 연결할 수 없기 때문,,)
```



<br/>

<br/>

<hr/>

**✋ 2계층에 들어가기 전 잠깐!**

```참고
🧐 여러 대의 컴퓨터가 통신하려면?
컴퓨터가 통신하려면 전선으로 연결 되어있어야함...
그렇다고 통신하려는 컴퓨터끼리 모두 연결하기에는 비용이 많이들고 비효율적임
따라서! 전선 하나를 가지고 여러대의 컴퓨터와 통신할 방법을 모색..

⁉️ 그래서 전선 하나에 여러 대(A,B,C,D)의 컴퓨터를 연결시킨다면..?
-> 서로 통신은 되지만.. 내가 원하는 컴에만 데이터를 보낼 수 없음🥲
(해당 전선과 연결된 모든 컴퓨터(A,B,C,D 모두)에 데이터가 가게 됨)

이때!!!! A가 B에게 데이터를 보내고 싶을 때!
목적지로 출발한 데이터를 중간에 적합한 경로로 스위칭 해주는 역할이 '스위치'임
하나의 스위치로 연결된 컴퓨터들을 하나의 '네트워크'라고함 (=인트라넷)
스위치는 데이터링크 계층에 속해있으므로 MAC주소 기반으로 동작!!

⁉️ 근데 만약 A와 B가 다른 네트워크에 존재한다면..? (서로 다른 스위치에 연결되있다면?)
그럼 통신을 위해 스위치끼리 연결해줘야하는데 (전선으로 연결되어 있지않다면.. 컴퓨터는 통신할 수 없음)

이때!!! 스위치끼리 연결해주는, 즉 서로 다른 네트워크에 속한 컴퓨터끼리 
통신이 가능하게 해주는 장비를 '라우터'라고 함!!
이런식으로 전 세계 네트워크들을 연결한 것을 '인터넷'이라고 함!
(실제로 해저케이블이 바다에 깔려있어서 전세계 컴퓨터들이 통신이 가능한것..)
```



### 💚 2계층 데이터 링크 계층 (Data Link Layer) <br/>

- **물리계층으로 송수신되는 정보의 오류와 흐름을 관리하여 안전한 정보의 전달을 수행**할 수 있도록 도와주는 역할<br/>
  - **두 장치 간의 신뢰성 있는 전송을 보장**하기 위한 계층<br/>
  
  - 통신에서의 오류도 찾기 및 재전송하는 기능을 가지고 있어 이 계층에서는 **맥 주소(Mac Address)**를 가지고 통신
  
  - **프레임(Frame)에 Mac주소를 부여하고 에러 검출, 재전송, 흐름 제어를 진행**
  
    ```예시
    ⁉️ 만약 같은 네트워트의 B, C, D 컴퓨터가 동시에 A에게 각각 데이터를 전달하면
    
    B: 10010 / C : 101101 / D :110110 -> A가 받는 데이터 : 10010101101110110
    -> A에게 B,C,D의 데이터는 구분없이 붙여서 들어오게 됨 
    
    이떄, 어디서 끊어 읽냐에 따라 올바른 데이터가 들어올지, 엉뚱한 데이터가 들어올지가 달라짐
    그래서 데이터의 구분을 위해 데이터의 시작과 앞에 임의의 값을 붙이는데 (예시 : 시작 1000 / 끝: 1111)
    이것을 바로 Framing이라고함! 데이터를 어디서 끊어 읽어야할지 구분자가 되어줌
    ```
  
- 데이터 단위 및 대표 장치<br/>
  -  전송되는 단위 : 프레임(Frame)<br/>
  - 대표적 장비 : 브리지, 스위치 등
    - 브리지나 스위치를 통해 Mac 주소를 가지고 물리계층에서 받은 정보 전달<br/>
  
- 하드웨어와 소프트웨어 특성을 둘 다 가짐
  - 물리계층은 하드웨어적 틍성을 가지고, 네트워크 계층부터는 소프트웨어적 특성을 가짐

```요약
🤓 2계층 데이터 링크 계층 요약
👉 같은 네트워크에 있는 여러 대의 컴퓨터들이 데이터를 주고받기 위해서 필요한 모둘
👉 Framing은 데이터링크 계층에 속하는 작업들 중 하나

👉2계층 + 1계층
👩‍💻송신자 
		-2계층에서 보내려는 데이터를 앞뒤에 구분자를 넣어 프레임화해서 1계층으로 보냄
		-1계층에서 프래임화한 데이터를 전기적 신호로 수신자에게 보냄
🧑‍💻 수신자
	- 1계층에서 전기적 신호를 받아서 데이터 해석
	- 2계층에서 프레임을 떼어 내고 원본 데이터만 받음
```

``` 참고
💡이해를 위한 용어 설명

① 맥 주소(Mac Address)
- 컴퓨터 간 데이터를 전송하기 위해 있는 컴퓨터의 물리적 주소, 하드웨어 주소
- 그 기계의 고유 번호, 그 하드웨어만 가지고 있는 식별번호(=주민번호)
- 맥주소는 12자리 문자열, 48비트로 표현되고 보통은 16진수로 표현 (ex : 02-46-8A-CE-00-FF)
- IP 주소 = 네트워크 주소 / Mac 주소 = 하드웨어 주소, 물리적 주소, 이더넷 주소
- Mac 주소 = 데이터 링크 계층에 사용 / IP 주소 = 네트워크 계층에서 사용

🤔 보통 네트워크 통신을 할때 IP 주소를 사용하는데 왜 Mac 주소가 필요한가?
- 네트워크 통신은 IP 주소만으로 통신하는것처럼 보이지만 실제로 마지막에 Mac 주소가 필요
- 이는 OSI 7 Layer이라는 통신 표준에 설계된대로 통신이 되기 때문!
- Mac 주소는 레이러 2 테이터 링크에서 사용되는데, 이떄 IP주소에서 Mac 주소로 변환하는 과정을 거침
- 그 과정을 ARP(Address Resolution Protocol)이라고 부름

② 주소 할당
- 물리 계층으로 받은 신호들이 네트워크 상의 장치에 올바르게 안착할 수 있게 함

③ 오류 감지
- 신호가 전달되는 동안 오류가 포함되는지 감지 오류가 있다면 해당 데이터를 폐기
```

<br/>

<br/>

<hr/>

### 💚 3계층 네트워크 계층 (Network Layer) <br/>

- 이 계층에서 가장 중요한 기능은 **데이터를 목적지까지 가장 빠르게 전달하는 기능(라우팅) 담당**<br/>
  - **라우터를 통해 이동할 경로를 선택해 IP 주소를 지정하고, 경로에 따라 패킷을 전달**해줌
    
    - 패킷을 네트워크 간의 IP를 통하여 데이터를 전달
    
  - **여러개의 노드를 거칠때마다 경로를 찾아주는 역할**을 하는 계층<br/>
  
  - 다양한 길이의 데이터를 네트워크를 통해 전달하고, 그 과정에서 전송계층이 요구하는 서비스 품질(QoS)을 제공하기 위한 기능적, 절차적인 수단을 제공<br/>
  
    ```참고
    네트워크 계층 간단한 예시!
    
    인터넷에서 내가 원하는 컴한테 데이터를 보내고 싶으면 데이터 앞에 받는 컴의 IP 주소를 써야함
    -> A가 B에게 데이터를 보낼 때, B의 IP 주소를 붙여서 보냄 (예 : 55.10.54.75 data)
    -> 상대방의 IP 주소를 알고 있어야 데이터를 보낼 수 있음 
    
    이때 [55.10.54.75 data]를 패킷이라고 한다면,
    패킷은 여러 라우터들을 통해 B가 있는 네트워크로 가게됨
    이때 데이터(패킷)을 목적지에 배송해주는 단계가 네트워크 계층!
    ```
  
    
  
- 네트워크 계층은 **라우팅, 흐름제어, 세그멘테이션(segmentation), 오류제어, 인터네트워킹 등을 수행**
  - 데이터를 연결하는 다른 네트워크를 통해 전달함으로써 인터넷이 가능하게 만드는 계층<br/>
  - 컴퓨터에게 데이터를 전송할 주소를 갖고 있어 통신 가능 (=IP주소가 네트워크 계층 헤더에 속함)<br/>
  - 논리적인 주소 구조(IP), 곧 네트워크 관리자가 직접 주소를 할당하는 구조를 가지며, 계층적(Hierarchical)이다.<br/>
  
- 데이터 단위 및 대표 장치<br/>
  - 데이터 단위 : 패킷(Packet)<br/>
  - 대표적 장치 : 라우터, 라우팅 기능을 장착한 L3 스위치(여기서 IP 주소 사용)<br/>

<img width="748" alt="image" src="https://user-images.githubusercontent.com/103012104/187398091-ae7ad9d5-53a4-4e6d-8dca-ecb984cc6b9b.png">

``` 요약
🤓 3계층 네트워크 계층 요약
👉 수 많은 네트워크들의 연결로 이루어진 inter-network 속에서
	어딘가에 있는 목적지 컴퓨터로 데이터를 전송하기 위해, IP 주소를 이용해 길을 찾고(roting)
	자신 다음의 라우터에게 데이터를 넘겨줘 빠르게 전달하는 기능
```



```참고
💡이해를 위한 용어 설명

① 라우팅(Routing)
- 라우팅은 어떤 네트워크 안에서 통신 데이터를 보낼 때, 최적의 경로를 선택하는 과정
- 최적의 경로는 주어진 데이터를 가장 짧은 거리 또는 가장 적은 시간 안에 전송할 수 있는 경로
- 라우터란 
		> 라우팅을 능동적으로 수행하는 장치
		> 패킷의 위치를 추출하여 그 위치에 대한 최적의 경로를 지정하며, 이 경로에 따라 데이터 패킷을 다음 장치로 전향시키는 장치

② 서비스품질(QoS /Quality of Service)
- QoS는 네트워크 디바이스가 트래픽을 구별한 후에 트래픽에 서로 다른 동작을 적용할 수 있도록 해줌
- 트래픽을 생성하는 애플리케이션의 필수 동작에 맞게 라우터나 스위치 같은 네트워크 디바이스가 해당 트래픽을 전달할 수 있도록 트래픽을 조작하는것


③ 패킷(Packet)
- pack + bucket의 합성어
- 정보를 보낼 때 특정 형태를 맞춰 보낸다는 것, 컴퓨터 간에 데이터를 주고받을 때 네트워크를 통해서 전송되는 데이터 조각
```

<br/>

<br/>

<hr/>

### 💚 4계층 전송 계층 (Transport Layer) <br/>

- **송신자와 수신자를 연결하는 통신 서비스를 제공하고 IP에 의해 전달된 데이터(패킷)의 오류를 검사하며 재선송 요구 제어등을 담당**<br/>
  
  - 데이터의 전달을 담당<br/>
  - **TCP와 UDP 프로토콜을 통해 통신을 활성화**하며, Port를 열어 응용프로그램들이 전송을 할 수 있게함<br/>
    - TCP : 정확성, 신뢰형, 연결지향적<br/>
    - UCP : 신속성, 비신뢰선, 비연결성, 실시간<br/>
  - 데이터가 온 경우, **4단계에서 해당 데이터를 하나로 통합해 5계층으로 전달**<br/>
  - 양 끝단(End to end)의 사용자가 **신뢰성 있는 데이터를 주고받게 하여 상위 계층이 데이터 전달의 유효성이나 효율성을 신경쓰지 않게 해주는 계층<br/>**
  
  ``` 요약
  전송 계층 간단한 예시!
  
  3계층까지 거치면서 인터넷상의 모든 컴퓨터가 서로 통신할 수 있게됨
  -> 데이터를 받는 수신자는 전 세계의 컴퓨터로부터 데이터를 받을 수 있게됨
  
  컴퓨터는 받은 데이터를 실행 중인 프로그램(프로세스)에 전달해주려고함
  근데 이때!? 어떤 데이터를 어떤 프로그램에 보내야할지 어떻게 알 수 있을까?
  
  먼저! 데이터를 받고자하는 프로세스들은 포트번호(Port Number)을 거처야함
  포트 번호 : 하나의 컴퓨터에서 동시에 실행되고 있는 프로세스들이 서로 겹치지않게 가져야하는 정수 값
  
  만약 카카오톡이 8081이라는 포트번호를 가질때
  송신자는 데이터를 보낼때 데이터를 받은 수신자 컴퓨터에 있는 프로세스의 포트 번호를 붙여서 데이터를 보내야함
  [port : 8081 ~data~]
  ```
  
  
  
- 시퀀스 넘버 기반의 오류제어 방식을 사용<br/>

- 전송 계층은 특정 연결의 유효성을 제어하고, 일부 프로토콜은 상태개념(Stateful)이 있고, 연결기반(Connection Oriented)<br/>
  - => **전송 계층이 패킷의 전송이 유효한지 확인하고 전송 실패한 패킷들은 다시 전송한다는 것**을 뜻함<br/>
  
- 데이터 단위<br/>
  - 데이터 전송을 위해서 Port 번호를 사용함.(대표적인 프로토콜로 TCP와 UDP가 있음)<br/>
  - 데이터 단위 : 세그먼트(Segment)<br/>

``` 요약
🤓 3계층 네트워크 계층 요약
- port 번호를 사용하여 도착지 컴퓨터의 최종 도착지인 프로세스에 까지 데이터가 도달하게 하는 모듈

3계층까지 거치면서 인터넷상의 모든 컴퓨터가 서로 통신할 수 있게됨
-> 데이터를 받는 수신자는 전 세계의 컴퓨터로부터 데이터를 받을 수 있게됨

컴퓨터는 받은 데이터를 실행 중인 프로그램(프로세스)에 전달해주려고함
근데 이때!? 어떤 데이터를 어떤 프로그램에 보내야할지 어떻게 알 수 있을까?

먼저! 데이터를 받고자하는 프로세스들은 포트번호(Port Number)을 거처야함
포트 번호 : 하나의 컴퓨터에서 동시에 실행되고 있는 프로세스들이 서로 겹치지않게 가져야하는 정수 값

만약 카카오톡이 8081이라는 포트번호를 가질때
송신자는 데이터를 보낼때 데이터를 받은 수신자 컴퓨터에 있는 프로세스의 포트 번호를 붙여서 데이터를 보내야함
[port : 8081 ~data~]
```

``` 참고
💡이해를 위한 용어 설명

① TCP (Transmission Control Protocol)
- 데이터를 중요하게 생각할 때 TCP 프로토콜 사용
- 신뢰할 수 있고 정확한 데이터를 전달하기 위해 연결형 통신을 사용하는 프로토콜
- TCP는 통신할 컴퓨터끼리 ‘보냈습니다’, ‘도착했습니다’라고 서로 확인 메시지를 보내면서 데이터를 주고받음으로써 통신의 신뢰성을 높임
- 웹이나 메일, 파일 공유 등과 같이 데이터를 누락시키고 싶지 않은 서비스는 TCP를 사용
-일반적으로 TCP와 IP를 함께 사용하는데, IP가 데이터의 배달을 처리한다면 TCP는 패킷을 추적 및 관리

② UDP(User Datagram Protocol)
- 데이터를 신속하게 보내고 싶을 때 UDP 프로토콜 사용
- 전송계층의 비연결 지향적 프로토콜 
	-> 비연결 지향적 : 데이터를 주고받을 때 연결 절차를 거치지 않고 발신자가 일방적으로 데이터를 발신하는 방식을 의미
- UDP는 데이터를 보내면 그것으로 끝이므로 신뢰성은 없지만 확인 응답과 같은 절차를 생략할 수 있으므로 통신의 신속성을 높임. 
-VoIP(Voice over IP)나 시간 동기, 이름 해결 등과 같이 무엇보다 속도를 필요로 하는 서비스는 UDP를 사용하고 있습니다.

출처 : https://coding-factory.tistory.com/614

```

<br/>

<br/>

<hr/>

### 💚 5계층 세션 계층 (Session Layer) <br/>

- 세션계층은 양 끝단의 응용 프로세스가 통신(대화)을 관리하기 위한 방법 제공<br/>

  - 최소한 기능 : **두 응용프로그램 간의 연결 설정, 유지 및 종료**<br/>
  - 그 밖에도 분실 데이터 복원을 위한 동기화 지점을 두어 상위 계층의 오류로 인한 데이터 손실을 복원<br/>

- **데이터가 통신하기 위한 논리적 연결을 담당** (통신을 하기위한 대문)<br/>

-  **TCP/IP 세션을 만들고 없애는 책임**을 지고 있음<br/>

  - 연결 세션에서 통신하는 사용자들을 동기화 하고 오류복구 진행<br/>

  - 동시 송수신 방식(duplex), 반이중 방식(half-duplex), 전이중 방식(full duplex)의 통신과 함께, 체크 포인팅과 유휴, 종료, 다시 시작 과정 등을 수행<br/>

- 통신 연결은 Port 기반으로 구성해 연결 (OS가 세션 계층)<br/>

- 세션 계층  예시<br/>

  - 통신 중 세션 형태 : TCP 세션 등<br/>
  - 네트워크 지원 용 API :  Socket, RPC, SMB 등<br/>
  - 데이터베이스 쿼리용 : SQL<br/>

- 데이터단위 : 메시지<br/>

```참고
💡이해를 위한 용어 설명

* 5계층 세션 계층
- 물리계층(1) ~ 전송계층(4)까지의 주된 기능은 단순히 데이터를 전달하는 것이였다면
- 세션계층(5) ~ 응용계층(7)의 주된 기능은 데이터를 송수신하는 양쪽의 종점 컴퓨터 내의 프로세스 간의 통신 프로토콜

세션
- 사전적 의미는 회의 등 여러가지 의미를 담고 있음
- 하나의 세션을 만든다는 것은 같은 계층의 송.수신측이 함꼐 회의를 한다는 것
- 예) 우편시스템에서 편지가 목적지에 잘 배송되더라도 상대방이 받고 싶은 의사가 없으면 편지는 버려지거나 되돌아옴
=> 컴퓨터 통신에서도 어떤 목적을 당성하기 위해 이를 처리하는 프로세서들이 서로 논리적으로 연결되어있어야하며 세션 계층이 이를 담강함

출처 : https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=ttochid1&logNo=10037450926

소켓(Socket) 
- 네트워크상에서 동작하는 프로그램 간 통신의 종착점(Endpoint) 
- 즉, 프로그램이 네트워크에서 데이터를 통신할 수 있도록 연결해주는 연결부

RPC(Remote Procedure Call)
- 별도의 원격 제어를 위한 코딩 없이 다른 주소 공간에서 함수나 프로시저를 실행할 수 있게 하는 프로세스 간 통신 기술
- IPC 방법의 한 종류로 원격지의 프로세스에 접근하여 프로시저 또는 함수를 호출하여 사용하는 방법
- 즉, RPC를 이용하면 프로그래머는 함수 또는 프로시저가 실행 프로그램이 존재하는 로컬 위치에 있든, 원격 위치에 있든 상관없이 동일한 기능을 수행할 수 있음을 의미

```

<br/>

<br/>

<hr/>

### 💚 6계층 표현 계층 (Presentation Layer) <br/>

- 표현 계층은 응용계층(7계층)으로 부터 받은 데이터를 세션 계층으로 보내기 전에 통신에 적당한 형태로 변환하고, 세션 계층에서 받은 데이터는 응용 계층에 맞게 변환화는 기능<br/>
  - 전송하는 데이터의 표현방식을 결정(ex. 데이터 변환, 압축, 암호화 등)<br/>
- 서로 다른 데이터 표현 형태를 갖는 시스템 간의 상호 접촉을 위해 필요한 계층<br/>
- 코드변환, 데이터 암호화, 데이터 압축, 구문 검색, 정보 형식(포맷) 변환, 문맥관리 기능을 함<br/>
- JPEG, MPEG등<br/>
- 데이터단위 : 메시지<br/>

<br/>

<br/>

<hr/>

### 💚 7계층 응용 계층 (Application Layer) <br/>

- 사용자와 가장 밀접한 계층, 네트워크(OSI 환경)에 접근할 수 있도록 서비스를 제공함<br/>
- 최종 목적지로, 응용 프로세스와 직접 관계하여 일반적인 응용서비스를 수행 (ex. Explore, chrome 등)<br/>
- 사용자 인터페이스, 전자우편, 데이터베이스 관리 등의 서비스 제공<br/>
- HTTP, SMTP, FTP, DNS 등과 같은 프로토콜이 있음<br/>
- 데이터단위 : 메시지<br/>



<hr/>

출처

⭐️⭐️참고 영상⭐️⭐️ - https://youtu.be/1pfTxp25MA8

https://onecoin-life.com/19

https://shlee0882.tistory.com/110

https://lxxyeon.tistory.com/155

https://mangkyu.tistory.com/15

https://coding-factory.tistory.com/614

https://better-together.tistory.com/140
