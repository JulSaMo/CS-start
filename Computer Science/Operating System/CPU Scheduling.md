// 2022.09.07 루키

# **CPU Scheduling**

## 요약

1. CPU Scheduling이란 기아현상과 오버헤드 등을 고려하여 프로세스를 CPU에 효율적으로 할당하는 것을 말한다.
2. 현재 CPU를 할당받은 프로세스가 다른 프로세스에 의해 CPU를 뺏길 수 있냐 아니냐에 따라 선점, 비선점 스케줄링으로 나뉘게 된다.
3. CPU 스케줄링에 의해 프로세스의 상태 전이가 발생하며, 상태의 종류로는 5가지가 있다. (생성, 실행, 준비, 대기, 종료)

### **[#](https://gyoogle.dev/blog/computer-science/operating-system/CPU%20Scheduling.html#_1-%E1%84%89%E1%85%B3%E1%84%8F%E1%85%A6%E1%84%8C%E1%85%AE%E1%86%AF%E1%84%85%E1%85%B5%E1%86%BC)1. 스케줄링이란?**

**프로세스가 작업을 수행할 때, 언제 어떤 프로세스에 CPU를 할당할지를 결정하는 작업이다!**

스케줄링 작업을 할 때 오버헤드와 기아현상을 고려하며 다음의 목표를 지향한다.

- 기아 현상이란?
    
    특정 프로세스의 우선 순위가 낮아서 원하는 자원을 계속 할당받지 못하는 상태가 발생하는 것
    
- 오버헤드
    
    컴퓨터 기능에 있어 특정한 기능을 수행하기 위해 추가로 사용되는 컴퓨터의 자원. 따라서 오버헤드를 최소화하는 방향으로 스케줄링 해야함
    
- 스캐줄링 고려사항
    1. `Batch System`: 가능하면 많은 일을 수행. 시간(time) 보단 처리량(throughout)이 중요
    2. `Interactive System`: 빠른 응답 시간. 적은 대기 시간.
    3. `Real-time System`: 기한(deadline) 맞추기

애초에 컴터를 효율적으로 돌리기 위한 것이니까 당연히 저 위에 것들을 목표로 해야 좋은 스케줄링 결과가 나오겠죠??

---

### **[#](https://gyoogle.dev/blog/computer-science/operating-system/CPU%20Scheduling.html#_2-%E1%84%89%E1%85%A5%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B7-%E1%84%87%E1%85%B5%E1%84%89%E1%85%A5%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B7-%E1%84%89%E1%85%B3%E1%84%8F%E1%85%A6%E1%84%8C%E1%85%AE%E1%86%AF%E1%84%85%E1%85%B5%E1%86%BC)2. CPU 스케줄링의 종류**

스케줄링은 알고리즘에 따라 여러 방식으로 나뉘는데 크게는 선점 스케줄링과 비선점 스케줄링으로 나뉜다.

### 선점(preemptive)

한 프로세스가 CPU를 할당받아 실행중이라도 다른 프로세스가
현재 프로세스를 중지 시키고 CPU를 강제적으로 뺏을 수 있는 스케줄링 방식

### 비선점 (nonpreemptive)

한 프로세스가 CPU를 할당받아 실행중이라면 다른 프로세스들이
CPU를 강제적으로 뺏을 수 없는 스케줄링 방식

---

### **[#](https://gyoogle.dev/blog/computer-science/operating-system/CPU%20Scheduling.html#_4-cpu-%E1%84%89%E1%85%B3%E1%84%8F%E1%85%A6%E1%84%8C%E1%85%AE%E1%86%AF%E1%84%85%E1%85%B5%E1%86%BC%E1%84%8B%E1%85%B4-%E1%84%8C%E1%85%A9%E1%86%BC%E1%84%85%E1%85%B2)3. CPU 스케줄링의 종류**

## 선점 스케줄링

1. **Priority Scheduling**
    - 정적/동적으로 우선순위를 부여하여 우선순위가 높은 순서대로 처리함
    - **우선 순위가 낮은 프로세스가 무한정 기다리는 Starvation 이 생길 수 있음**
    - Aging 방법으로 Starvation 문제 해결 가능
    - aging 방법이란
        
        오래 기다린 프로세스의 우선 순위를 높여주는 방식
        
2. **Round Robin**

