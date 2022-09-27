// 2022.09.27 Noel🎸



# ❤️‍🔥 스트레티지 패턴(Strategy Pattern)<br/>

<br/>

### 🤔 전략 패턴(Strategy Pattern)이란?<br/>

> 전략 패턴은 **알고리즘의 집합(Algorithm Family)**을 사용하는 **행위 패턴<br/>**

- 여러 알고리즘을 각각 객체로 **캡슐화**하고, 동일한 목적을 하는 알고리즘을 하나의 인터페이스로 묶음<br/>

- 그럼 이 알고리즘들이 클라이언트 객체에서 교체되면서 사용 할 수 있음<br/>

- 따라서 알고리즘이 클라이언트 객체에 독립적으로 구성되기 때문에 **느슨한 연결(Decoupling)**이 됨<br/>

  - 느슨하게 연결되면 클라이언트 객체가 알고리즘이 변할때 영향을 받지 않는 것을 의미!<br/>

  ```
  예) 알고리즘 수정이 필요한 상황에서
  - 캡슐화된 해당 알고리즘만 수정하면 되고 내부적으로 어떻게 수정되고 어떻게 구현되었는지 클라이언트 객체는 알지못함
  ```

<br/>

<br/>

### 전략 패턴 구조<br/>

![image-20220927170937679](/Users/yuahyeon/Library/Application Support/typora-user-images/image-20220927170937679.png)

🔵 **Context (Composition)** <br/>

- `Concrete Strategy` 객체로 구성<br/>
- `Strategy` 객체에 대한 참조를 유지<br/>
- `Strategy`가 데이터에 접근 할 수 있는 인터페이스를 정의<br/>

<br/>

🔴 **Strategy (Compositor)** <br/>

- 지원되는 모든 알고리즘에 사용되는 공통적인 인터페이스를 정의<br/>
- `Context`는 `Strategy` 인터페이스를 사용하여 `Concrete Strategy`에 정의된 알고리즘을 호출<br/>

<br/>

**🔴 Concrete Strategy** <br/>

- `Strategy` 인터페이스를 사용하여 알고리즘을 구현<br/>

<br/>

<br/>

### 전략 패턴은 언제 사용할까?<br/>

전략패턴은 **어떤 상황에서 사용할 알고리즘이 여러 개 존재할 때** 사용하면 좋음

- 알고리즘을 런타임에서 바꿀 수 있기 때문에 이런 상황에서 효과적으로 대응할 수 있음

```예시
예시 상황

자동차의 경로만 알려주는 내비게이션 제작함 
> 그러다 사용자가 늘어 [도보로 이동하는 사람의 경로], [대중교통을 이동하는 사람의 경로]와 같이 다양한 알고리즘이 필요해짐 
> 이때❗️ 클래스 안에 계속해서 구현하다 보면, 하나의 변경으로 인해 많은 곳을 수정해야 하는 문제가 발생합

이를 해결하기 위해 전략 패턴을 사용
> [자동차의 경로], [도보로 이동하는 경로], [대중교통 경로]에 대한 알고리즘을 따로 구현하고 이들을 캡슐화
> 각각의 알고리즘을 서로에게 영향을 주지도 않고 각자 독립적으로 작동하도록 만들어줌으로써 위의 문제 해결가능!

출처: https://icksw.tistory.com/259 [PinguiOS:티스토리]
```

<br/>

<br/>

### 장단점<br/>

👍**장점**<br/>

- 런타임에서 객체 내부에서 사용되는 알고리즘을 변경할 수 있음<br/>
- `알고리즘을 사용하는 코드`와 `알고리즘을 구현하는 코드`를 분리 할 수 있음<br/>
- `Open / Closed Principle`(개방 폐쇄 원칙)을 준수 <br/>
  - `Context`를 변경하지 않고도 새로운 `Strategy`를 추가할 수 있음<br/>

<br/>

👎**단점**<br/>

- 알고리즘이 몇 개 없고 변경되는 일도 거의 없는 경우, 전략 패턴의 도입이 오히려 복잡성을 증가<br/>
- 클라이언트가 적절한 `Strategy`를 선택하기 위해서는 각각의 차이점을 알고 있어야 합니다.<br/>
- `Strategy`, `Context` 간 통신 오버헤드가 발생<br/>

<br/>

## 🕊 Swift 예제!<br/>

그럼 Swift로 한번 만들어 볼까요?<br/>

