// 20220907

// Brown

# 🟠 들어가며
## 📝 운영체제와 응용프로그램
```
운영체제(OS) : Window, DOS, UNIX, Linux, Mac OS 등
응용 프로그램 : 한글, 엑셀, 메모장 등 컴퓨터 내의 다양한 프로그램들
```

- 운영체제 는 컴퓨터의 자원들을 효율적으로 관리하며 사용자가 컴퓨터를 편리하고 효과적으로 사용할 수 있도록 환경을 제공하는 여러 프로그램의 모임이라고 이해하면 된다. (추후 더 자세하게 다룬 포스팅을 올릴 예정이댜)
- 운영 체제는 컴퓨터 사용자와 컴퓨터 하드웨어 간의 인터페이스로서 동작하는 시스템 소프트웨어의 일종으로, 다른 응용프로그램이 유용한 작업을 할 수 있도록 환경을 제공해 준다.

<p align="center"><img width="500" alt="image" src="https://user-images.githubusercontent.com/96969693/188933432-37419da6-a892-4cc1-9302-6d97fe693d0c.png"></p>


## 📝 커널 (kernel)

컴퓨터와 전원을 켜면 운영체제는 이와 동시에 수행된다. 소프트웨어가 컴퓨터 시스템에서 수행되기 위해서는 메모리에 그 프로그램이 올라가 있어야 한다. 마찬가지로 운영체제 자체도 소프트웨어로서 전원이 켜짐과 동시에 메모리에 올라가야한다.

하지만 운영체제처럼 규모가 큰 프로그램이 모두 메모리에 올라가면 한정된 메모리 공간이 낭비가 심할 것이다. 

따라서 운영체제 중 항상 필요한 부분만을 전원이 켜짐과 동시에 메모리에 올려놓고, 그렇지 않은 부분은 필요할 때 메모리에 올려서 사용하게 된다. 이때 메모리에 상주하는 운영체제의 부분을 kernel(커널)이라고 한다.

```
즉, 커널은 메모리에 상주하는 부분으로써 운영체제의 핵심적인 부분을 뜻한다.
(그래서 보통은 '운영체제'라고 하면 kernel을 뜻하기도 한다)
```

## 📝 CPU 모드

CPU는 사용자 애플리케이션 (User application)이 시스템을 손상시키는 것을 방지하기 위해 2가지 모드를 제공한다. CPU에 있는 Mode bit로 모드를 구분하여 0은 ```커널모드(kernel mode)```, 1은 ```사용자모드 (user mode)```로 나뉘어서 구동된다. 

운영체제에서 프로그램이 구동되는데 있어서 파일을 읽어오거나, 파일을 쓰거나, 혹은 화면에 메세지를 출력하는 등 많은 부분이 커널 모드를 사용한다.

### 🔸 사용자 모드 (User Mode)

- 사용자 모드에서 사용자 애플리케이션 코드가 실행된다. 
- 사용자가 접근할 수 있는 영역에 제한이 있기 때문에 해당 모드에서는 하드웨어(디스크, I/O 등)에 접근할 수 없다.
(이전에 Blocking I/O를 배울 때 직접 하드웨어에 접근하지 못한다고 배웠다! 우후후)
- 접근을 위해서는 '시스템 콜(System Call)'을 사용해야 한다. 사용자 애플리케이션의 각 스레드들은 고유의 사용자 모드 스택을 갖는다.(?)

### 🔸 커널 모드 (Kernel Mode)

- 운영체제(OS)가 CPU를 사용하는 모드이다. 
- 시스템 콜을 통해 커널모드로 전환이 되면 운영체제는 하드웨어를 제어하는 명령어(Privileged Instructions)를 실행한다.
- Privileged Instructions는 사용자 모드에서 실행되면 exception이 발생한다.

<p align="center"><img width="661" alt="image" src="https://user-images.githubusercontent.com/96969693/188934386-e2ab0e07-7778-4c19-8f1e-48df7d33c6d9.png"></p>

