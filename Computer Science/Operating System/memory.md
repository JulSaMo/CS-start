# 메모리(Memory)

## 메인 메모리(Main Memory, Physical Memory, 주기억장치)
  - CPU가 직접 접근할 수 있는 기억 장치로, 프로세스가 실행되려면 프로그램 코드를 메인 메모리에 적재해 두어야 한다.
  - 그런데 만약 프로그램 용량이 메인 메모리보다 크면 어떤 일이 벌어질까?
  - 프로그램의 크기가 전체 메모리보다 크면 전체 프로그램을 메모리에 가져오는 대신, 적당한 크기로 잘라서 가져오는데 이를 메모리 오버레이(Memory Overlay)라고 한다. 즉, 실행하는 데 필수적인 모듈만 올려놓고 나머지는 필요할 때마다 메모리에 가져와 사용하는 것이다.

## 가상 메모리(Virtual Memory)
  - 실제 물리 메모리 개념과 사용자의 논리 메모리 개념을 분리한 것이다.
  - 메모리의 공간은 한정적이므로 사용자에게 더 많은 메모리를 제공하기 위해 가상주소를 사용한다.
  - 메모리 관리 장치는 가상 주소를 이용해 실제 데이터가 담겨 있는 주소로 변환해 준다.
  - 여기서 가상 주소 공간은 하나의 프로세스가 메모리에 저장되는 논리적인 모습을 가상 메모리에 구현한 공간이며,
  - 가장 주소는 해당 공간을 가리키는 주소이다.

## 가상 메모리가 필요한 이유
  - 물리 메모리의 한계
    - 모든 프로그램 코드를 물리 메모리에 올릴 수가 없다.
    - 그렇다해서 프로그램을 교체하면서 올리면 메모리 교체 성능 문제가 발생한다.

  - 가상 메모리의 장점
      - 프로그램 용량이 실제 물리 메모리보다 커도 된다.
      - 전체 프로그램이 물리 메모리에 올라와 있지 않아도 된다.
      - 더 많은 프로그램을 동시에 실행할 수 있다.
        - 응답 시간은 유지
        - CPU 이용률과 처리율은 증가
      - 즉 다중 프로그래밍을 실현하기 위해 물리 메모리의 제약을 보완하고 프로세스 전체를 메모리에 올리지 않고도 실행할 수 있도록 해준다.

# 주기억장치 & 보조기억장치

## 가상 메모리의 구현
#### 운영체제는 물리 메모리의 제약을 갖고 있는 주기억장치를 보조하기 위해 디스크를 보조기억장치(Paging Space)로 사용한다.
![다운로드](https://user-images.githubusercontent.com/66079439/188807024-58c4eb2e-2e43-4a6f-b191-0a9733526c1c.png)
#### 즉, 메인 메모리(주기억장치)와 디스크의 페이징 스페이스(보조기억장치)를 묶어 하나의 메모리처럼 동작하게 하며, 이를 통해 메인 메모리의 한계를 넘는 메모리 사용을 가능하게 하는 가상 메모리를 구현한다.

# Swapping
  - CPU 할당 시간이 끝난 프로세스의 메모리에 보조기억장치를 내보내는 작업(Swap-out)
  - CPU 할당 시간이 끝난 프로세스의 메모리에 보조기억장치를 불러오는 작업(Swap-in)
  - Swap 작업에는 디스크 전송 시간이 돌기 때문에 메모리 공간이 부족할 때 Swapping이 이루어진다.

# 메모리 관리
  - 다중 프로그래밍 시스템에 여러 프로세스를 수용하기 위해 주기억장치(RAM)을 동적 분할하는 메모리 관리 작업이 필요함.
  - 즉, 하드 디스크에 있는 프로그램을 어떻게 메인 메모리에 적재할 것인지 판단해야함

## 연속 메모리 관리
#### 프로그램 전체가 하나의 커다란 공간에 연속적으로 할당되어야 한다.
  - 고정 분할 기법: 주기억장치가 고정된 파티션으로 분할 -> 내부 단편화 발생
  - 동적 분할 기법: 파티션들이 동적 생성되며 자신의 크기와 같은 파티션에 적재 -> 외부 단편화 발생
#### 이렇게 연속 메모리 관리 기법을 사용할 경우, 단편화 현상이 발생한다.

## 단편화
#### 기억 장치의 빈 공간 또는 자료가 여러 조각으로 나뉘는 현상이다. 프로세스들이 메모리에 적재되고 제거되는 일이 반복되면, 프로세스들이 차지하는 메모리 틈 사이에 사용하지 못할 만큼의 자유 공간이 늘어나게 된다. 이러한 단편화는 2가지로 나뉜다.
  - 내부 단편화
    - 프로세스가 사용하는 메모리 공간에 남는 부분
    - 프로세스가 요청한 양보다 더 많은 메모리를 할당할 때 발생하며, 메모리 분할 자유 공간과 프로세스가 사용하는 공간의 크기 차이를 의미한다.
![내부단편화](https://user-images.githubusercontent.com/66079439/188808586-1bf63926-651b-4fcc-ac14-26e4acc30aff.png)
  
  - 외부 단편화
    - 메모리 공간 중 사용하지 못하게 되는 부분
    - 메모리 할당 및 해제 작업의 반복으로 작은 메모리가 중간 중간 존재할 수 있다. 이렇게 사용하지 않는 메모리가 존재해서 총 메모리 공간은 충분하지만 실제로 할당할 수 없는 상황이다.
    - 외부 단편화를 해결하기 위해 압축을 이용하여 프로세스가 사용하는 공간을 한쪽으로 몰 수 있지만, 작업 효율이 좋지는 않다.
![외부단편화](https://user-images.githubusercontent.com/66079439/188808761-7f068904-ef3f-4f20-9aef-84841a954906.png)

## 불연속 메모리 관리
#### 프로그램의 일부가 서로 다른 주소 공간에 할당될 수 있는 기법이다. 앞서 봤던 단편화 문제를 해결하기 위해 제시된 기법으로, 외부 단편화 해소를 위한 페이징과 내부 단편화 해소를 위한 세그멘테이션으로 나뉜다.

## Reference
  - https://aeroej.tistory.com/124