라운드 로빈의 사전적의미는 서명한 사람의 순서를 밝히지 않기 위해 원형으로 서명한 항의서라고 합니다!! 한국으로 따지면 사발통문(沙鉢通文)인 거죠?

- FCFS에 의해 프로세스들이 보내지고 각 프로세스가 동일한 시간의 `Time Quantum` 만큼 CPU를 선점하게 됨. 
→ 모두가 같은 타임퀀텀을 가진다는 의미에서 라운드 로빈이라고 이름 지은거같습니다.
- **FCFS란?**
    
    • 먼저 요청한 프로세스 순으로 스케줄링하는 것 (**(First-Come First-Served))**
    
- Time Quantum이란?
    
    실행의 최소 단위 시간. CPU 선점하게 해줄테니, 너 얼만큼 쓸래? 라고 지정해주는거임
    
- 할당 시간(`Time Quantum`)이 크면 FCFS와 같게 되고, 작으면 Context Switching이 잦아져서 오버헤드가 증가하게 된다는 특징이 있다.

3. Multilevel-Queue (다단계 큐)
 <img width="732" alt="image" src="https://user-images.githubusercontent.com/103009135/188775385-139ea185-ad5e-4bdf-bb3f-cbc9054501b8.png">
 작업들을 여러 종류의 그룹으로 나누어 여러 개의 큐를 이용하는 기법
 
 <img width="887" alt="image" src="https://user-images.githubusercontent.com/103009135/188775752-1a4c5871-1755-49ea-a751-8e996e1d68df.png">
<img width="837" alt="image" src="https://user-images.githubusercontent.com/103009135/188775798-8d97a924-53c9-49d6-8e05-0b97d7c08c96.png">

- 우선순위가 낮은 큐들이 실행 못하는 걸 방지하고자 각 큐마다 다른 `Time Quantum`을 설정 해주는 방식 사용
- 우선순위가 높은 큐는 작은 `Time Quantum` 할당. 우선순위가 낮은 큐는 큰 `Time Quantum` 할당.
- Quiz! 우선순위가 높다면 그만큼 작업시간을 많이 줘야 잘 처리될 거 같아서 Time Quantum을 넉넉히 줘야할 거 같은데 왜 작은 시간을 할당해줄까요?
    
    큐의 우선순위가 높다는 것은 사용자와 맞닿는 최전선의 프로세스들입니다. 사용자와 interactive 한 부분이기 때문에 당연히 최대한 빨리 처리해야하므로 작은 time quantum을 할당합니다. 
    

### 정리

다단계큐 알고리즘은 각각 프로세스의 중요도에 따라 큐로 나누고 각 큐에서 다른 알고리즘을 적용해 효율을 높일 수 있는 장점이 있습니다. 
하지만 한 번 해당 큐에 들어가면 프로세스는 다른 큐로 이동되거나 변경되는 것이 거의 불가능하다는 단점이 있습니다. 
즉 스케줄링 오버헤드가 낮은 대신에 inflexible 유연적이지 못합니다.

2. **Multilevel-Feedback-Queue (다단계 피드백 큐)
이런 다단계큐 알고리즘의 단점을 극복하기 위해 나온 알고리즘이 바로 다단계 피드백 큐 알고리즘입니다!!**

<img width="825" alt="image" src="https://user-images.githubusercontent.com/103009135/188775953-66ceead2-b491-401c-85fb-9e858f151559.png">

- 다단계 큐에서 자신의 `Time Quantum`을 다 채운 프로세스는 밑으로 내려가고 자신의 `Time Quantum`을 다 채우지 못한 프로세스는 원래 큐 그대로
    - Time Quantum을 다 채운 프로세스는 CPU burst 프로세스로 판단하기 때문
    - CPU Burst란?
        
        CPU 버스트는 사용자 프로그램이 CPU를 직접 가지고 빠른 명령을 수행하는 단계이다. 이 단계에서 사용자 프로그램은 CPU 내에서 일어나는 명령 (ex. Add)이나 메모리(ex. Store, Load)에 접근하는 일반 명령을 사용할 수 있다.
        
- 짧은 작업에 유리, 입출력 위주(Interrupt가 잦은) 작업에 우선권을 줌
- 처리 시간이 짧은 프로세스를 먼저 처리하기 때문에 Turnaround 평균 시간을 줄여줌

### **다단계 피드백 큐를 이해하기 위해서는 아래 링크글을 반드시 읽어보시길 바랍니다!!**

