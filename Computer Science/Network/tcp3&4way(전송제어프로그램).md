## TCP N-way Handshake 를 들어가기 전에
#### 포트 상태 정보
  - CLOSED: 포트가 닫힌 상태
  - LISTEN: 포트가 열린 상태로 연결 요청 대기중
  - SYN_RCV: SYNC 요청을 받고 상대방의 응답을 기다리는 중
  - ESTABLISHED: 포트 연결 상태

#### 플래그 정보
  - TCP Header에는 CONTROL BIT(플래그 비트, 6bit)가 존재하며, 각각의 bit는 "URG-ACK-PSH-RST-SYN-FIN"의 의미를 가진다.
      - 즉, 해당 위치의 bit가 1이면 해당 패킷이 어떠한 내용을 담고 있는 패킷인지를 나타낸다.
  - SYN(Synchronize Sequence Number) / 000010
      - 연결 설정. Sequence Number를 랜덤으로 설정하여 세션을 연결하는데 사용하며, 초기에 Sequence Number를 전송한다.
  - ACK(Acknowledgement) / 010000
      - 응답 확인. 패킷을 받았다는 것을 의미한다.
      - Acknowlegement Number 필드가 유효한지를 나타낸다.
      - 양단 프로세스가 쉬지 않고 데이터를 전송한다고 가정하면 최초 연결 설정 과정에서 전송되는 첫 번째 세그먼트를 제외한 모든 세그먼트의 ACK 비트는 1로 지정된다고 생각할 수 있다.
  - FIN(Finish) / 000001
      - 연결 해제. 세션 연결을 종료시킬 때 사용되며, 더 이상 전송할 데이터가 없음을 의미한다.

## TCP 3way Handshake이란?
#### TCP 3 Way Handshake는 TCP/IP 프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다.
  - Client > Server: TCP SYN
  - Server > Client: TCP SYN ACK
  - Client > Server: TCP ACK

## TCP 3way Handshaking 역할 (Connection Establish)
  - 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제로 데이터 전달이 시작하기 전에 한쪽이 다른 쪽이 준비되었다는 것을 알 수 있도록 한다.
  - 양쪽 모두 상대편에 대한 초기 순차일련번호를 얻을 수 있도록 한다.  

### TCP 3way Handshaking 과정
![3wayHandshake](https://user-images.githubusercontent.com/66079439/187107557-de54e79f-b2ed-4886-bc7a-ff164b627bbe.png)

[Step1]
  - 클라이언트는 서버에 접속을 요청하는 SYN 패킷을 보낸다. 이때 클라이언트 는 SYN을 보내고 SYN/ACK 응답을 기다리는 SYN_SENT 상태가 된다.  
  
[Step2]  
  - 서버는 SYN요청을 받고 클라이언트에게 요청을 수락한다는 ACK와 SYN flag가 설정된 패킷을 발송하고 클라이언트가 다시 ACK로 응답하기를 기다린다. 이때 서버는 SYN_RECEIVED 상태가 된다.  
  
[Step3]  
  - 클라이언트는 서버에게 ACK를 보내고 이후로부터는 연결이 이루어지고 데이터가 오가게 되는 것이다. 이때의 B서버 상태가 ESTABLISHED이다.

  
위와 같은 방식으로 통신하는 것이 신뢰성 있는 연결을 맺어준다는 TCP의 3 Way Handshake 방식이다.
  
  
## TCP 4way Handshaking 역할 (Connection Termination)
  - 3way Handshake가 TCP의 연결을 초기화 할 때 사용한다면, 4way Handshake는 세션을 종료하기 위해 수행되는 절차이다.

### TCP 4way Handshaking 과정
![4wayHandshake](https://user-images.githubusercontent.com/66079439/187108573-4df5bab7-ec58-4408-9ace-b3c3d2cfc9e0.png)

[Step1]
  - 클라이언트가 연결을 종료하겠다는 FIN 플래그를 전송한다.
  
[Step2]  
  - 일단 확인메시지를 보내고 자신의 통신이 끝날때까지 기다리는데 이 상태가 TIME_WAIT 상태다.
  
[Step3]  
  - 서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN 플래그를 전송한다.
  
[Step4]  
  - 클라이언트는 확인했다는 메시지를 보낸다.
  - 그런데 만약 서버에서 FIN을 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN 패킷보다 늦게 도착하는 상황이 발생한다면 어떻게 될까?
  - 클라이언트에서 세션을 종료시킨 후 뒤늦게 도착하는 패킷이 있다면 이 패킷은 Drop되고 데이터는 유실될 것이다. 이러한 현상에 대비하여 클라이언트는 서버로부터 FIN을 수신하더라도 일정시간(디폴트 240초) 동안 세션을 남겨놓고 잉여 패킷을 기다리는 과정을 거치게 된다.
  - 이를 TIME_WAIT이라고 한다.

+)
Q. TCP의 연결 설정 과정(3단계)과 연결 종료 과정(4단계)이 단계가 차이나는 이유?
A. 클라이언트가 데이터 전송을 마쳤다고 하더라도 서버는 아직 보낼 데이터가 남아있을 수 있기 때문에 일단 FIN에 대한 ACK만 보내고, 데이터를 모두 전송한 후에 자신도 FIN 메시지를 보내기 때문.

Q. 초기 Sequence Number인 ISN을 0부터 시작하지 않고 난수를 생성해서 설정하는 이유?
A. Connection을 맺을 때 사용하는 포트(Port)는 유한 범위 내에서 사용하고 시간이 지남에 따라 재사용된다.
따라서 두 통신 호스트가 과거에 사용된 포트 번호 쌍을 사용하는 가능성이 존재한다. 서버 측에서는 패킷의 SYN을 보고 패킷을 구분하게 되는데 난수가 아닌 순차적인 Number가 전송된다면 이전의 Connection으로부터의 오는 패킷으로 인식할 수 있다. 이런 문제가 발생할 가능성을 줄이기 위해서 난수로 ISN을 설정한다.

## Reference
  - https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake
  - https://velog.io/@averycode/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPUDP%EC%99%80-3-Way-Handshake4-Way-Handshake






