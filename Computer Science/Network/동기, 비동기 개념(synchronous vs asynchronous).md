// 2022.08.28 Rookie

# 동기, 비동기 관련 개념을 작성합니다 

# [Network] Synchronous/Asynchronous


<br>

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fda50Yz%2Fbtq0Dsje4ZV%2FlGe8H8nZgdBdgFvo7IczS0%2Fimg.png">

<br>

[homoefficio](http://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/)님 블로그에 나온 2대2 매트릭스로 잘 정리된 사진이다. 이 사진만 보고 모두 이해가 된다면, 차이점에 대해 잘 알고 있는 것이다.


## Synchronous/Asynchronous

동기/비동기는 일을 수행 중인 `동시성`에 주목하자

아까처럼 함수 A와 B라고 똑같이 생각했을 때, B의 수행 결과나 종료 상태를 A가 신경쓰고 있는 유무의 차이라고 생각하면 된다.

- **Synchronous** : 함수 A는 함수 B가 일을 하는 중에 기다리면서, 현재 상태가 어떤지 계속 체크한다. 
- **Asynchronous** : 함수 B의 수행 상태를 B 혼자 직접 신경쓰면서 처리한다. (Callback)

즉, 호출된 함수(B)를 호출한 함수(A)가 신경쓰는지, 호출된 함수(B) 스스로 신경쓰는지를 동기/비동기라고 생각하면 된다.

비동기는 호출시 Callback을 전달하여 작업의 완료 여부를 호출한 함수에게 답하게 된다. (Callback이 오기 전까지 호출한 함수는 신경쓰지 않고 다른 일을 할 수 있음)

<br>

<br>

위 그림처럼 총 4가지의 경우가 나올 수 있다. 이걸 좀 더 이해하기 쉽게 Case 별로 예시를 통해 보면서 이해하고 넘어가보자

<br>

```
상황 : 치킨집에 직접 치킨을 사러감
```

<br>

### 1) Blocking & Synchronous

```
나 : 사장님 치킨 한마리만 포장해주세요
사장님 : 네 금방되니까 잠시만요!
나 : 넹
-- 사장님 치킨 튀기는 중--
나 : (아 언제 되지?..궁금한데 그냥 멀뚱히 서서 치킨 튀기는거 보면서 기다림)
```

<br>

### 2) Blocking & Asynchronous

```
나 : 사장님 치킨 한마리만 포장해주세요
사장님 : 네 금방되니까 잠시만요!
나 : 앗 넹
-- 사장님 치킨 튀기는 중--
나 : (언제 되는지 안 궁금함, 잠시만이래서 다 될때까지 서서 붙잡힌 상황)
```

<br>

### 3) Non-blocking & Synchronous

```
나 : 사장님 치킨 한마리만 포장해주세요
사장님 : 네~ 주문 밀려서 시간 좀 걸리니까 볼일 보시다 오세요
나 : 넹
-- 사장님 치킨 튀기는 중--
(5분뒤) 나 : 제꺼 나왔나요?
사장님 : 아직이요
(10분뒤) 나 : 제꺼 나왔나요?
사장님 : 아직이요ㅠ
(15분뒤) 나 : 제꺼 나왔나요?
사장님 : 아직이요ㅠㅠ
```

<br>

### 4) Non-blocking & Asynchronous

```
나 : 사장님 치킨 한마리만 포장해주세요
사장님 : 네~ 주문 밀려서 시간 좀 걸리니까 볼일 보시다 오세요
나 : 넹
-- 사장님 치킨 튀기는 중--
나 : (앉아서 다른 일 하는 중)
...
사장님 : 치킨 나왔습니다
나 : 잘먹겠습니다~
```

<br>

#### [참고 사항]

- [링크](http://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/)
- [링크](https://musma.github.io/2019/04/17/blocking-and-synchronous.html)
