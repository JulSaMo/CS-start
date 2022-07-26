// 20220830
<br>
// Brown
<br>
<br>
<p align="center"><img width="718" alt="image" src="https://user-images.githubusercontent.com/96969693/187373027-f74b88db-65ed-46ff-bd80-426550a8d216.png"></p>

### 🍯 재미난 이야기
2014년 구글에서는 HTTP를 HTTPS로 모두 바꾸라고 권고했었다고 합니다.
그 전까지는 전자상거래가 있는 웹 사이트에서만 번거로운 HTTPS를 사용했는데, 보안이 더 강한 HTTPS로 전환을 장려하기 위해서 구글은 HTTPS를 사용하는 웹 사이트에 대해서 검색 순위 결과에 약간의 가산점을 준다면서 발표했다고 합니다. 그래서 이렇게 대대적인 전환이 이뤄졌다고 볼 수 있겠군요!!
<br>
<br>
# ✅ 면접 대비 요약
```Question``` HTTP 와 HTTPS의 차이점에 대해서 설명해보세요.
<br>
```Answer``` HTTP는 따로 암호화 과정을 거치지 않기 때문에 중간에 패킷을 가로챌 수 있고, 수정할 수 있습니다. 따라서 보안이 취약해집니다. 이를 보완하기 위해 나온것이 HTTPS이고, HTTPS는 중간에 암호화 계층을 거쳐서 패킷을 암호화합니다.
<br>
<br>

# 🟠 HTTP (Hypertext Transfer Protocol)
서로 다른 시스템들 사이에서 통신을 주고받게 해주는 가장 기초적인 프로토콜이다. 웹서핑을 할 때 서버에서 자신의 브라우저로 데이터를 전송해주는 용도로 가장 많이 사용된다. 인터넷 초기에 모든 웹사이트에서 기본적으로 사용됐던 프로토콜이기도 하다. 

즉, HTTP는 인터넷에서 하이퍼텍스트를 교환하기 위한 통신규약으로, 80번 포트를 사용하고 있다. 따라서 HTTP 서버가 80번 포트에서 요청을 기다리고 있으며, 클라이언트는 80번 포트로 요청을 보내게 된다.

```
💡 여기서 말하는 프로토콜이란?
컴퓨터 내부에서 또는 컴퓨터 사이에서 데이터 교환 방식을 정의하는 규칙 체계이다.
기기 간 통신은 교환되는 데이터의 형식에 대해 상호 합의를 요구한다. 
이런 형식을 정의하는 규칙의 집합이라고 보면 된다.
```

## 🔸 HTTP의 구조
HTTP는 애플리케이션 레벨의 프로토콜로 TCP/IP 위에서 작동한다. HTTP는 상태를 가지고 있지 않는 ```Stateless 프로토콜``` 이며 Method, Path, Versionn, Headers, Body로 구성된다.

<p align="center"><img width="717" alt="image" src="https://user-images.githubusercontent.com/96969693/187374731-f4a655d2-b7c8-42e2-b33b-25cf3d7956fe.png"></p>

### 🔸 HTTP의 문제점
하지만 HTTP는 암호화가 되지 않은 평문 데이터르 런송하는 프로토콜 이기 때문에, HTTP로 비밀번호나 주민번호 등을 주고받으면 제 3자가 정보를 조회할 수 있었다. 즉, 데이터가 쉽게 도난당할 수 있는 구조다.

# 🟠 HTTPS (Hypertext Transfer Protocol Secure)

HTTPS는 SSL(Secure Socket Layer)를 사용함으로써 HTTP의 문제점을 해결했다. SSL은 서버와 브라우저 사이에 안전하게 암호화된 연결을 만들 수 있게 도와주고, 서버 브라우저가 민감한 정보를 주고받을 때 이것이 도난당하는 것을 막아준다. 

HTTPS는 443번 포트를 사용하며, 네트워크 상에서 중간에 제 3자가 정보를 볼 수 없도록 암호화를 지원한다.

```
💡 SSL (Secure Socket Layer)란
암호화 기반 인터넷 보안 프로토콜이다. 
인터넷 통신의 개인정보 보호, 인증, 데이터 무결성을 보장하기 위해서 개발되었다.
```


## ✋🏻 여기서 잠깐, 대칭키 암호화, 비대칭키(공개키) 암호화에 대해서 알고 가야한다!
HTTPS는 대칭키 암호화 방식과 비대칭키 암호화방식 모두를 사용한다. 각각의 암호화방식은 다음과 같다.

```
< 대칭키 암호화>
- 클라이언트와 서버가 동일한 키를 사용해 암호화/복호화를 진행함
- 키가 노출되면 매우 위험하지만 연산 속도가 빠름
```


