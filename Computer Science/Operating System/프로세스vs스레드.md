// 22.09.07 Noel



# ❤️ 프로세스 VS 스레드

<br/>

### 🤔 프로그램(Program)이란?<br/>

> 컴퓨터에서 실행할 수 있는 파일<br/>

- 윈도우의 경우 확장자가 .exe 인 파일들<br/>

<br/>

### 🤔 프로세스(Process)란<br/>

>  컴퓨터에서 연속적으로 실행되고 있는 컴퓨터 프로그램<br/>

- 메모리에 올라와 실행되고 있는 프로그램의 인스턴스(독립적인 개체)<br/>
- 운영체제로부터 시스템 자원을 항당 받는 작업의 단위<br/>

- 프로그램(program)이 실행되서 돌아가고 있는 상태, 즉 컴퓨터가 어떤 일을 하고 있는 상태<br/>
- 프로세스는 관리의 단위 (관리 주체는 OS)<br/>

#### 특징

<img width="798" alt="image" src="https://user-images.githubusercontent.com/103012104/188881267-90371266-f38a-460f-ba81-a257da2a6f44.png">

- 프로세스는 `각각 독립된 메모리 영역(Code, Data, Stack, Heap의 구조)을 할당` 받음<br/>

  | 구분      | 내용                                                         |
  | --------- | ------------------------------------------------------------ |
  | **Code**  | 코드 자체를 구성하는 메모리 영역(프로그램 명령)              |
  | **Data**  | 전역변수, 정적변수, 배열 등<br/>- 초기화 된 데이터는 Data 영역에 저장<br/>- 초기화 되지 않은 데이터는 bss 영역에 저장 |
  | **Heap**  | 동적 할당 시 사용 (new(), malloc() 등)                       |
  | **Stack** | 지역변수, 매개변수, 리턴 값 (임시 메모리 영역)               |

- 프로세스(Process) 하나당 `최소 1개의 스레드(Thread)가 존재`<br/>
- 각 프로세스는 `OS에서 별도의 주소공간을 할당`해줘 그 곳에서 실행되며, <br/>
- 한 프로세스는 `다른 프로세스의 변수나 자료구조에 접근할 수 없음`<br/>
  - 한 프로세스가 다른 프로세스의 자원에 접근하려면 `프로세스 간의 통신(IPC, inter-process communication)을 사용`해야함 <br/>

<br/>

<br/>

### 🤔 스레드(Thread)란 <br/>

> 프로세스 내에서 실행되는 여러 흐름 단위 <br/>
>
> 프로그램 내에서 다른 코드와 독립되어 실행될 수 있는 최소단위의 *instruction Sequence* <br/>

- 프로세스가 할당받은 자원을 이용하는 실행의 단위 <br/>

- 프로세스 = 연산꺼리, 고로 흐름(스레드)이 있는데 `최소 1개 ~ n개`가 있을 수 있음 <br/>

  - 한 프로세스 안에도 여러 개의 작업들이 동시에 진행 될 필요가 있음 <br/>
  - 여러 개의 흐름(스레드)이 있는 경우, 동시에 각자 작동❗️ <br/>
  - 한 프로세스에서 개별화된 코드의 실행이 스레드! <br/>

  ``` 예시
  크롬에서 
  ① 게임을 다운받는 동시에, 
  ② 웹 서핑도 할 수 있어야하고
  ③ 유튜브 영상의 데이터를 받아오면서, 받아진 데이터로 영상을 재생할 수 있어야함
  ```

- 특징 <br/>

  - 스레드는 프로세스 내에서 각각` Stack만 할당`받고 `Code, Data, Heap 영역은 공유`한다. <br/>
  - 스레드는 한 프로세스 내의 주소 공간이나 자원들(힙 공간 등)을 `같은 프로세스 내의 스레드끼리 공유`하면서 실행  <br/>
    -  반면 프로세스는 다른 프로세스의 메모리에 직접 접근할 수 없음 <br/>
  - 각각의 스레드는 별도의 레지스터와 스택을 갖고 있지만, 힙 메모리는 서로 읽고 쓸 수 있음 <br/>
  - 한 스레드가 프로세스 자원을 변경하면, 다른 이웃 스레드(sibling thread)도 변경 결과를 즉시 볼 수 있음 <br/>

<img width="763" alt="image" src="https://user-images.githubusercontent.com/103012104/188881342-9dced40c-5cc1-4cc3-8f7b-ce41f9f273d6.png">


