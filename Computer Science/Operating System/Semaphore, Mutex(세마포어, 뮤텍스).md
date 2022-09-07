// 20220907

// Brown

# 🟠 들어가며

## 🔸 Critical section (임계영역) 이란?

- 여러 프로세스가 데이터를 공유하며 수행될 때, 각 프로세스에서 공유 데이터를 접근하는 프로그램 코드 블록
- 즉, 여러 프로세스가 동일 자원을 동시에 참조하여 값이 오염될 위험 가능성이 있는 영역!!
- 공유 데이터를 여러 프로세스가 동시에 엑세스하면, 시간적인 차이 등으로 잘못된 결과를 낼 수 있기 때문에 한 프로세스가 공유 데이터를 엑세스하고 있을 때 다른 프로세스들은 절대로 그 데이터를 엑세스하지 못하도록 해야한다. 그래서 프로그래밍 시, 성능 향상을 위해 임계 영역을 최소화하는 설계를 해야한다.
 
# 🟠 세마포어 (Semaphore)

<p align="center"><img width="473" alt="image" src="https://user-images.githubusercontent.com/96969693/188944444-6b73e047-e96f-4903-9d21-1411f663261b.png"></p>

- 프로세스 간 메시지를 전송하거나 공유메모리를 통해 특정 데이터를 공유하게 되는 경우 문제가 발생할 수 있다. (메시지 전송이나 공유메모리 관련 프로세스 간 통신 참고 👉 https://didu-story.tistory.com/313)
- 즉, 공유된 자원에 여러 개의 프로세스가 동시에 접근하게 되면서 문제가 발생하는 것으로써, 공유된 자원 속 하나의 데이터는 한 번에 하나의 프로세스만 접근할 수 있도록 제한해두어야 한다.
- 이를 위한 것이 바로 '세마포어(Semaphore)' 이다.

```
<세마포어의 기본 지식을 알고가자>
- 동시에 하나의 자원에 접근을 방지하게 할 수 있는 비동기 문제를 해결하는데 사용된다.
- 여러 프로세스가 데이터를 공유하면서 작업을 수행할 때, 동시에 접근하면 안되는 자원을 동시에 접근할 수 없도록 막는 플래그 기능을 한다. 
- Semaphore 는 공유 자원에 진입할 수 있는 허용 개수를 의미한다.  (0이 되면 프로세스들의 공유 자원에 진입하는 것을 막는 것)
```

## 🔸 세마포어 (Semaphore) 쉽게 이해하기 

서버에 프린터기 다섯대가 물려있다고 치자. 사용자가 프린트를 사용하려고 서버에 요청을 보냈다. 그러면 공유자원 즉 프린터가 5개 있으니까 세마포어는 처음에 5로 설정된다. 그리고 프린터를 사용자가 사용할 때마다 하나씩 세마포어가 감소된다. 그러다가 사용할 프린터가 없어지면 세마포어는 조만간 0이 되고, 다 쓰고 반환하면 세마포어는 다시 +1 증가한다. 이런식으로 생각하면 된다!!

```
즉, 세마포어는 단순히 변수라고 생각하면 편하다. 공유자원의 개수를 나타내는 변수
```

```swift
var semaphore = 2

// 작업1 수행 
semaphore -= 1 

// 작업2 수행
semaphore -= 1 // 현재 semaphore == 0

// 작업 3 수행
// 현재 semaphore 가 0이기 때문에 대기한다!
```

## 🔸 세마포어(Semaphore) 접근 함수 : wait(), signal()

이를 위해 제공되는 함수가 wait()과 signal() 이다. 

### 📝 wait() 

- semaphore 의 값이 현재 0보다 크면 값을 -1
- 카운팅 값이 0이 되면 값이 증가할때까지 대기
- 프로세스가 자원을 사용할테니 '기다려라!'라는 의미

### 📝 signal()

- semaphore 값을 +1
- 프로세스가 자원을 사용하고 나왔다는 '신호'를 의미

## 🔸 Swift에서의 semaphore ✨

스위프트에서는 semaphore의 역할을 하는 DispatchSemaphore가 있다. [👉참고글](https://sujinnaljin.medium.com/ios-%EC%B0%A8%EA%B7%BC%EC%B0%A8%EA%B7%BC-%EC%8B%9C%EC%9E%91%ED%95%98%EB%8A%94-gcd-10-cb37c3e0cf13)


### 1. 동시 작업 개수 제한

공유 자원에 접근 가능한 작업 수를 2로 제한한 코드를 작성해보자.

```swift
let semaphore = DispatchSemaphore(value: 2)
```

위와 같이 공유 자원에 접근 가능한 (혹은 한번에 실행 가능한) 작업 수를 명시하고, 임계 구역에 들어갈 때에는 semaphore의 wait()를, 나올때는 signal()을 호출한다. (wait가 -1, signal 이 +1)

```swift
for i in 1...8 {
    semaphore.wait() //semaphore 감소
    DispatchQueue.global().async() {

        // 임계구역 (critical section)
        print("공유 자원 접근 시작 🌹")
        sleep(3)

        print("공유 자원 접근 종료 🥀")
        sleep(3)
        semaphore.signal() //semaphore 증가
    }
}
```

이렇게 하면 접근 가능한 작업수가 2개 이기 때문에  2개 안에서 작업이 왔다갔다 한다. (시작시작, 종로종료, 시작시작,,, )

<p align="center"><img width="181" alt="image" src="https://user-images.githubusercontent.com/96969693/188944954-c8ccf000-04f9-4562-bc89-16eeb402f99a.png"></p>


### 2. 두 쓰레드의 특정 이벤트 완료 상태 동기화

DispatchSemaphore는 두 가지 방식으로 사용가능하다. 하나는 위에서 본 동시 작업 개수를 제한하는 것이고, 하나는 두 쓰레드가 특정 이벤트의 완료 상태를 동기화하는 경우에 유용하다는 것이다.

```
Useful for when two threads need to reconcile the completion of a particular event.
```

이게 무슨말이냐면

- 쓰레드 A는 작업 A 실행중
- 쓰레드 B는 작업 A가 끝난 후에 무언가르 수행하려고 함.

이런 상황에서 쓰레드 B(소비자)는 예상된 작업을 기다리기 위해서 wait를 호출하고, 쓰레드 A(생성자)는 작업이 준비되면 signal을 호출하는 식으로 쓰레드 B가 작업 A의 완료 상태를 동기화할 수 있다는 것이다.

<br>
이런 방식으로 사용할 경우에는 semaphore 초기값을 0으로 설정한다.

```swift
//DispatchSemaphore 초기값 0으로 설정
let semaphore = DispatchSemaphore(value: 0)

print("task A가 끝나길 기다림")

// 다른 스레드에서 task A 실행
DispatchQueue.global(qos: .background).async {
    //task A
    print("task A 시작!")
    print("task A 진행중..")
    print("task A 끝!")
    //task A 끝났다고 알려줌
    semaphore.signal()
}

// task A 끝날때까지는 value 가 0이라, task A 종료까지 block
semaphore.wait()        
print("task A 완료됨")
```

- task A가 끝나지 않았따면 (즉 , signal()이 실행되지 않았다면) semaphore.wait() 이후의 작업은 실행되지 않을 것이다.
- 그 전의 세마포어 값은 0이기 때문에

## 🟠 다른 예시 코드 [코드참고 👉](https://onelife2live.tistory.com/5)

아래 코드도 세마포어를 사용한 예시이다. 이 코드를 돌리면 결과값이 3000이 나오는데, 만약에 세마포어를 사용하지 않았다면 3000이 나오지 않고 더 작은 값이 나올 것이다. 모든 함수가 동시에 접근하여 연산하려고 하기 때문이다! 
세마포어를 사용했기 때문에 작업이 한개씩 진행됐음을 확인할 수 있다.

```swift
let queue = DispatchQueue(label: "Queue", attributes: .concurrent)
let group = DispatchGroup()
var result: Int = 0

// 보통 리소스 풀을 관리할 때는 0보다 큰 값을 value 파라미터로 전달합니다.
// 여러 작업을 하나씩 순서대로 실행해야 한다면 1을 전달합니다.
let semaphore = DispatchSemaphore(value: 1)

queue.async(group: group) {
    for _ in 1...1000 {
        semaphore.wait() // 1 감소
        result += 1
        semaphore.signal() // 1 증가
    }
}

queue.async(group: group) {
    for _ in 1...1000 {
        semaphore.wait()
        result += 1
        semaphore.signal()
    }
}

queue.async(group: group) {
    for _ in 1...1000 {
        semaphore.wait()
        result += 1
        semaphore.signal()
    }
}

group.notify(queue: DispatchQueue.main) {
    print(result)
}

// 3000
```

[👉 이 글도 읽어보면 좋을 것 같다. UIKit에서 어떻게 코드를 작성하는지 엿볼수있다!](https://ios-development.tistory.com/920)


# 🟠 뮤텍스 (Mutex) 

```
동시 프로그래밍에서 공유 불가능한 자원의 동시 사용을 피하기 위해서 사용하는 알고리즘
```

- 임계구역(critical section)을 가진 쓰레드들의 실행시간 (running time)이 서로 겹치지 않고 각각 단독으로 실행 (상호배제) 되도록 하는 기술
- 한 프로세스에 의해 소유될 수 있는 key를 기반으로 한 상호배제 기법
- key에 해당하는 어떤 객체 (object)가 있으며, 이 객체를 소유한 쓰레드/프로세스 만이 공유자원에 접근할 수 있다.
- 다중 프로세스들의 공유 리소스에 대한 접근을 조율하기 위해 동기화 (Synchronization) 또는 락(lock)을 사용한다.
- 즉, 뮤텍스 객체를 두 쓰레드가 동시에 사용할 수 없다!

<p align="center"><img width="518" alt="image" src="https://user-images.githubusercontent.com/96969693/188945913-adcb6bcd-d3b4-4c31-9c8e-3e96d0fb9158.png"></p>

## 🟠 뮤텍스 (Mutex) 쉽게 이해하기 

[참고 👉](https://worthpreading.tistory.com/90)

뮤텍스는 화장실이 하나 뿐이 없는 식당에 비유할 수 있다. 화장실을 가기 위해서는 카운터에서 열쇠를 받아가야한다. 
내가 만약 화장실을 가려고하는데, 카운터에 키가 있으면 화장실에 사람이 없다는 뜻이고, 나는 그 열쇠를 이용해서 화장실에 갈 수 있다.

<p align="center"><img width="271" alt="image" src="https://user-images.githubusercontent.com/96969693/188946092-c0f6b9c7-a2fd-4ea4-8398-4285d9c293ab.png"></p>

내가 만약 화장실에 있는데 옆테이블에 잇는 사람도 화장실에 가고싶다. 이 사람은 아무리 급하더라도, 화장실 키가 없기 때문에 화장실에 가지 못한다. 이사람은 결국 카운터에서 키가 올때까지 나를 기다려야한다.

<p align="center"><img width="246" alt="image" src="https://user-images.githubusercontent.com/96969693/188946333-4e95308d-0f51-448b-942f-bddb351e87dd.png"></p>

또 내 옆옆테이블에서 화장실이 가고싶다. 이사람도 또 기다려야한다.

<p align="center"><img width="275" alt="image" src="https://user-images.githubusercontent.com/96969693/188946311-fa3d343c-0541-4ae2-bb35-90dc7f929e01.png"></p>

내가 화장실에서 나와서 키를 돌려두었다. 이제 기다리던 사람 중 맨 앞사람이 키를 받아 화장실에 갈 것이다.

<p align="center"><img width="275" alt="image" src="https://user-images.githubusercontent.com/96969693/188946284-f6ed576f-1326-4382-b5d0-f6d35a3c5d1b.png"></p>

```
이렇게 동작하는 방식이 뮤텍스가 동작하는 방식이다. 화장실을 이용하는 사람은 프로세스 혹은 쓰레드이며, 화장실은 공유자원, 화장실 키는 공유자원에 접근하기 위한 어떤 오브젝트이다!
```

<p align="center"><img width="317" alt="image" src="https://user-images.githubusercontent.com/96969693/188946246-b2b80b84-469f-437e-9e47-ab319cbe0061.png"></p>


# 🟠 Swift에서의 Mutex ✨

스위프트에서의 뮤텍스는, DispatchSemaphore 처럼 따로 지원하지 않는 것으로 보인다. 그래서 Mutex를 Swift에서 사용하도록 밴치마킹(?)해서 만든 글을 첨부한다. 읽어보면 아주 좋을듰!!!!

https://medium.com/@sergebouts/swift-mutex-benchmark-b21ee293d9ad
 

# 🟠 대표적인 뮤텍스 알고리즘

## 1. 데커 (Dekker) 알고리즘

flag 와 turn 변수를 통해 임계구역에 들어갈 프로세스/스레드를 결정하는 방식

```
flag : 프로세스 중 누가 임계영역에 진입할 것이지 나타내는 변수
turn : 누가 임계구역에 들어갈 차례인지 나타내는 변수
```

```C++
while(true) {
    flag[i] = true; // 프로세스 i가 임계 구역 진입 시도
    while(flag[j]) { // 프로세스 j가 현재 임계 구역에 있는지 확인
        if(turn == j) { // j가 임계 구역 사용 중이면
            flag[i] = false; // 프로세스 i 진입 취소
            while(turn == j); // turn이 j에서 변경될 때까지 대기
            flag[i] = true; // j turn이 끝나면 다시 진입 시도
        }
    }
}

// ------- 임계 구역 ---------

turn = j; // 임계 구역 사용 끝나면 turn을 넘김
flag[i] = false; // flag 값을 false로 바꿔 임계 구역 사용 완료를 알림
```


## 2. 피터슨 (peterson) 알고리즘

데커와 유사하지만, 상대방 프로세스/스레드에게 진입 기회를 양보하는 것에 차이가 있다.

```C++
while(true) {
    flag[i] = true; // 프로세스 i가 임계 구역 진입 시도
    turn = j; // 다른 프로세스에게 진입 기회 양보
    while(flag[j] && turn == j) { // 다른 프로세스가 진입 시도하면 대기
    }
}

// ------- 임계 구역 ---------

flag[i] = false; // flag 값을 false로 바꿔 임계 구역 사용 완료를 알림
```


## 3. 제과점 (Bakery) 알고리즘

여러 프로세스/스레드에 대한 처리가 가능한 알고리즘. 가장 작은 수의 번호표를 가지고 있는 프로세스가 임계구역에 진입한다.

```C++
while(true) {
    
    isReady[i] = true; // 번호표 받을 준비
    number[i] = max(number[0~n-1]) + 1; // 현재 실행 중인 프로세스 중에 가장 큰 번호 배정 
    isReady[i] = false; // 번호표 수령 완료
    
    for(j = 0; j < n; j++) { // 모든 프로세스 번호표 비교
        while(isReady[j]); // 비교 프로세스가 번호표 받을 때까지 대기
        while(number[j] && number[j] < number[i] && j < i);
        
        // 프로세스 j가 번호표 가지고 있어야 함
        // 프로세스 j의 번호표 < 프로세스 i의 번호표
    }
}

// ------- 임계 구역 ---------

number[i] = 0; // 임계 구역 사용 종료
```

# 🟠 뮤텍스와 세마포어 차이점

무슨말인지 잘 모르겠어서 더더더 딮하게 공부해야할 듯 싶습니다,,, 후,, 

### 1️⃣ 동기화 대상의 개수 
- Mutex는 동기화 대상이 only 1개 일 때 사용한다.
- Semaphore는 동기화 대상이 1개 이상일 때 사용한다.

### 2️⃣ 세마포어는 뮤텍스가 될 수 있지만, 뮤텍스는 세마포어가 될 수 없다.
- Mutex는 0, 1로 이루어진 이진 상태를 가지므로, Binary Semaphore이라고도 불린다.

### 3️⃣ 자원 소유에 차이가 있다.
- 뮤텍스는 자원 소유가 가능하고 책임을 갖는다. (상태가 0과 1뿐이므로 Lock 가질 수 있음) 
  - lock : 현재 임계구역에 들어갈 권한을 얻어옴 (만약 다른 쓰레드/프로세스가 임계구역 수행중이면, 종료할때까지 대기한다.)
  - unlock : 현재 임계구역을 모두 사용했음을 알림. (대기중인 다른 쓰레드/프로세스가 임계구역에 진입할 수 있음)
- Semaphor 는 자원을 소유하지 못한다.

### 4️⃣ 뮤텍스는 소유하고 있는 쓰레드만이 이 뮤텍스를 해제할 수 있다.
- 반면, semaphore는 semaphore를 소유하지 않는 쓰레드가 semaphore를 해제할 수 있다.

### 5️⃣ Semaphore는 시슽메 범위에 걸쳐 있고, 파일 시스템 상의 파일로 존재한다.
- 반면 뮤텍스는, 프로세스의 범위를 가지며, 프로세스가 종료될 때 자동으로 clean up 된다.

<br>
뮤텍스와 세마포어 둘다 데이터 무결성을 보장할 수 없으며 모든 교착 상태를 해결하지는 못한다는 한계점이 있다. 하지만 상호 배제를 위한 기본적인 기법이며, 여기에 조금 더 복잡한 매커니즘을 적용해 개선된 성능을 가질 수 있도록 하는것이 가장 중요한 프로그래밍 방식이 될 것이다.

<br>

# 📖 Reference 

- [github gyoogle](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Semaphore%20%26%20Mutex.md)
- [차근차근시작하는 GCD - 10](https://sujinnaljin.medium.com/ios-%EC%B0%A8%EA%B7%BC%EC%B0%A8%EA%B7%BC-%EC%8B%9C%EC%9E%91%ED%95%98%EB%8A%94-gcd-10-cb37c3e0cf13)
- [GCD 활용하기 2편](https://onelife2live.tistory.com/5)
- [Semaphore란? 차이는?](https://jwprogramming.tistory.com/13)
- [뮤텍스와 세마포어란?](https://chelseashin.tistory.com/40)
- [뮤텍스와 세마포어의 차이](https://worthpreading.tistory.com/90)

