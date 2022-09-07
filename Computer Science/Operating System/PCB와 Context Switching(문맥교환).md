// 20220907

// Brown

# 🔸 Process Management

CPU가 프로세스가 어러개일 때, CPU 스케쥴링을 통해 관리하는 것을 말한다.

[process management 단계별로 살펴보기](https://velog.io/@hyehello/CS-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-OS-04.-Process-Management)


# 🟠 PCB (Process Control Block) 이란? 

- 운영체제가 프로세스를 제어하기 위해 정보를 저장해 놓는 곳으로, 프로세스의 상태 정보를 저장하기 위한 구조체이다.
- 프로세스 상태 관리와 Context Switching을 위해 필요하다.
- PCB는 프로세스 생성 시 만들어지며 주기억장치에 유지된다.
- CPU에 급한 프로세스 처리 때문에 긴급 요청이 왔을 때, 기존에 작업하던 프로세스를 어딘가에 임시저장해놓아야 급한 애를 빨리 처리한 후에 다시 불러올 수 있을 것이다. 즉, 프로세스에 관한 정보들을 어딘가에 놓을 공간이 필요하고, 이 공간이 PCB 이다.

```
PCB란 운영체제가 프로세스에 대한 중요한 정보를 저장해 놓을 수 있는 저장 장소
```

<p align="center"><img width="671" alt="image" src="https://user-images.githubusercontent.com/96969693/188939013-f3bf28f6-e60b-487a-b48a-e3fc8ac59c84.png"></p>

```
프로그램 실행 → 프로세스 생성 → 프로세스 주소 공간에 (코드, 데이터, 스택) 생성 → 이 프로세스의 메타데이터들이 PCB에 저장
```

## 🔸PCB 안에 들어있는 정보, Process Metadata

프로세스들의 특징을 갖고 있는 것을 Process Metadata 라고 한다 .

<p align="center"><img width="301" alt="image" src="https://user-images.githubusercontent.com/96969693/188939139-0af05124-9a79-429b-b492-d99b7dba4619.png"></p>

- Process ID: 프로세스를 구분하는 ID
  - PID라고도 부르기도하고, 프로세스의 고유 번호이다.
- Process State: 각 프로세스들의 상태를 저장한다
  - 준비, 대기, 실행 등의 상태
- Program Counter: 다음 Instruction의 주소를 저장하는 카운터. CPU는 이 값을 통해 Process의 Instruction을 수행한다.
  - 컴퓨터에서 말하는 Instruction는 컴퓨터에게 일을 시키는 단위로, 컴퓨터가 알아들을 수 있는 기계어로 이루어진 명령이다.
  - 하드웨어에서 사용하는 명령어이다. (사용자가 수행하는명령은 command, 소프트웨어적인 명령은 statement)
- Register: Accumulator, CPU Register, General Register 등을 포함한다.
- CPU Scheduling Information: 우선순위, 최종 실행 시간, CPU 점유 시간 등이 포함된다.
- Memory Information: 해당 프로세스 주소 공간 (lower bound~upper bound) 정보를 저장한다.
- Process Information: 페이지 테이블, 스케쥴링 큐 포인터, 소유자, 부모 등
- Device I/O Status: 프로세스에 할당된 입출력 장치 목록, 열린 팔린 목록 등
- Pointer: 부모/자식 프로세스에 대한 포인터, 자원에 대한 포인터 등
- Open File List: 프로세스를 위해 열려있는 파일의 리스트


위의 PCB정보가 아래 테이블처럼 저장된다!!

<p align="center"><img width="488" alt="image" src="https://user-images.githubusercontent.com/96969693/188939363-010d7e51-40e5-48b5-b622-ac07db459a59.png"></p>


## 🔸 PCB 관리 방법
- Linked List 방식으로 관리한다.
- PCB List Head에 PCB가 생성될 때마다 하나씩 데이터가 붙게 된다. 주소 값으로 연결이 이루어져있는 연결리스트이기 때문에 삽입과 삭제가 용이하다. 

``` 즉, 프로세스가 생성되면 해당 PCB가 생성되고, 프로세스 완료 시 제거된다.  이렇게 수행중인 프로세스를 변경할 때 CPU의 레지스터 정보가 변경되는 것을 Context Switching 이라고 한다. 
```

```
< 프로세스 생성 과정 >
1. 새로운 프로세스를 위한 프로세스 식별자를 할당한다.
2. 새로운 프로세스에 한 주소 공간과 프로세스 제어블록(PCB)를 할당한다.
3. 새로운 프로세스의 프로세서 제어 블록을 초기화한다. (상태정보, 카운터, 우선순위 등)
4. 새로운 프로세스를 스케줄링 큐의 준비/보류 리스트에 연결한다.
```

# 🟠 Context Switching 

## 🔸 Context Switching 이란?

```
멀티프로세스 환경에서 CPU가 어떤 하나의 프로세스를 실행하고 있는 상태에서 인터럽트 요청에 의해 다음 우선 순위의 프로세스가 실행되어야할 때 기존의 프로세스 상태 또는 레지스터값 (Context)를 저장하고 CPU가 다음 프로세스를 수행하도록 새로운 프로세스의 상태 또는 레지스터값(Context)으로 교체하는 작업
```

- 인터럽트 (Interrupt) : CPU가 프로그램을 실행하고 있을 때 실행중인 프로그램 밖에서 예외 상황이 발생하여 처리가 필요한 경우 CPU에게 알려 예외 상황을 처리할 수 있도록 하는 것을 말한다. (I/O request, CPU 사용 시간이 만료됐을때, 자식 프로세스를 만들 때 등과 같은 상황이 인터럽트 요청이다)

(쉬운말로 프로세스가 하던 일을 멈추고 이미 정해진 코드에서 요청에 대한 처리를 수행한다.)

### 📝 Context(레지스터 값)이란?
사용자와 다른 사용자, 사용자와 시스템 또는 디바이스간의 상호작용에 영향을 미치는 사람, 장소, 개체 등의 현재 상황(상태)를 규정하는 정보들을 말한다. 즉 여기서 나온 Context의 의미는 CPU가 해당 프로세스를 실행하기 위한 해당 프로세스의 정보들이다. (이 정보들은 위에 나온 PCB에 저장된다, 즉 PCB에 저장되는 정보들이 Context = 레지스터값!)

### ⚠️ 주의

참고로 Context Switching이 발생할 때, 해당 CPU는 아무런 일을 하지 못한다. 따라서 Context Switching이 잦아지면 오히려 오버헤드가 발생해서 효율(성능)이 떨어진다. 

## 🔸 Context Switching 은 어떻게 진행되는가?
- Task의 대부분 정보는 Register에 저장되고 PCB로 관리되고 있다.
- 현재 실행하고 있는 Task의 PCB정보를 저장하게 된다. (Process Stack, Ready Queue)
- 다음 실행할 Task의 PCB 정보를 읽어 Register에 적재하고 CPU가 이전에 진행했던 과정을 연속적으로 수행할 수 있다.
 

## 🔸 Context Switching 과정

- 인터럽트 시스템콜이 발생하면 p0에서 해당 데이터를 저장하고 
- p1 실행하기 위해서 p1의 정보들을 가지고옴
- 그리고 p1이 실행되고, 다시 p0로 돌아가려면
- 다시 진행

<p align="cener"><img width="537" alt="image" src="https://user-images.githubusercontent.com/96969693/188939690-b493a0ff-e908-486d-8865-8d7e446e0439.png"></p>


## 🔸 Context switching의 오버헤드

<p align="center"><img width="473" alt="image" src="https://user-images.githubusercontent.com/96969693/188939899-196b933c-65c3-422b-aa08-0541b16762e0.png"></p>

- idle : 아무것도 동작하지 않는 상태를 의미

```
이렇게 Idle가 겹치는 시기들을 오버헤드라고 한다. 이때 CPU가 메모리에 적재하는 중이라 아무것도 하지 않는 상태이다. Thread가 많아지면 Context swtiching이 많아져서 오버헤드가 점점 증가해서 성능에 영향을 미친다.
```

## 🔸 Context Switching swift에서는 어떻게 사용되나?

```swift
Task.yield()
```

이 키워드를 찾아보면 될것 같다. 공식 문서에서는 아래와 같이 설명했다.

```
현재 작업을 일시 중단하고 다른 작업을 실행할 수 있도록 하는 것
```
[yield() 애플 공식 문서](https://developer.apple.com/documentation/swift/task/yield())



# ✅ 면접에서 나왔던 질문 [출처](https://nesoy.github.io/articles/2018-11/Context-Switching)

- Computer 가 매번 하나의 Task만 처리할 수 있다면? 
  - 하나의 Task가 끝날 때 까지 다음 Task는 기다릴수밖에 없고, 동시에 작업할 수 없는 환경이 만들어지게 되면서 반응속도가 매우 느릴 것입니다.

- 그렇다면 다양한 사람들이 동시에 사용하는 것처럼 하기 위해선 어떻게 해야할까?
  - computer 멀티태스킹을 통해 빠른 반응속도로 응답할 수 있습니다. 
  - 빠른속도로 Task 를 바꿔가며 실행하기 때문에 사람의 눈으로 봣을때는 동시에 진행되는 것처럼하는 장점이 있습니다.
  - CPU 가 Task를 빠르게 바꿔가며 실행하기 위해서 Context Switchng이 필요하게 되었습니다.

- Context Switching이란 무엇입니까?
  - CPU가 어느 프로세스를 실행하고 있을때, 인터럽트 요청이 있을 경우 기존의 프로세스의 상태를 PCB에 저장하고, 새로운 프로세스를 수행하도록 프로세스를 교체하는 작업을 의미합니다.

- 왜 Context Switching이 필요한가?
  - Context Switching이 있기 때문에, 동시에 여러개의 프로세스가 동작하는 것처럼 프로세스를 실행시킬 수 있습니다. 하지만 사실은 context switching이 일어날 때는 CPU의 동작이 멈추는 '오버헤드'가 발생하여 성능저하의 원인이 되기도 합니다. 그렇기 때문에 CPU 스케줄링 알고리즘에서도 특별히 신경써서 고려해야하는 점이기 때문에 중요합니다!

- Context Switching 은 어떻게 진행되나요?
  - 멀티쓰레드로 작업중인 환경에서, 기존 프로세스를 실행하고 있는 도중 인터럽트 요청이 있는 경우 기존 테스크를 PCB에 저장합니다. 그리고 새로운 프로세스로부터 정보를 reload 하여 실행을 진행합니다. 이렇게 Context switching 하는 과정에서는 CPU는 동작을 멈추게 됩니다. 새로운 프로세스의 테스크를 끝내면 PCB에 저장하고, 기존의 프로세스 태스크를 다시 reload하여 태스크를 진행합니다.


## 📖 References

- [command, instruction, statement 차이점](https://foxtrotin.tistory.com/295)
- [운영체제-PCB란?](https://dev-mystory.tistory.com/119)
- [PCB](https://velog.io/@hoyun7443/PCB)
- [context switching이란?](https://nesoy.github.io/articles/2018-11/Context-Switching)
- [10분 테코톡 interrupt와 context switching](https://www.youtube.com/watch?v=-4HKhwlH3FQ)

