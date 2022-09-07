/ 2022.09.07

### 경쟁 상태란?

공유 자원에 대해 여러 프로세스(쓰레드)가 동시에 접근할 때, 결과값에 영향을 줄 수 있는 상태

경쟁 상태시 동시 접근 시 자료의 일관성을 해칠 수 있다는 문제가 발생함

### **WWDC에서 나온 Example**

아래 코드는 글로벌 쓰레드에서 어떤 배열에 요소를 추가하는 작업을 비동기적으로 처리하게 설정한 것이다.

Granpa와 Cub이라는 문자열을 sleepingBears에 넣는 작업.

<img width="856" alt="image" src="https://user-images.githubusercontent.com/103009135/188779625-77f9a139-863f-4b3b-8aa4-e063e1d0cbea.png">

<img width="832" alt="image" src="https://user-images.githubusercontent.com/103009135/188779581-3ba9975e-4d36-4fa7-a339-df3a2f70f4d1.png">


sleepingBears라는 배열에 접근하는데, 글로벌 쓰레드 두개가 경쟁하는 상황이다. 누가 이길지 모르니, 추가된 요소의 순서가 달라져 다른 배열이 되는 모습을 볼 수 있다.

이러면 참 골 때리는 상황이 연출되겟죠?? 

### **[#](https://gyoogle.dev/blog/computer-science/operating-system/Race%20Condition.html#race-condition%E1%84%8B%E1%85%B5-%E1%84%87%E1%85%A1%E1%86%AF%E1%84%89%E1%85%A2%E1%86%BC%E1%84%92%E1%85%A1%E1%84%82%E1%85%B3%E1%86%AB-%E1%84%80%E1%85%A7%E1%86%BC%E1%84%8B%E1%85%AE)Race Condition이 발생하는 경우**

1. **[#](https://gyoogle.dev/blog/computer-science/operating-system/Race%20Condition.html#%E1%84%8F%E1%85%A5%E1%84%82%E1%85%A5%E1%86%AF-%E1%84%8C%E1%85%A1%E1%86%A8%E1%84%8B%E1%85%A5%E1%86%B8%E1%84%8B%E1%85%B3%E1%86%AF-%E1%84%89%E1%85%AE%E1%84%92%E1%85%A2%E1%86%BC%E1%84%92%E1%85%A1%E1%84%82%E1%85%B3%E1%86%AB-%E1%84%8C%E1%85%AE%E1%86%BC%E1%84%8B%E1%85%A6-%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%90%E1%85%A5%E1%84%85%E1%85%A5%E1%86%B8%E1%84%90%E1%85%B3-%E1%84%87%E1%85%A1%E1%86%AF%E1%84%89%E1%85%A2%E1%86%BC)커널 작업을 수행하는 중에 인터럽트 발생**
    - 문제점 : 커널모드에서 데이터를 로드하여 작업을 수행하다가 인터럽트가 발생하여 같은 데이터를 조작하는 경우
    - 해결법 : 커널모드에서 작업을 수행하는 동안, 인터럽트를 disable 시켜 CPU 제어권을 가져가지 못하도록 한다.
2. **[#](https://gyoogle.dev/blog/computer-science/operating-system/Race%20Condition.html#%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%89%E1%85%A6%E1%84%89%E1%85%B3%E1%84%80%E1%85%A1-system-call-%E1%84%8B%E1%85%B3%E1%86%AF-%E1%84%92%E1%85%A1%E1%84%8B%E1%85%A7-%E1%84%8F%E1%85%A5%E1%84%82%E1%85%A5%E1%86%AF-%E1%84%86%E1%85%A9%E1%84%83%E1%85%B3%E1%84%85%E1%85%A9-%E1%84%8C%E1%85%B5%E1%86%AB%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%92%E1%85%A1%E1%84%8B%E1%85%A7-%E1%84%8C%E1%85%A1%E1%86%A8%E1%84%8B%E1%85%A5%E1%86%B8%E1%84%8B%E1%85%B3%E1%86%AF-%E1%84%89%E1%85%AE%E1%84%92%E1%85%A2%E1%86%BC%E1%84%92%E1%85%A1%E1%84%82%E1%85%B3%E1%86%AB-%E1%84%83%E1%85%A9%E1%84%8C%E1%85%AE%E1%86%BC-%E1%84%86%E1%85%AE%E1%86%AB%E1%84%86%E1%85%A2%E1%86%A8-%E1%84%80%E1%85%AD%E1%84%92%E1%85%AA%E1%86%AB%E1%84%8B%E1%85%B5-%E1%84%87%E1%85%A1%E1%86%AF%E1%84%89%E1%85%A2%E1%86%BC%E1%84%92%E1%85%A1%E1%86%AF-%E1%84%84%E1%85%A2)프로세스가 'System Call'을 하여 커널 모드로 진입하여 작업을 수행하는 도중 문맥 교환이 발생할 때**
    - 문제점 : 프로세스1이 커널모드에서 데이터를 조작하는 도중, 시간이 초과되어 CPU 제어권이 프로세스2로 넘어가 같은 데이터를 조작하는 경우 ( 프로세스2가 작업에 반영되지 않음 )
    - 해결법 : 프로세스가 커널모드에서 작업을 하는 경우 시간이 초과되어도 CPU 제어권이 다른 프로세스에게 넘어가지 않도록 함
3. **[#](https://gyoogle.dev/blog/computer-science/operating-system/Race%20Condition.html#%E1%84%86%E1%85%A5%E1%86%AF%E1%84%90%E1%85%B5-%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%89%E1%85%A6%E1%84%89%E1%85%A5-%E1%84%92%E1%85%AA%E1%86%AB%E1%84%80%E1%85%A7%E1%86%BC%E1%84%8B%E1%85%A6%E1%84%89%E1%85%A5-%E1%84%80%E1%85%A9%E1%86%BC%E1%84%8B%E1%85%B2-%E1%84%86%E1%85%A6%E1%84%86%E1%85%A9%E1%84%85%E1%85%B5-%E1%84%82%E1%85%A2%E1%84%8B%E1%85%B4-%E1%84%8F%E1%85%A5%E1%84%82%E1%85%A5%E1%86%AF-%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%E1%84%8B%E1%85%A6-%E1%84%8C%E1%85%A5%E1%86%B8%E1%84%80%E1%85%B3%E1%86%AB%E1%84%92%E1%85%A1%E1%86%AF-%E1%84%84%E1%85%A2)멀티 프로세서 환경에서 공유 메모리 내의 커널 데이터에 접근할 때**
    - 문제점 : 멀티 프로세서 환경에서 2개의 CPU가 동시에 커널 내부의 공유 데이터에 접근하여 조작하는 경우
    - 해결법 : 커널 내부에 있는 각 공유 데이터에 접근할 때마다, 그 데이터에 대한 lock/unlock을 하는 방법
    

## Additional Reference

[https://sujinnaljin.medium.com/ios-차근차근-시작하는-gcd-12-c06b599fe7f5](https://sujinnaljin.medium.com/ios-%EC%B0%A8%EA%B7%BC%EC%B0%A8%EA%B7%BC-%EC%8B%9C%EC%9E%91%ED%95%98%EB%8A%94-gcd-12-c06b599fe7f5) (경쟁 상태) 

[https://dev-workplace.tistory.com/10](https://dev-workplace.tistory.com/10) (디스패치 큐란?)

[https://developer.apple.com/documentation/dispatch/dispatchqueue](https://developer.apple.com/documentation/dispatch/dispatchqueue) (Apple Documentation)