```
위 그림과 같이 사용자 process는 User Mode에서 실행되다가 시스템 자원을 사용해야할 때 시스템 콜을 호출해서 커널 모드로 전환되어 작업을 수행하고 완료 시 다시 사용자 모드로 전환한다. 
```


# 🟠 시스템콜 (System Call, = 시스템 호출)

위에서 CPU 모드에 대해서 설명이 나올때 대충~! 시스템콜이 무슨 역할을 하는지 감이 왔을 것이다. 더 자세히 알아보자.

OS는 다양한 서비스 들을 수행하기 위해 하드웨어를 직접적으로 관리한다. 이와 반면 응용 프로그램은 OS가 제공하는 인터페이스를 통해서만 자원을 사용할 수 있다. OS가 제공하는 이러한 인터페이스를 '시스템 콜 (system call)' 이라고 한다.

시스템콜은 이러한 커널 영역의 기능을 사용자 모드가 사용 가능하게, 즉, 프로세스가 하드웨어에 직접 접근해서 필요한 기능을 할 수 있게 해준다. (즉, 응용프로그램은 시스템 콜을 사용해서 원하는 기능을 수행할 수 있음.)

보통 직접적으로 시스템콜을 사용하기 보다는 API(라이브러리 함수)를 통해 사용하게 된다.

<p align="center"><img width="669" alt="image" src="https://user-images.githubusercontent.com/96969693/188934642-b265be9a-3c3b-49e2-8df2-d6469250f7f4.png"></p>

```
위 그림처럼 운영체제(OS)는 메모리에 프로그램 적재, I/O처리, 파일시스템 처리 등 여러 서비스들을 제공하는데 사용자 프로세스는 이에 직접적인 접근이 아닌 시스템 콜 호출을 통해 서비스를 제공받을 수 있다.
```

## 🔸 시스템콜 종류

시스템콜은 크게 6가지로 분류할 수 있다.

### 1. 프로세스 제어 (Process Control)
  - 끝내기(exit), 중지 (abort)
  - 적재(load), 실행(execute)
  - 프로세스 생성(create process) - fork
  - 프로세스 속성 획득과 속성 설정
  - 시간 대기 (wait time)
  - 사건 대기 (wait event)
  - 사건을 알림 (signal event)
  - 메모리 할당 및 해제
### 2. 파일 조작 (File Manipulation)
  - 파일 생성 / 삭제 (create, delete)
  - 열기 / 닫기 / 읽기 / 쓰기 (open, close, read, write)
  - 위치 변경 (reposition)
  - 파일 속성 획득 및 설정 (get file attribute, set file attribute)
### 3. 장치 관리 (Device Manipulation)
  - 하드웨어의 제어와 상태 정보를 얻음 (ioctl)
  - 장치를 요구(request device), 장치를 방출 (release device)
  - 읽기 (read), 쓰기(write), 위치 변경
  - 장치 속성 획득 및 설정
  - 장치의 논리적 부착 및 분리
### 4. 정보 유지 (Information Maintenance)
  - getpid(), alarm(), sleep()
  - 시간과 날짜의 설정과 획득 (time)
  - 시스템 데이터의 설정과 획득 (date)
  - 프로세스 파일, 장치 속성의 획득 및 설정
### 5. 통신 (Communication)
  - pipe(), shm_open(), mmap()
  - 통신 연결의 생성, 제거
  - 메시지의 송신, 수신
  - 상태 정보 전달
  - 원격 장치의 부착 및 분리
### 6. 보호 (Protection)
  - chmod()
  - umask()
  - chown()


위에서 나온 명령어들은,,, UNIX에서 사용하는 명령어이다... (시스템콜은 스위프트에서는 어떻게 사용될까?)

<p align="center"><img width="533" alt="image" src="https://user-images.githubusercontent.com/96969693/188935476-c9e5cfb7-5b34-458e-aaae-8f3e60792f4f.png"></p>

# 🟠 Swift에서의 시스템 콜

### 📝 그전에, 시스템콜을 API(라이브러리 함수)로 접근한다는 게 무슨 뜻일까?