[https://jhnyang.tistory.com/156](https://jhnyang.tistory.com/156)

**멀티레벨큐가 우선순위에 따라 들어가는 입구가 달랐다면 멀티레벨피드백큐는 모든 프로세스들이 제일 위에 있는 큐로 일단 들어와요.**만약 제일 위에 있는 queue는 RR으로 스케줄링을 하는데 time-quantum을 8로 스케줄링을 해요, **자신의 time quantum을 다 채우지 못한 process는 냅두고 time quantum을 다 채운 프로세스는 그 밑의 레벨에 있는 큐로 들어가게 됩니다.** 특징은, 밑에 있는 큐는 타임퀀텀의 크기를 첫 번째 있는 큐의 두 배로 돌려요!마지막 큐는 백그라운드 프로세스가 보통 그랬듯이 대게 FCFS로 처리됩니다.

일단 multilevel queue인데 queue에 서로 feedback이 있죠? 그래서 이걸 multilevel feedback queue라 합니다. 그런데 이거의 의미가 뭔지 생각해 봅시다.
일단 시작은 다 똑같은 데로 들어왔는데 자신의 time quantum을 다 채운 애는밑으로 내려가고 자신의 time quantum을 다 채우지 못한 애는 그냥 원래대로 들어가요. **자신의 time quantum을 다 채운 거랑 다 못 채운거랑 의미는 뭘까요?**

이 특징은 바로 **CPU burst와 중요도의 상관관계를 사람들이 발견한데서 있습니다.보통 사용자와 interactive하지 않은, background의 프로세스는 CPU burst가 매우 크다는 특징을 이용한거죠.**자, 여러분 사양이 엄청 큰 게임을 다운로드 한다고 생각해봐요, 그 게임 다운로드 하는데 적어도 30분은 기다려야 한다고 합시다. 그럼 우리는 이거 그냥 백그라운드로 돌려놓고 인터넷서칭을 하죠, 즉 바로바로 처리해야할 일은 인터넷 서칭이 됩니다. 만약 게임다운로드 하는 동안 나는 아무것도 할 수 없다면 답답하고 짜증날테니까요 ㅎㅎㅎ

이렇게 **게임 다운로드처럼 CPU를 계속 써야하는, CPU burst가 큰 프로세스를 우선순위가 낮다고 판별하는 겁니다. 그리고 나와 상호작용할 가능성이 높은 프로세스, 내 입출력을 필요로 하는(마우스 클릭이라던지 키보드 타이핑이라던지) 이런 애들은 CPU처리가 I/O작업이랑 번갈아가며 일어나므로 CPU burst가 작다는 특징을 기져요 그리고 이를 우선순위가 높구나! 이런 특징을 활용한 것이 멀티레벨피드백 큐인겁니다** ㅎㅎ알겠죵?
 
time quantum을 다채웠다는것은 CPU burst process일 가능성이 높죠 그래서 한번 더 밑으로 내려보는겁니다. 16으로 했더니 그걸 또 다 채웠어!! 아 그럼 이거는 CPU bound process구나! 그러니까 아예 밑으로 내려가서 CPU bound process들은 사용자하고 대화형으로 동작하는 것이 아니니까 context switching을 안하고 그냥 개를 쭉 수행시켜주는 것이 유리하겠죠? 그러니까 FCFS로 그냥 하는겁니다.
즉 다음 단계로 넘어갈 수록 CPU burst가 크다는 거니까 우선순위가 점점 낮아진다! 이런 룰이 되는거예요

## **비선점 스케줄링**

1. **FCFS (First Come First Served)**
    - 큐에 도착한 순서대로 CPU 할당
    - 실행 시간이 짧은 게 뒤로 가면 평균 대기 시간이 길어짐
2. **SJF (Shortest Job First)**
    - 수행시간이 가장 짧다고 판단되는 작업을 먼저 수행
    - FCFS 보다 평균 대기 시간 감소, 짧은 작업에 유리
3. **HRN (Hightest Response-ratio Next)**
    - 우선순위를 계산하여 점유 불평등을 보완한 방법(SJF의 단점 보완)
    - 우선순위 = (대기시간 + 실행시간) / (실행시간)

### **[#](https://gyoogle.dev/blog/computer-science/operating-system/CPU%20Scheduling.html#_3-%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%89%E1%85%A6%E1%84%89%E1%85%B3-%E1%84%89%E1%85%A1%E1%86%BC%E1%84%90%E1%85%A2)4. 프로세스 상태**

프로세스는 실행의 흐름에 따라 상태(스테이트)가 변한다. 상태를 정의하는 이름은 운영체제에 따라 다르지만, 대부분 서로 비슷한 개념으##로 구성되어 있습니다. 프로세스의 흐름은 일반적으로 5개의 상태로 정의된다고 합니다.

<img width="909" alt="image" src="https://user-images.githubusercontent.com/103009135/188776044-31dca8f5-c64b-4879-a31f-bd0b74a7a37d.png">

### 프로세스의 5가지 상태

1. 생성 (New) : 프로세스 생성 상태
2. 실행 (Running) : 프로세스가 CPU에 할당되어 실행 중인 상태
3. 준비 (Ready) : 프로세스가 CPU에 할당되기를 기다리는 상태
4. 대기 (Waiting) : 보류(Block)라고도 하며, 프로세스가 입출력이나 이벤트를 기다리는 상태
5. 종료 (Terminated) : 프로세스 종료 상태

---

**프로세스의 상태 전이**

1. **승인 (Admitted)** : 프로세스 생성이 가능하여 승인됨.
2. **스케줄러 디스패치 (Scheduler Dispatch)** : 준비 상태에 있는 프로세스 중 하나를 선택하여 실행시키는 것.
3. **인터럽트 (Interrupt)** : 예외, 입출력, 이벤트 등이 발생하여 현재 실행 중인 프로세스를 준비 상태로 바꾸고, 해당 작업을 먼저 처리하는 것.
4. **입출력 또는 이벤트 대기 (I/O or Event wait)** : 실행 중인 프로세스가 입출력이나 이벤트를 처리해야 하는 경우, 입출력/이벤트가 모두 끝날 때까지 대기 상태로 만드는 것.
5. **입출력 또는 이벤트 완료 (I/O or Event Completion)** : 입출력/이벤트가 끝난 프로세스를 준비 상태로 전환하여 스케줄러에 의해 선택될 수 있도록 만드는 것.

- 선점 스케줄링 : `Interrupt`, `I/O or Event Completion`, `I/O or Event Wait`, `Exit`
- 비선점 스케줄링 : `I/O or Event Wait`, `Exit`

### **[#](https://gyoogle.dev/blog/computer-science/operating-system/CPU%20Scheduling.html#_5-cpu-%E1%84%89%E1%85%B3%E1%84%8F%E1%85%A6%E1%84%8C%E1%85%AE%E1%86%AF%E1%84%85%E1%85%B5%E1%86%BC-%E1%84%8E%E1%85%A5%E1%86%A8%E1%84%83%E1%85%A9)5. CPU 스케줄링 척도**

1. Response Time
    - 작업이 처음 실행되기까지 걸린 시간
2. Turnaround Time
    - 실행 시간과 대기 시간을 모두 합한 시간으로 작업이 완료될 때 까지 걸린 시간

---

### **[#](https://gyoogle.dev/blog/computer-science/operating-system/CPU%20Scheduling.html#%E1%84%8E%E1%85%AE%E1%86%AF%E1%84%8E%E1%85%A5) Original References (참고하면 이해하기 훨씬 좋아요!!)**

- 스케줄링 목표 : **[링크(opens new window)](https://jhnyang.tistory.com/29?category=815411)**
- 프로세스 전이도 그림 출처 : **[링크(opens new window)](https://rebas.kr/852)**
- CPU 스케줄링 종류 및 정의 참고 : **[링크(opens new window)](https://m.blog.naver.com/PostView.nhn?blogId=so_fragrant&logNo=80056608452&proxyReferer=https:%2F%2Fwww.google.com%2F)**
- 다단계큐 참고 : **[링크(opens new window)](https://jhnyang.tistory.com/28)**
- 다단계 피드백 큐 참고 : **[링크(opens new window)](https://jhnyang.tistory.com/156)**

## Additional references

글을 읽다가 모르는 부분이 나와 참고한 블로그들입니다. 

[https://velog.io/@yerin4847/CPU-스케줄링CPU-Scheduling](https://velog.io/@yerin4847/CPU-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81CPU-Scheduling) (CPU 스케줄링 참고 자료) 

[https://donggu1105.tistory.com/163](https://donggu1105.tistory.com/163) (큐에 관하여)