```
< 비대칭키 암호화 >
- 1개의 쌍으로 구성된 공개키와 개인키를 암호화/복호화 하는데 사용함
- 키가 노출되어도 비교적 안전하지만 연산 속도가 느림
```

비대칭키 암호화는 공개키/개인키 암호화 방식을 이용해 데이터를 암호화 하고 있다. 공개키와 개인키는 서로를 위한 1쌍의 키다.
- 공개키 : 모두에게 공개하는 키
- 개인키 : 나만 가지고 알아야하는 키

암호화를 공개키로 하느냐, 개인키로 하느냐에 따라 얻는 효과가 다른데, 공개키와 개인키로 암호화하면 각각 다음과 같은 효과를 얻을 수 있다.
- 공개키 암호화: 공개키로 암호화를 하면 개인키로만 복호화할 수 있다. (즉, 나만 볼 수 있다.)
- 개인키 암호화: 개인키로 암호화하면 공개키로만 복호화할 수 있다. (공개키는 모두에게 공개되어 있으므로, 내가 인증한 정보임을 알려 신뢰성을 보장할 수 있다.)

<p align="center"><img width="456" alt="image" src="https://user-images.githubusercontent.com/96969693/187376772-c4f511fe-39a7-4d8f-8d18-e6ef0263c9c7.png"></p>

### ✨ 조금 더 쉬운 이해를 위해 공개키와 개인키에 대한 그림 첨부!

<p align="center"><img width="800" alt="image" src="https://user-images.githubusercontent.com/96969693/188319062-68600cce-e72a-40e4-a7f3-70bbfc9dd551.png"></p>


## 🔸 HTTPS의 동작 과정
대칭키 암호화와 비대칭키 암호화를 모두 사용해서 빠른속도와 안정성을 모두 얻고있는 것이 장점이다.
HTTPS 연결과정에서는 먼저 서버와 클라이언트 간에 세션키를 교환한다. 여기서 세션키는 주고받는 데이터를 암호화하기 위해서 사용되는 대칭키이며, 데이터간의 교환에는 빠른연산속도가 필요하므로 세션키는 대칭키로 만들어진다.

문제는 이 세션키를 클라이언트와 서버가 어떻게 교환할 것이냐 인데, 이 과정에서 비대칭키가 사용된다. 즉, 처음 연결을 성립하여 안전하게 세션키를 공유하는 과정에서 비대칭키가 사용되는 것이고, 이후에 데이터를 교환하는 과정에서 빠른 연산속도를 위해 대칭키가 사용되는 것이다.

<p align="center"><img width="510" alt="image" src="https://user-images.githubusercontent.com/96969693/187380183-9e6f959f-49b6-46cb-9688-06fa148bdcb1.png"></p>

(사진에서 2번은 세션키를 교환하기 위해 안전하게 비대칭키 사용, 이후의 과정에서 빠른 연산속도를 위해 3) 대칭키 사용)

## 📝 실제 HTTPS 연결 과정이 성립되는 흐름을 살펴보자.
1. 클라이언트 (브라우저)가 서버로 최초 연결을 시도함.

<p align="center"><img width="440" alt="image" src="https://user-images.githubusercontent.com/96969693/187380815-0374143e-8ba5-4843-91aa-c3fafcda3254.png"></p>

2. 서버는 공개키를 브라우저에게 넘겨줌

<p align="center"><img width="418" alt="image" src="https://user-images.githubusercontent.com/96969693/187381012-3fa0f293-ce0c-4d8b-b6eb-43407afaea9f.png"></p>

3. 브라우저는 인증서의 유효성을 검사하고 세션키를 발급함.
4. 브라우저는 세션키를 보관하며, 추가로 서버의 공개키로 세션키를 암호화하여 서버로 전송함

<p align="center"><img width="418" alt="image" src="https://user-images.githubusercontent.com/96969693/187381306-4ede4b0b-40b0-4549-ab29-2f650105f868.png"></p>

5. 서버는 개인키로 암호화된 세션키를 복호화하여 세션키를 얻음.

<p align="center"><img width="406" alt="image" src="https://user-images.githubusercontent.com/96969693/187381481-387b0f2e-c9e9-4efe-9843-0908b953a2e4.png"></p>

6. 클라이언트와 서버는 동일한 세션키를 공유하므로, 데이터를 전달할 때 세션키로 암호화/복호화를 진행함

<p align="center"><img width="423" alt="image" src="https://user-images.githubusercontent.com/96969693/187381701-b6b30fe9-d36f-4e37-85cd-ad2d60a68ab8.png"></p>


## 📖 Reference
[그림출처, 전반적인 내용, 대칭/비대칭 암호화 방식 설명](https://mangkyu.tistory.com/98)

[요약 출처](https://zeroco.tistory.com/70)

[기본개념 출처](https://brunch.co.kr/@hyoi0303/10)






