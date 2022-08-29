// 2022.08.28 Rookie

# block, non block / 동기, 비동기에 관한 개념을 정리함

## 3줄 요약

1. block, non block과 동기, 비동기 개념은 컴퓨터가 개발자가 작성한 코드를 수행하는 방식 중 하나이다. 그리고 둘은 엄연히 다른 개념이다!
2. 작업 수행을 요청받은 함수가 작업 실행 순서(제어권)를 바로 돌려준다면 non block, 작업이 끝날 때 까지 제어권을 돌려주지 않으면 block 이라고 한다.
3. 작업수행을 요청한 함수가 직접 작업 완료 여부를 체크한다면 동기, 그렇지 않다면 비동기이다. 따라서 비동기 함수는 요청을 받은 함수가 작업 완료 여부를 알려줘야하는데, 이 때 사용되는 것이 completion handler 같은 escaping closure 이다.

## blocking, non blocking

```
1. 블로킹(blocking) vs 논블로킹(non-blocking)우리가 어떤 프로그램을 만들었다고 해보자. 아마 어떤 코드를 작성해서 만들었을 것이고, 이 코드는 수많은 함수들이 순서대로 나열되어있는 모습일 것이다. 이렇게 한 프로그램은 여러개의 함수들로 이루어져 있다.어떤 함수 안에 여러개의 함수들이 있다고 가정해보자. 아마 이런 모습일 것이다. (설명의 편의를 위해 부모함수와 자식함수 A, B라고 부르도록 하겠다)
```

```
function 부모함수() {
  A();
  B();
  ...
}
```

- 제어권이란?
    
    ```
    제어권은 말 그대로 '권한'이다. A 함수의 내용이 아래와 같다고 했을 때, A에게제어권이 있어야 함수 안에 있는 작업들이 실행될 수 있다.결과값은우리가 보통 말하는 함수의 리턴값이다. 여기서 결과값은 3이 될 것이라고 쉽게 예상할 수 있다. 그런데 여기서 주의할 점이 하나 더 있다. 꼭 결과값은 3이 아니어도 된다는 것이다. 만약 A가 아직 계산을 끝마치지 못했는데, 갑자기 결과값을 요구한다면 '아직 계산못함'을 임시 결과값으로 내보낼 수도 있다
    
    example
    
    function A() {
      let a = 1;
      let b = 2;
      let sum = a + b;
      return sum;
    }
    ```
    

```
function 부모함수() {
  A();
  B();
  ...
}

function A() {
  let a = 1;
  let b = 2;
  let sum = a + b;
  return sum;
}
 

블로킹은다른 함수를 호출할 때, 제어권도 아예 함께 넘겨주고 작업이 끝난 후에 돌려받는 방식이다. 위의 예시에선 부모함수가 A를 실행시킬 때 제어권을 아예 넘겨주게 되어서, 본인은 다른 일을 하지 못하고 A의 작업이 끝날때까지 마냥 기다리는 것이다. 그러다 A의 작업이 끝나면 제어권을 돌려받고 다음함수인 B를 실행시킨다.논블로킹도 마찬가지로호출할 때 제어권을 넘겨주기는 하지만, 바로 돌려받는다. A의 작업이 안끝나도 바로 제어권을 돌려받고 부모함수는 B작업을 시작하는 것이다. 호출된 A는 알아서 실행되도록 놔둔다.

결론적으로 블로킹/논블로킹을 구분짓는 기준은 '요청받은 함수가 제어권을 언제 돌려주는지'이다.
```

## synchronous

```
동기(Sync)일단 '시간을 맞춘다'는 말은 무슨 뜻일까? 쉽게 말해 함수가 두 개 이상 존재할 때, 이함수들이 작업을 동시에 시작하거나, 끝나는 타이밍을 맞추거나, 하나가 끝나고 다른 하나를 차례로 실행하는 것을 시간을 맞춘다고 한다. 함수들끼리 어느정도 작업 시간에 대한 규칙(?)을 정해놓는 방식이라고 표현할 수 있을 것 같다.이런 규칙을 정하고 지킬 수 있는 이유는, 요청자가 요청한 일들이 완료되었는지를 계속 확인하기 때문이다. 요청하는 함수는 요청을 보내놓고, 요청을 처리하는 함수들이 작업을 마쳤는지 계속해서 물어본다. 요청자는 완료가 되었다는 응답을 받으면, 그때 다른 함수의 실행을 시작하거나 하는 것이다.

동기는 또 다른 관점에서는, 제어권과 결과값을 동시에 반환하는 것을 말하기도 한다. 아까 봤던 예시를 그림으로 표현한 것인데, 여기서 호출된 A는 작업을 마치고 자신을 호출한 부모함수에게 결과값(3)을 알려주면서, 동시에 제어권도 함께 돌려준다.

```
https://www.notion.so/d6429faca47a42cc9770e9aa1cd850fb#da2d96d132d84563b84a6106c5a1b559


## asynchronous

```
비동기(Async)비동기는 동기적이지 않은 방식을 말한다. 다시말해두 함수는 서로가 언제 시작하고, 언제 일을 마치는지 전혀 신경쓰지 않는 것이다. (개인플레이..) 이 경우에는 요청자는 작업을 요청해놓고 계속 완료되었는지 확인하는게 아니라, 알아서 알려주겠거니 하고 있는다. 다시말해요청을 받은 함수가 완료되었는지 여부를 알아서 알려주는 방식이다. 이렇게 작업을 시작하고 끝내는 시간을 아는 것은 호출된 함수 본인뿐이기 때문에, 여러 함수들이시작되고 끝나는 시간은 맞춰지지 않을 수 있게 된다.혹은결과값과 제어권이 다른 시점에 따로따로 반환되는 것도 비동기라고 할 수 있다.
```