OS는 다양한 서비스들을 수행하기 위해 하드웨어를 직접적으로 관리한다. 이와 반면에 응용프로그램은 OS가 제공하는 인터페이스를 통해서만 자원을 사용할수 있다고 했다. 그래서 시스템콜이라는 개념이 나왔다고 까지 배웠다.

이러한 시스템 콜은 직접 사용하게 많은 어려움이 있다고 한다. (왜?) 때문에 프로그래밍 언어들은 시스템콜을 편리하게 사용하기 위한 수단으로 API를 제공한다.

<p align="center"><img width="492" alt="image" src="https://user-images.githubusercontent.com/96969693/188935583-e97a7ec1-7b31-41ee-aa26-e8dae7b9e1fb.png"></p>

### 📝 대부분 C언어와 관련있는 설명이던데, C언어를 사용한 간단한 프로그램을 예시로 시스템콜을 우선적으로 이해해보자.

```C++
#include <stdio.h>
int main()
{
  ...
  printf("Hello World!");
  ...
  return 0;
}
```

- printf() 함수는 user mode에서 수행되어 stdio 라이브러리를 호출한다.
- stdio 라이브러리는 시스템콜인 write()를 호출하고, 실행의 흐름은 kernel mode 로 바뀐다. 
- 커널은 호출을 실행하여 모니터에 문자열을 출력하고 실행의 흐름은 다시 user mode 로 넘어와 printf()의 함수의 다음단계를 진행한다.

<p align="center"><img width="452" alt="image" src="https://user-images.githubusercontent.com/96969693/188936069-8d29b54c-9c10-445e-b429-1b625fb3809d.png"></p>

### 📝 C언어에서의 시스템 콜 (그냥 알아만 두기..)

C언어에서 제공하고 있는 표준함수는 POSIX(Portable Operating System Interface)의 규정에 따라 함수를 제공하고 있으며, OS개발사 또는 컴파일러 개발사에서 추가적인 확장 API들을 제공하는 것이 일반적이다. 

C언어를 활용하여 개발하는 개발자 입장에서는 시스템콜 함수이든, 라이브러리 콜 함수이든 단지 함수의 형태이므로 특별히 구별되지는 않을 것이다. 그러나 system call function이 자주 호출되면 시스템 성능에 영향을 주기 때문에 최대한 알고쓰고 자제해야한다.

system call function 과 library call function의 차이점은 아래 게시글에서 추가로 확인해보자. (C언어에 집중된 설명이므로, 나는 간략하게 훑고 넘어갔다) [👉 시스템콜과 라이브러리콜 함수의 차이 보러가기](https://www.it-note.kr/3)


## 💡 아니 그럼 swift에서도 따로 system call 함수가 있는걸까?

과연 이게 Swift에서는 어떻게 사용되고 어떻게 쓰이는 것일까.

단순하게 생각해보자. 우리가 사용하는 Xcode도 응용프로그램이다. Xcode내부에서도 시스템콜을 통해서 파일을 가져오고 print를 하고 하지 않을까?

[스위프트 system 오픈소스 공개](https://www.swift.org/blog/swift-system/)

2020년쯤 스위프트에서도 시스템 콜과 관련한 함수들을 전부 오픈소스화 해놓았다고 말했다고 한다. 
즉, 원래는 C 인터페이스에 의존하여 시스템콜 함수를 호출했었는데 이 이후로부터 스위프트 독자적인 함수를 사용할 수 있게 했나보다...! 

(근데 왜 예시를 찾질 못하니,,)

일단 스위프트에서 어떤 방식으로 사용하는지에 대해서 전혀 찾지 못해서 여기까지만 조사했다.

## 📖 Reference
- [운영체제와 커널이란?](https://goodmilktea.tistory.com/23)
- [운영체제와 응요프로그램이란?](https://m.blog.naver.com/zerozero/60000338473)
- [운영체제 서비스와 시스템 콜](https://cloudstudying.kr/lectures/189)
- [시스템 콜](https://codybuilder.com/41)