예제는 개발하는 훈이님 블로그 기반으로 작성되었습니다! <br/>(원문 : https://jeonyeohun.tistory.com/379)<br/>



![image-20220927212238480](/Users/yuahyeon/Library/Application Support/typora-user-images/image-20220927212238480.png)

어떤 문자열이 들어왔을때 조건을 검사해주는 `Validator` 객체가 있음<br/>

지금은 별 문제 없지만 나중에 추가적 요구사항이 생겨 요 객체에 알고리즘을 추가하게 되면<br/>

기존 객체에 변경사항이 생기기 때문에 `개방페쇄원칙(OCP)`에 어긋남!<br/>

<br/>

### ‼️ 따라서 전략패턴을 사용해야함!<br/>

![image-20220927213124669](/Users/yuahyeon/Library/Application Support/typora-user-images/image-20220927213124669.png) 전략패턴은 클라이언트 객체는 `Strategy(알고리즘 집합의 인터페이스)`를 가지고  필요에 따라 주입할 수 있음<br/>

또 새로운 요구사항인 아스키 코드를 검사하는 알고리즘을  `Strategy`에 추가함에 따라  `개방페쇄원칙(OCP)`을 지킬 수 있음<br/>

<br/>

#### 그럼 이제 Swift 코드로 구현해보자!<br/>

위의 예시 상황을 토대로 코드로 작성<br/>

<br/>

#### ① `Context` `Strategy`가 될 프로토콜 정의<br/>

```swift
//Strategy = 알고리즘의 인터페이스가 될 프로토콜
protocol Validatable {
    func validate(text: String) -> Bool
  // validate() : 인자로 문자열을 받으면 적절한 알고리즘 수행뒤에 Bool타입 반환
  // 전략에 맞는 알고리즘들은 이 프로토콜을 채택해 validate를 구현하면 됨
}
 
//Context = 클라이언트 객체 내부의 인터페이스를 제공할 프로토콜
protocol Validator {
    var validationStrategy: Validatable { get set }
  //검증에 사용할 알고리즘의 인터페이스를 가지게됨
    func validate(text: String) -> Bool
  // 실제로 사용자가 호출하고 결과를 반환하게될 메소드
}
```

 <br/>

#### ② Context (클라이언트 객체) 정의

- `StringValidator`의 `validate` 메서드
  - 알고리즘 없음
  - 대신 `Strategy(validationStrategy)`이 가진 알고리즘을 실행해 그 결과를 반환
  - 즉! 이것이 **알고리즘의 구현과 알고리즘을 사용하는 객체가 완전히 분리**된 것!!

```swift
// Context (클라이언트 객체) 정의
final class StringValidator: Validator {
    var validationStrategy: Validatable
    
    init(strategy: Validatable) {
        self.validationStrategy = strategy
    }
    
    func change(strategy: Validatable) {
        self.validationStrategy = strategy
    }
    // change 메서드를 통해 현재 알고리즘을 다른 알고리즘으로 변경 가능
  
    func validate(text: String) -> Bool {
        return validationStrategy.validate(text: text)
    }
  //검증 알고리즘을 수행
}
```

<br/>

#### ③ Concrete Strategy (알고리즘) 구현!<br/>

- `Strategy`을 채택하는 두개의 알고리즘 제작!<br/>

```swift
// 문자열이 숫자인지 확인하는 알고리즘
class NumberValidator: Validatable {
    func validate(text: String) -> Bool {
        return text.allSatisfy({ $0.isNumber })
    }
}
 
// 문자열의 길이가 10 미만인지 확인하는 알고리즘
class LengthValidator: Validatable {
    func validate(text: String) -> Bool {
        return text.count < 10
    }
}
```

<br/>

#### ④ Context (클라이언트 객체) 사용 및 변경<br/>

- 클라이언트 객체 사용 시 : 생성자를 통해 사용할 알고리즘을 선택<br/>
- 클라인언트에서 사용할 알고리즘 변경 : `change` 메서드를 통해<br/>

```swift
// Context 에서 사용할 알고리즘 선택
let validator = StringValidator(strategy: LengthValidator())
print(validator.validate(text: "12345678910")) // false
 
//Context 에서 사용할 알고리즘 변경
validator.change(strategy: NumberValidator())
print(validator.validate(text: "12345678910")) // true
```

<br/>

#### ➄ 새로운 Concrete Strategy (알고리즘) 추가<br/>

```swift
// 새로운 알고리즘 추가 : 문자열이 아스키 코드로 표현가능한지 확인하는 알고리즘
class AsciiValidator: Validatable {
    func validate(text: String) -> Bool {
        return text.allSatisfy({ $0.isASCII })
    }
}
```

```swift
// 클라이언트 객체에 적용
validator.change(strategy: AsciiValidator())
print(validator.validate(text: "12345678910")) // true
```

<br/>

<br/>

<HR/>

출처<br/>

 https://icksw.tistory.com/259 <br/>

https://jeonyeohun.tistory.com/379<br/>