```
블로킹 :요청받는 함수가 작업을 모두 마치고 나서야 요청자에게 제어권을 넘겨줌 (그동안 요청자는 아무것도 하지않고 기다림)논블로킹 :요청받은 함수가 요청자에게 제어권을 바로 넘겨줌 (그동안 요청자는 다른 일을 할 수 있음)
```

```
동기 :요청자가 요청받은 함수의 작업이 완료되었는지 계속 확인 (여러 함수들이 시간을 맞춰 실행됨)비동기 :요청자는 요청후 신경X, 요청받은 함수가 작업을 마치면 알려줌 (함수들의 작업 시작/종료 시간이 맞지 않을수도)
```

### But!

근데 솔직히 여기까지 읽으면 걍 이런거군..? 근데 어쩌란거지? 딱 이정도만 생각든다. 그러니 코드를 통해 알아보도록합시다!!! (아래 코드는 자체제작한거로 이상한게 있으면 말씀해주세요)

## Practices

### 블로킹, 동기 예시

특정 구문을 완료할 때 까지 제어권을 돌려주지 않으며, 작업을 요청한 함수가 직접 그 완료여부를 체크함

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4d441f2a-f5b6-4642-8163-106cd4eaa8da/Untitled.png)

func calculate(a:Int, b:Int ) → Int {

print(”계산을 시작합니다.”)

let multiplier = a + b // 이 구문이 caclulate 함수의 작업을 block함.
( 그 다음 작업에 result가 필요하기때문) 

let result = a * b * multiplier // calculate함수는 자신의 작업을 계속 수행하기 위해 위의 구문을 완료했는지 직접 체크를 해야한다.

print(”계산을 끝냅니다.”)

return result  // End

}

## 블로킹, 비동기 예시

특정 구문을 완료할 때 까지 제어권을 돌려주지 않지만 작업을 요청받은 함수가 끝나면 알려줌.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b28c9130-46d0-4432-809a-ffd86ee2c74e/Untitled.png)

func calculate(a:Int, b:Int ) → Int {

print(”계산을 시작합니다.”)

let finalResult = requestMultiplier( ) { response in 

let multiplier = response

print(”multiplier를 성공적으로 받아왔습니다.”)
let result = a * b * self.multiplier

print(”계산이 끝났습니다”)

return result

}  //  requestMultiplier 함수가 calculate 함수의 작업을 block함 

(requestMultiplier의 수행이 끝나기전까지 finalResult를 return할 수 없음)

return finalResult * 3

}

// calculate 함수와 requestMultiplier 함수는 작업을 비동기적으로 수행한다. 

// requestMultiplier은 작업이 끝났음을  response in 이하의 escaping closure 구문을 통해 알려준다)

## 논블로킹, 동기 예시

제어권을 바로 돌려주지만 작업을 요청한 함수가 직접 그 완료여부를 체크함

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/192a66ce-5681-4c97-90a6-923775a1b63f/Untitled.png)

func calculate(a:Int, b:Int ) → Int {

print(”하나 둘 셋”) // #1

print(”절사모”) // #2 - 1번 출력된거 맞지? 그럼 나 출력한다?

print(”화이팅!”) // #3 - 2번 출력된거 맞지? 그럼 나 출력한다?

return a+b // 너네 다 출력했지? 그럼 나 반환한다?

}

#1, 2, 3 프린트 함수문이 동기적으로(순차적) 진행되며, a+b 반환 결과에 아무런 영향도 미치지 않으니 calculate 함수의 작업을 block 하지도 않음. 

## 논블로킹, 비동기 예시

제어권을 바로 돌려주고 작업을 요청받은 함수가 끝나면 직접 알려줌.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1573656e-80f5-4c1e-afe8-9eaab4845bc7/Untitled.png)

func calculate(a:Int, b:Int ) → Int {

let multiplier = 1

print(”계산을 시작합니다.”)

while true {

requestMultiplier( ) {  result in 

let multiplier = result

print(”multiplier를 성공적으로 받아왔습니다.”)

} // 서버로부터 result를 가져오는 작업이 비동기적으로 이루어지지만 그 이후 calculate 함수 내의 코드가 그 결과를 반드시 필요하지 않으니 함수를 block하지는 않음. 그냥 다른 코드를 계속 수행함 

print(”서버로 부터 받아온 multiplier는 \(multiplier)이다”)

if multiplier < 6 {

break

}

}

print(”while문을 다시 수행합니다.”)

}

## More

iOS프로그래밍에서는 **동기는 Blocking의 개념**으로, 그리고 **비동기는 Non-Blocking의 개념**으로만 사용하고 있다는 찌라시가 있으나 공식적인 출처가 없음.

## Reference

[https://www.inflearn.com/questions/25632](https://www.inflearn.com/questions/25632) (iOS에서의 동기비동기, block non block)

[https://joooing.tistory.com/entry/동기비동기-블로킹논블로킹](https://joooing.tistory.com/entry/%EB%8F%99%EA%B8%B0%EB%B9%84%EB%8F%99%EA%B8%B0-%EB%B8%94%EB%A1%9C%ED%82%B9%EB%85%BC%EB%B8%94%EB%A1%9C%ED%82%B9) (동기 비동기 잘 정리한 글)

[https://sujinnaljin.medium.com/swift-async-await-concurrency-bd7bcf34e26f](https://sujinnaljin.medium.com/swift-async-await-concurrency-bd7bcf34e26f) (필독 !!! 동기 비동기 swift 문법)

[https://deveric.tistory.com/99](https://deveric.tistory.com/99)( 동기 비동기 예시)
