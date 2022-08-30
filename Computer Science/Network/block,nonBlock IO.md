// 2022.08.30 Rookie

## 요약

Block과 non Block은 작업을 수행하는 방식의 일종이며 데이터를 input, output하는 동안 작업을 중단하느냐 안하느냐로 구분한다.

---

## **Blocking I/O**

Blocking I/O 는 다음과 같은 순서로 이루어지는 작업을 뜻합니다.

### (1) Process(Thread)가 Kernel에게 I/O를 요청하는 함수를 호출합니다.

- Process와 thread
    
    **Process**
    
    Process는 컴퓨터에서 연속적으로 실행되는 컴퓨터 프로그램이다. 지금 이 글을 읽고 있다면 gitHub를 켜놨을터이니, gitHub가 프로세스가 되는 것이다. 
    
    프로세스는 각각 독립된 메모리 영역(code,data,stack,heap)을 할당받는다. 당연히 gitHub를 실행하면 이전에 했던 데이터들이 메모리에 올라가있어야 빠르게 프로세스가 수행되겠죠?
    
    **Thread**
    
    쓰레드는 프로세스 내에서 실행되는 작업 흐름 단위입니다. 
    
    gitHub를 켜면 우리는 다양한 작업을 수행합니다. 브랜치 옮기기, 커밋 남기기 등등… 이러한 작업이 한번에 딱 이뤄지지는 않겠죠? 예를 들어 커밋을 남긴다고하면 git 서버에 명령을 전달하고, 아이디에 맞는 기록을 찾는 복잡한 과정이 이루어지는데, 이 때 작업 단위를 쓰레드라고 합니다.
    
- Kernel
운영체제는 **항상 필요한 부분**만 전원이 켜짐과 동시에 메모리에 올려놓고 그렇지 않은 부분은 필요할 때마다 메모리에 올려서 사용하게 된다. 이 때 **메모리에 상주하는 운영체제의 일부분을 커널**이라 한다.
    
    **Reference**
    
    [https://goodmilktea.tistory.com/23](https://goodmilktea.tistory.com/23) 
    

프로그램이 수행되려면 당연히 자료(데이터)를 받아와야겟죠? 그러니 컴퓨터 운영체제 OS에게 자료의 입,출입을 요청하는 것입니다. 

### (2) Kernel이 작업을 완료하면 작업 결과를 반환 받음.

- 특징
    - I/O 작업이 진행되는 동안 user Process(Thread) 는 자신의 작업을 중단한 채 대기
    - Resource 낭비가 심함 (I/O 작업이 CPU 자원을 거의 쓰지 않으므로)

`여러 Client 가 접속하는 서버를 Blocking 방식으로 구현하는 경우` -> I/O 작업을 진행하는 작업을 중지 -> 다른 Client가 진행중인 작업을 중지하면 안되므로, client 별로 별도의 Thread를 생성해야 함 -> 접속자 수가 매우 많아짐 이로 인해, 많아진 Threads 로 *컨텍스트 스위칭 횟수가 증가함,,, 비효율적인 동작 방식*

- 컨텍스트 스위칭이란?
    
    동시에 다수의 프로세스를 수행하기 위해, 아주 짧은 시간간격으로 프로세스를 전환시켜 수행하는 작업 방식
    
    원래 한 프로세스를 실행하면 cpu가 점유되서 다른 프로세스를 할 수 없다고 한다.
    
    ## Reference
    
    [https://www.youtube.com/watch?v=1grtWKqTn50](https://www.youtube.com/watch?v=1grtWKqTn50) (우아한테크 유튜브 5분~7분)
    
    - 정의
    **멀티 프로세스 환경에서 CPU가 어떤 하나의 프로세스를 실행하고 있는 상태에서, **인터럽트 요청에 의해** 다음 우선 순위의 프로세스가 실행되어야 할 때, 기존의 프로세스의 상태 또는 레지스터 값(Context)을 저장하고 CPU가 다음 프로세스를 수행하도록 새로운 프로세스의 상태 또는 레지스터 값(Context)으로 **교체**
    하는 작업을 컨텍스트 스위칭 이라고 한다
    
    [https://velog.io/@taehee-kim-dev/컨텍스트-스위칭](https://velog.io/@taehee-kim-dev/%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8-%EC%8A%A4%EC%9C%84%EC%B9%AD) 
    

---

## No**n-Blocking I/O**

마찬가지로 non Blocking I/O 는 다음과 같은 순서로 이루어지는 작업을 뜻합니다.

하지만!!! I/O 작업이 진행되는 동안 User Process의 작업을 중단하지 않습니다. (매우 중요)

- 진행 순서
    1. User Process가 recvfrom 함수 호출 (커널에게 해당 Socket으로부터 data를 받고 싶다고 요청함)
    ** Socket: 네트워크상에서 동작하는 프로그램 간 통신의 종착점(Endpoint). 간단히 말해서는 특정 문자들을 조합하여 만든 네트워크 주소이다.
    
    2. Kernel은 이 요청에 대해서, 곧바로 recvBuffer를 채워서 보내지 못하므로, "EWOULDBLOCK"을 return함.
    
    ** buffer: 데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 메모리의 공간. buffer가 가득차게 되면 목적지로 데이터를 보내게 된다. buffer에 저장된 데이터들은 이진수 데이터들이며 buffer의 크기가 데이터 처리 단위가 된다고 한다.
    여기서 revbuffer는 데이터를 받아오는 동안 사용하는 buffer이다.
    
    3. **Blocking 방식과 달리, User Process는 다른 작업을 진행할 수 있음!!**
    
    4. recvBuffer에 user가 받을 수 있는 데이터가 있는 경우, Buffer로부터 데이터를 복사하여 받아옴.
        
        이때, recvBuffer는 Kernel이 가지고 있는 메모리에 적재되어 있으므로, Memory간 복사로 인해, I/O보다 훨씬 빠른 속도로 data를 받아올 수 있음. 
        
        이미지를 서버에서 통신해서 가져와서 휴대폰에 띄운다고 생각해보자! 이전에 내가 다운 받은 이미지가 buffer로 메모리 공간 어디에 저장되어있다면 굳이 URL을 사용하여 통신하지 않고 memory에서 꺼내쓸 수 있으니 훨씬 빠르다! 
         
        
    5. recvfrom 함수는 빠른 속도로 data를 복사한 후, 복사한 data의 길이와 함께 반환함.
    

---

## References

[https://velog.io/@rhdmstj17/소켓과-웹소켓-한-번에-정리-1](https://velog.io/@rhdmstj17/%EC%86%8C%EC%BC%93%EA%B3%BC-%EC%9B%B9%EC%86%8C%EC%BC%93-%ED%95%9C-%EB%B2%88%EC%97%90-%EC%A0%95%EB%A6%AC-1) (소켓에 대한 깊이있는 이해…)

[https://medium.com/@su_bak/term-socket이란-7ca7963617ff](https://medium.com/@su_bak/term-socket%EC%9D%B4%EB%9E%80-7ca7963617ff) (소켓에 대한 얕은 이해)

[https://m.blog.naver.com/ginameee/220839976258](https://m.blog.naver.com/ginameee/220839976258) (소켓, 버퍼 등 기본 개념 정리)