```요약
🗒 요약
- 하나의 프로세스는 최소 하나의 스레드를 가짐
- 프로세스는 독립된 공간에 할당되어 다른 프로세스에 접근이 어려움
- 하나의 프로세스에는 여러 스레드가 있을 수 있음
	> 스레드가 여러개인 경우,스레드는 프로세스 내의 자원들을 공유하면서 동시에 각자 실행
- 운영체체(OS)의 작업 최소 단위 : 프로세스(Process) / CPU의 작업 최소 단위 : 스레드(Thread)
```

<br/>

<br/>

<hr/>

<br/>

# ❤️ 멀티 프로세스 / 멀티 스레드

<br/>

### 🤔 멀티 프로세스란?<br/>

- 하나의 응용프로그램을 여러 개의 프로세스로 구성하여 `각 프로세스가 하나의 작업(테스크)을 처리`하도록 하는 것<br/>

| 장단점   | 내용                                                         |
| -------- | ------------------------------------------------------------ |
| **장점** | ① 메모리 침범 문제를 OS 차원에서 해결<br/> ② 여러개의 자식 프로세스 중 하나에 문제가 발생 시, 그  프로세스만 타격, 다른 영향이 확산되지 않음 |
| **단점** | **① Context Switching에서의 오버헤드**<br/>    > 각 프로세스가 독립된 메모리 영역을 할당받아, 프로세스 사이에서 공유되는 메모리가 없어 Context Switching 발생 시, 캐쉬에 있는 모든 데이터를 리셋하고 다시 캐쉬 정보를 불러와야 함<br/>**② 프로세스 간의 복잡한 통신(IPC)가 필요**<br/>   >프로세스는 독립된 메모리 영역을 할당 받아, 하나의 프로그램에 속하는 프로세스 사이의 변수를 공유할 수 없음 |

```단어
💡 이해를 위한 용어 설명

① Context Switching
- CPU에서 여러 프로세스를 돌아가면서 작업을 처리하는데 이 과정을 Context Switching이라고 함
	> 구체적으로, 동작 중인 프로세스가 대기를 하면서 해당 프로세스의 상태(Context)를 보관하고, 
	> 대기하고 있던 다음 순서의 프로세스가 동작하면서 이전에 보관했던 프로세스의 상태를 복구하는 작업

```

<br/>

### 🤔 멀티 스레드란?<br/>

- 하나의 응용프로그램에서 여러 스레드를 구성해 각 스레드에게 하나의 작업을 처리하게 하는 것 <br/>
  - 윈도우, 리눅스 등 많은 운영체제들이 멀티 프로세싱을 지원하고있지만 멀티 스레딩을 기본으로 함 <br/>

| 장단점   | 내용                                                         |
| -------- | ------------------------------------------------------------ |
| **장점** | **① 시스템 자원 소모 감소 (자원의 효율성 증대)**<br/>    > 프로세스를 생성 해 자원을 할당하는 시스템 콜이 줄어 자원을 효율적으로 관리 할 수 있음<br/>**② 시스템 처리량 증가 (처리 비용 감소)**<br/>    > 스레드 간 데이터를 주고 받는 것이 간단해지고 시스텀 자원 소모가 줄어듦<br/>    > 스레드 사이의 작업량이 작아 Context Switcing이 빠름<br/>**③ 간단한 통신 방법으로 인한 프로그램 응답 시간 단축**<br/>    > 스레드는 프로세스 내의 Stack 영역을 제외한 모든 메모리를 공유하기때문에 통신의 부담이 적음 |
| **단점** | ① 주의 깊은 설계가 필요<br/>② 디버깅이 까다로움<br/>③ 단일 프로세스 시스템의 경우 효과를 기대하기 어려움<br/>④ 다른 프로세스에서 스레드를 제어할 수 없음 (프로세스 밖에서도 스레드 각각을 제어할 수 없음)<br/>⑤ 멀티 스레드의 경우, 자원 공유의 문제가 발생 (동기화 문제)<br/>⑥ 하나의 스레드에 문제 발생 시, 전체 프로세스가 영향을 받음 |

<br/>

<br/>

<HR/>

출처

https://youtu.be/x-Lp-h_pf9Q

https://youtu.be/iks_Xb9DtTM

https://gmlwjd9405.github.io/2018/09/14/process-vs-thread.html

https://velog.io/@nnnyeong/OS-%EB%A9%80%ED%8B%B0%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EB%A9%80%ED%8B%B0%EC%8A%A4%EB%A0%88%EB%93%9C-%EB%A9%80%ED%8B%B0-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EB%A9%80%ED%8B%B0%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EB%A9%80%ED%8B%B0%EC%8A%A4%EB%A0%88%EB%93%9C%EC%97%90%EC%84%9C%EC%9D%98-%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%86%B5%EC%8B%A0
