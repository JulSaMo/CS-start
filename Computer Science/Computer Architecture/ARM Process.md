// 220728

// Seonghun Jeon (Jack)



# ARM 프로세스 (ARM Process)



## 🔡 ARM을 공부하기 전에..

CPU의 언어 (ex. 010101011) =! 프로그래밍 언어 (ex. 자바, 파이썬... )

ISA(Instruction Set Architecture)란 하드웨어와 소프트웨어 사이의 Interface를 정의하는 것. 하드웨어와 프로그램 사이의 매개체 역할을 한다.

즉 ISA란, 프로그래밍 언어와 CPU 언어를 이어주는 매개체 역할을 한다.

프로그래밍 언어가 컴파일을 거쳐 CPU의 언어로 변환이 되어야 컴퓨터가 이를 인식할 수 있는데 이를 도와주는 대표적인 ISA 언어가 인텔, AMD에서 제작한 x86, x86-64 등이다.

인텔, AMD가 독주하던 ISA 시장에 새로운 강자로 등장한 것이 ARM.

ARM은 CPU의 설계 뼈대까지만 만들어 타사에 판매하며, 설계도를 산 회사는 그 뼈대에 살을 붙여 CPU 칩을 완성시킨다. 

ARM은 주로 핸드폰 같은 작은 디바이스에서 쓰인다.

아이폰, 갤럭시 전부 ARM 기반

![스크린샷 2022-07-28 오후 6.13.50](/Users/seojeon22/Library/Application Support/typora-user-images/스크린샷 2022-07-28 오후 6.13.50.png)

![스크린샷 2022-07-28 오후 6.14.08](/Users/seojeon22/Library/Application Support/typora-user-images/스크린샷 2022-07-28 오후 6.14.08.png)



## 💪🏻 ARM이란?

- Advanced RISC Machine의 약자
- 회사 이름: 영국 반도체 기업
- CPU 아키텍쳐 이름: Arm 프로세서

![스크린샷 2022-07-28 오후 6.16.27](/Users/seojeon22/Library/Application Support/typora-user-images/스크린샷 2022-07-28 오후 6.16.27.png)



## 📑 Processor 란?

- 일반적으로 프로세서란, 이론적으로 메모리에 저장된 명령어들을 실행하는 유한 상태 오토마톤을 의미한다. (오토마톤: 자동적으로 정보 처리를 하는 기계. 또는, 그 추상적인 기능에 착안한 수학적 모델. 기계를 유한개의 입과 내부 상태에서 유한개의 출력을 방출하는 기구로서 다룸)
- 시스템의 상태는 프로세서에 있는 레지스터의 값들과 메모리에 저장된 값들에 의해 결정된다.
- 각각의 명령어는 이들의 상태 변화를 정의하며 또한 다음번에 실행될 명령어를 결정한다.



## 💪🏻 ARM Processor란?

- 메모리, 인터페이스, 라디오, 시스템 온 칩, 시스템 온 모듈 등이 포함된다.
- 임베디드 기기에 주로 사용되는 32bit 프로세서
- RISC 아키텍처가 있는 프로세서는 일반적으로 복잡한 명령 세트 컴퓨팅(CISC) 아키텍쳐보다 적은 트랜지스터를 필요로 하여 비용, 전력소비 및 열 방출을 향상시킨다. -> 이러한 특성은 스마트폰, 랩탑, 태블릿, 기타 임베디드 시스템과 같은 가볍고 휴대가능한 배터리 전원 장치에 바람직하지만 서버와 데스크탑에도 어느정도 유용하다.
- 모바일 기기 또는 IoT 디바이스에 많이 사용된다.
- 스마트폰에서 CPU 역할을 하는 AP(Application Processor)가 널리 보급되며 인지도가 올랐다.

![스크린샷 2022-07-28 오후 6.19.39](/Users/seojeon22/Library/Application Support/typora-user-images/스크린샷 2022-07-28 오후 6.19.39.png)

![스크린샷 2022-07-28 오후 6.40.44](/Users/seojeon22/Library/Application Support/typora-user-images/스크린샷 2022-07-28 오후 6.40.44.png)



## 💪🏻 ARM Processor를 배워야하는 이유!

- 소형 기기에서는 ARM 프로세서를 많이 사용한다.
- ARM 프로세서의 기본 원리를 알면 프로그램을 CPU가 어떻게 돌리는지 정확히 파악할 수 있다.
- ARM 프로세서의 원리를 제대로 파악하는 개발자들은 조금 더 안정적인 코드를 작성할 수 있다.
- RTOS나 운영체제의 세부 동작 원리를 배우려면 ARM 프로세서를 알아야한다.
- ARM 프로세서의 기본 원리를 알아야 스타트업이나 익셉션 코드를 작성할 수 있다.



## 😅 CISC? RISC?

CISC: Complex Instruction Set Computing

RISC: Reduced Instruction Set Computing

CISC 프로세서는 RISC 보다 지시사항이 많음

RISC의 기본적인 개념: 프로세서가 많은 작업을 수행하면 안된다. 기본 작업을 빠르게 수행하는 것이 중요하다.

CISC의 기본적인 개념: 시간이 좀 더 걸리더라도 복잡한 작업이 가능해야한다.

RISC에는 없는 수많은 명령어들이 CISC에는 있었기 때문에 직접 어셈블리 코드를 손으로 입력하던 옛 시대에는 CISC를 선호했다.

![스크린샷 2022-07-28 오후 5.52.27](/Users/seojeon22/Library/Application Support/typora-user-images/스크린샷 2022-07-28 오후 5.52.27.png)





### Reference

< ISA >

https://inyongs.tistory.com/108



< ARM >

https://www.youtube.com/watch?v=C_Xb5J5jVzY

​	