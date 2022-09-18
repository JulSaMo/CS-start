// 20220918 Brown
<br>

# 🟠 객체 (Object)

CS에서 객체는 물리적으로 존재하거나 추상적으로 생각할 수 있는 것 중에서 자신의 속성을 가지고 있고 다른것과 식별 가능한 것을 말한다.
컴퓨터를 예로들면, '키보드, 마우스, 스피커 등'이 객체가 될 수 있고, 이것들은 각각 '입력, 소리출력, 인터페이스 조작 등'의 기능을 포함한다.

# 🟠 객체지향 프로그래밍 (OOP, Object Oriented Programming)

```
객체들의 상호작용으로 서술하는 프로그래밍 기법
현실세계의 객체를 소프트웨어의 객체로 설계하는 것 (현실객체의 속서오가 동작을 추려내서 소프트웨어의 객체의 필드와 메서드로 정의 하는 과정)
```

즉, 코드로 객체를 만들고, 그 객체를 사용하는 프로그래밍 방법이다. 프로그램을 그저 데이터와 처리방법으로 나누는 것이 아닌, 프로그램을 다수의 '객체'로 만들어놓고, 객체들끼리 서로 상호작용을 통해서 하나의 프로그램을 만들어지는 방식이다.

가장 쉽게 컴퓨터로 예를 들면, 컴퓨터 한대는 'CPU, RAM, BOARD, SSD,,,' 여러가지의 부품들로 구성되고, 각 부품들이 각각의 기능을 담당하여 상호작용읕 통해 컴퓨터가 동작하게 된다. 이것처럼, 부품들은 ```객체```라고 생각하면 된다.


# 🟠 객체지향 프로그래밍의 4가지 특성 (✨중요!)

## 1️⃣ 추상화

```
객체의 공통적인 속성과 기능을 추출하여 정의하는 것
```
- 즉, 현실세계의 사물을 객체로 보고, 필요한 공통특성만 다루어 현실의 복잡성을 제거하고 목적에 집중할 수 있도록 한다.
- 예를들어 토끼, 강아지, 사자라는 객체들을 ```하나읙 공통된 특징을 바탕으로``` 포유류 로 추상화 할 수 있다.


## 2️⃣ 캡슐화

<p align="center"><img width="500" alt="image" src="https://user-images.githubusercontent.com/96969693/190886447-32bec2ab-583f-49c8-979b-493c83793680.png"></p>

```
- 객체 수행 목적에 따라 데이터 구조 및 처리 방법을 결합시켜 묶어서, 외부에 내부 기능 구현 내용을 감추고 이용방법만 알려줌.
- 외부객체는 내부객체의 구조를 알지 못하고, 객체가 노출해서 제공하는 필드와 메서드만 이용할 수 있음.
```

### 📝 이렇게 왜 외부객체가 알지 못하게 캡슐화를 하는건가요?

캡슐화는 관련있는 변수와 함수를 하나의 클래스로 묶고 외부에서 접근하지 못하도록 ```은닉```하는게 핵심이다. 객체에 직접적인 접근을 막고 외부에서 내부의 정보에 직접 접근하거나 변경할 수 없고, 객체가 접근하는 필드와 메서드를 통해서만 접근이 가능하다.

<p align="center"><img width="598" alt="image" src="https://user-images.githubusercontent.com/96969693/190886520-914758fb-f6d8-409e-928a-c427f28288b0.png"></p>

왜 이렇게 하냐면, 바로 캡슐화를 하면 ```은닉화```특징의 장점을 갖기 때문이다.

### ```은닉화의 장점```

- 외부에서 특정 객체의 데이터 및 함수의 직접접근을 막음으로써 변경을 못하게 하여, 유지보수나 확장시 오류의 범위를 최소화할 수 있다.
(객체 내 정보 손상, 오용을 방지하고, 조작법이 바뀌어도 사용방법 자체는 바뀌지 않아서 오류의 범위를 최소화한다는 것이다.)
- 데이터가 변경되어도 다른 객체에 영향을 주지 않는, 독립성을 갖는다.
- 처리된 결과를 사용하므로, 이식성이 좋고 객체를 모듈화 할 수 있어서 새로운 시스템의 구성에 하나의 모듈처럼 사용이 가능하다.


<p align="center"><img width="564" alt="image" src="https://user-images.githubusercontent.com/96969693/190886596-53fe59c2-61a0-4168-9731-c86910a7a45c.png"></p>


캡슐화를 위해서는 접근제어자를 통해 설계가 잘 이루어져야 한다. 자신 내부의 모듈을 감추고 다른 모듈 내부 작업도 직저적으로 개입하지 못하게 하도록 설계해야한다. (ex. public, private, getter, setter 등과 같은 접근제어자가 존재하는 이유이기도 하다.)\
 
 
## 3️⃣ 상속 (Interitance)
 
```
상위개념의 특징을 하위 개념이 물려받아 사용하는 것
```

### 📝 상속은 왜 해야하나요?

- 재사용읋 인해서 코드의 길이를 줄이고, 가독성을 높인다.
- 상속은 코드의 재사용 관점이 아닌, 기능의 확장개념으로 생각해야한다. (상위 클래스에 있는 기능을 그대로 상속받는다고!)


## 4️⃣ 다형성 (Polymorphism) (✨중요, 물어보는 면접 좀 많앗음!)

```
상속과 연관있는 개념으로, 한 객체가 다른 여러형태(객체)로 재구성되는 것
```
즉, 한 부모 밑에서 상속받는 자식들이 모두 똑같지는 않다라는 개념이다.

오버로드와 오버라이드가 다형성의 대표적인 예시이다. 오버로드와 오버라이딩 처럼, 자식클래스가  다양한 형태로 존재할 수 있게 하는 특징이 바로 다형성이다.

<p align="center"><img width="536" alt="image" src="https://user-images.githubusercontent.com/96969693/190886881-36155aeb-86f2-4e7f-9b9b-3dc5aa4a5a88.png"></p>

### 📝 오버라이드와 오버로드가 뭔가요? 차이점을 알아두자!

오버라이드, 오버로드를 적용한 프로그래밍 방식을 각각 오버라이딩, 오버로딩 이라고 한다.

### ✏️ 오버라이딩 (Overriding) (Swift 기준!)

```
서브클래스는 슈퍼클래스에서 상속할 메서드, 프로퍼티, 서브스크립트를 서브클래스에서 원하는대로 구현(재정의)할 수 있는데, 이것을 오버라이딩 이라고 함.
```
(⚠️ swift에서의 오버라이딩은 제약조건이 조금 존재함. 프로퍼티의 경우 저장속성만 추가할 수 있고, 이름과 타입은 반드시 명시해야하고, final을 붙이면 더 이상 상속이 불가능하거나 오버라이딩이 불가능하다.. 등 다양한 제한 조건이 있는데 나중에 더 알아보자.)

```swift
class Human {
    func description {
        print("나는 사람")
    {
}

class Teacher: Human { }
```

위에서 ```Teacher```이란 클래스가 Human이라는 클래스를 상속받았기 때문에 아래처럼 description이란 메서드에 접근이 가능하다.

```swift
let brown: Teacher = .init()
brown.description()  // Human의 func에 접근 가능!
```

이렇게 그냥 접근하게 되면, 부모클래스의 ```Human```에 그대로 접근가능한건데, ```override```를 사용하면 함수를 '재정의'할 수 있다.

```swift
class Teacher: Human {
    override func description() {
        print("나는 보라온!")
    }
}

let brown: Teacher = .init()
brown.description()
// 나는 보라온! 이라고 출력된다.
```

이렇게 한다면, 재정의된 Teacher에 접근한 프로퍼티들은 모두 override 된 함수가 실행된다! 이것이 바로 오버라이딩에 대한 개념이다.


### ✏️ 오버로딩 (Overloading) (Swift 기준!)

함수의 이름은 같으나, 매개변수, 리턴타입 등으로 다르게 설정하여 함수를 중복으로 선언할 수 있다는 개념이다. Swift는 오버로딩을 허용하고, 함수, 서브스크립트, 생성자에서 사용할 수 있다.

이 개념은, 객체지향 프로그래밍에서 쓰이는 개념이라고 잘 알아두자!

```swift
func sum() { }
func sum() { }
```
이렇게 하게 되면, ```Invalid redclaration of "sum()"``` 이라는 에러가 뜨게된다. 함수가 재선언됐다는 에러이다.
Swift는 오버로딩을 지원하기 때문에, 아래와 같이 파라미터나 리턴값을 다르게 하여 함수를 재정의하면 에러가 나지 않는다.

```swift
func sum() { }
func sum(_a: Int, _ b: Int) { }
func sum() -> Int { return 0 }
```

이렇게 세 함수는 ```sum()```이라는 이름은 같지만 각각 갖고 있는 매개변수, 리턴값이 다르기 때문에 재선언됐다는 에러가 나지 않는다. 이는 오버로딩 개념을 지원하는 특성 때문이다.

즉, 함수를 식별할 때 함수 이름 뿐만 아니라, 함수 이름, 파라미터(타입, 개수, argument label), 리턴타입 모두를 고려해서 함수를 식별한다고 알 수 있다.
오버로딩의 장점은, 타입이나 리턴값이 다르지만, 동일한 기능을 하는 함수를 하나로 만들 수 있다는 것이다.

```swift
// ❌ 오버로딩을 지원하지 않는다면
func sumString(_ a: String, _ b: String) -> String {
    return a + b
}

func sumInt(_ a: Int, _ b: Int) -> Int {
    return a + b
}

sumInt(1, 2)
sumString("ABC","DEF")

// ✅ 오버로딩을 지원하는 경우
func sum(_ a: Stirng, _ b: String) -> String {
    return a + b
}

func sum(_ a: Int, _ b: Int) -> Int {
    return a + b
}

sum(1,2)
sum("ABC","DEF")
```

위 두개의 함수는 모두 sum 기능을 한다. 하지만 오버로딩을 지원하지 않는 경우에는 ```sumString``` ```sumInt```로 따로 구분해서 타입별로 함수를 작성해주어야한다. 하지만, 오버로딩이 가능하다면, 아래의 경우처럼 ```sum``` 하나의 함수이름으로 접근이 가능하다. (결국 다른함수긴 하지만, 코드를 작성하는 입장에서는 매우 편리하고, 가독성 또한 좋아진다.)

## 🔸 OOP의 장점

- 재사용성: 상속을 통해 코드의 재사용성을 높일 수 있다.
- 생산성 향상: 잘 설계된 클래스를 만들어서 독립적인 객체를 사용함으로써 개발의 생산성을 향상시킬 수 있다.
- 자연적인 모델링: 일상생활에서 모습의 구조가 객체에 자연스럽게 녹아들었기 때문에 생각하고 있는 것을 그대로 자연스럽게 구현할 수 있다. (기능별로 나눠서 구현한다거나,,)
- 유지보수의 우수성: 기존 기능을 수정 시 함수를 새롭게 바꾸더라도 캡슐화 되어 그 함수의 세부 정보가 은닉되어 있기 때문에 주변에 미치는 영향을 최소화 하기 때문에 유지보수의 우수성을 갖는다. 새로운 객체의 종류를 추가 시에는 상속을 통해서 기존의 기능을 활용하고, 존재하지 않은 새로운 속성만 추가하면 되므로 매우 경제적이다.

## 🔸 OOP의 단점

- 많은 오버헤드가 발생한다. (객체간의 정보교환이 모두 메시지 교환을 통해서 일어나기 때문이다.)

```
오버헤드란, 어떤 처리를 하기 위해서 소모되는 간접적인 처리 시간, 메모리를 의미한다.
```

- 상태를 가지는 객체로 인한 버그 발생 가능성이 존재함: 내부 변수로 인해 객체가 예측할 수 없는 상태를 갖게 되기 때문이다.

# 🟠 OOP의 5대 원칙 ```SOLID```와 SWIFT

## 🔸 스위프트는 객체지향? 함수지향? 무슨 패러다임 언어임??

스위프트의 대표적인 특징은 아래와 같다.

```bash
- ARC (Automatic Reference Counting, 자동 참조 카운팅) 지원
- Objective-C의 동적 객체 모델과 매개변수 형식 도입
- 컴파일 언어
```

그리고, Swift는 ```다중 패러다임 언어```이다. 스위프트는 다음과 같은 프로그래밍 패러다임을 차용해서 만들어졌다.

```bash
- 명령형 프로그래밍 패러다임
- 객체지향 프로그래밍 패러다임
- 함수형 프로그래밍 패러다임
- 프로토콜 프로그래밍 패러다임
```

정확하게는, 명령형과 객체지향을 기반으로, 함수형, 프로토콜 프로그래밍 패러다임을 지향한다. (진짜 짬뽕이잖아?🍜)

- 애플의 프레임워크 대부분은 객체지향 프로그래밍 패러다임을 기반으로 설계된 수많은 클래스로 구성되어있음.
- 애플의 프레임워크에서 사용될 언어라면, 객체지향 프로그래밍 패러다임을 수용해야만 할 것이다.
- 또, 스위프트는 함수형 프로그래밍 패러다임을 강조한다. 애플 프레임워크를 벗어나 다른 영역에서 스위프트를 사용했을 때, 순수하게 함수형 프로그래밍 패러다임으로 프로그램을 작성할 수 있기 때문이다.)

따라서 스위프트는, 함수형과 객체지향 둘다 차용하고 있으므로, 두개의 패러다임을 잘 섞어서 코딩을 한다면, 필요한 기능에 맞게 최적의 성능을 발휘하고, 생산성도 극대화 할 수 있을 듯?!

## 🔸 스위프트와 SOLID ✨

### 📝 SOLID란

```bash
- 로버트 마틴이라는 사람이 명명한 객체지향 프로그램 및 설계의 기본 원칙 다섯가지 S, O, L, I, D
```
SOLID 각각의 알파벳이 뭘 의미하는지는 아래서 설명하겠다.

## 📝 스위프트와 SOLID

swift는 위에서 배웠듯, 멀티패러다임 언어이다. 하지만, 애플의 대부분의 프레임워크는 객체지향 프로그래밍 패러다임을 기반으로 설계된 수많은 클래스로 구성되있다고 했잖슴? 

스위프트에서 지원하는 Foudnation, UIKit, 코코아 터치 등 이러한 프레임워크들은 기본적으로 OOP에 근간을 두고 있다고 한다. SOLID의 원칙들과 iOS를 연관지어 살펴보고, 왜 많은 클래스들이 그런식으로 만들어졌는지 알아보자.

동시에 스위프트는 OOP에 근간을 두고 있지만 SOLID원칙을 위반하는 경우도 있다고 하는데 이 예시들을 살펴보고, 잘못된 코드란 무엇인지 알아보자!

## 1. SRP (Single Responsibility Principle): 단일 책임 원칙

```
클래스는 단 하나의 책임을 가져야 하며, 클래스를 변경하려는 이유는 단 하나여야한다는 원칙
```

- 변화에 대한 유연성 확보하기 위해서 이 원칙을 지켜야 함.
- 낮은 결합도, 높은 응집도를 추구하기 위해서 이 원칙을 지켜야 함.

### 👉 스위프트에서 SRP를 위반한 예시

가장 대표적인 위반 사례는 MVC 패턴이 가진 문제 Massive View 현상이다.

```
💡 Massive View 란? 
MVC의 flow는 Model -> Controller -> View 가 되어야 하는데, 이 flow가 아닌,
View가 Model과 Controller의 도움 없이 모든 것을 다 해내는 케이스, 이를 바로 Massive View 현상이라고 한다.
```

MVC패턴의 단점을 극복하기 위해서 여러 다른 패턴들이 생겨나고 시도되고 있다. 새롭게 시도되는 패턴들은 너무 많은 역할을 하고 있는 VC를 쪼개서 단일 책임만을 가지는 여러 클래스를 만들려고 한다는 점이 공통점이다. 이렇게 새롭게 시도되는 패턴들의 경우 SRP를 위반하지 않았다고 할 수 있다. (단일 책임을 갖도록 분리하는 것이므로!)

#### 🤔 SRP를 지키기 위해서는 어떻게 해야할까 (feat. swift)

```
- 가장 쉬운 방법은, 클래스를 작게 만드는 것
```

'함수는 10줄', '클래스는 100~200줄'로 제한사항을 두고 프로그래밍을 해보면 좋다. 클래스와 함수를 작게 만드는 것이 무조건적인 SRP를 충족시키기 위한 충분조건은 아니지만, 필요조건이라고 할 수 있다. 

함수 10줄 룰을 지키기 위해서는, 함수가 짧아야 하므로, 하나의 역할을 가진 함수가 될 수 밖에 없고, '추상화 레벨'에 대해서 고민할 수 밖에 없다. 추상화 레벨이란, 얼만큼의 정보를 해당 함수에서 노출해서 보여줄 것인가 하는 것이다.

```
- 추상화 레벨에 대한 예시
  - 라면 조리법을 살펴보자.
  - 물 550ml를 끓인다 -> 면과 스프, 후레이크를 넣는다 -> 4분 30초르 끓인다.
  - 물 끓이는 단계를 더 쪼개보면, 냄비를 꺼낸다, 정수기로 물을 받는다, 물을 담는다,,, 등 여러 동작이 있다. 하지만 이를 조리법에 포함시키지는 않았다.
  - "물 550ml를 끓인다"에 모든 내용을 묶어서 표현 (이것이 함수)했기 때문이다.
```

위 라면의 예시처럼, 작업(함수)를 어느 수준까지 쪼개서 설명(추상화)할 건지 지속적으로 고민하게 되므로, 함수를 짧게 만드는 것은 SRP의 필요조건이다.

클래스 200줄 룰을 지키기 위해서는, 프로퍼티나 함수, 메서드를 그냥 아무데나 만들어서 쓸수 없다. 꼭 이 프로퍼티가 필요한지, 함수가 필요한지 등에 대한 고민이 지속적으로 필요하다. 해당 클래스에 있을 이유가 없는데 존재하게 된다면, SRP 위반이다. 또한, 함수 내부에서 self의 호출 빈도가 적을 수록 클래스와 연관성이 작다는 뜻이므로, 나중에 클래스를 리팩토링 시켜야할 상황이 오면 우선적으로 내쫓을 후보가 된다!


## 2. OCP (Open-Closed Principle): 개방-폐쇄 원칙

```
- 모듈은 확장에는 열려있어야 하고, 변경에는 닫혀있어야 한다.
- 기능을 변경 또는 확장할 수 있으면서, 그 기능을 사용하는 코드는 수정하지 않아야한다.

🤔 열려있고 닫혀있는게 뭔데?
- 열려있다?: 기능 추가나 변경을 할 수 있어야 한다는 뜻
- 닫혀있다?: 기능 추가를 할 때 그 모듈을 스고 있는 코드들은 수정하지 않아야한다는 뜻 
```

### 👉 스위프트에서 OCP를 위반한 예시

```어떤 타입에 대한 반복적인 분기문```이 OCP를 위반한 대표적인 예시이다.

- 즉, 하나의 enum에 여러 군데에서 반복적으로 if/switch문을 쓰고 있다면 고민을 해봐야할 필요가 있다.
- 왜냐하면, 이런 경우 기능 추가는 case문으로 추가하면되어 간편하지만, 이렇게 추가하는 순간 해당 enum을 스위칭하고 있는 모든 코드를 찾아서 수정해주어야한다는 치명적인 단점이 존재한다. (OCP 위반!!)


#### 🤔 OCP원칙을 지키기 위해서는 어떻게 해야할까 (feat. swift)

최대한 if/switch문을 안쓰는 연습을 하는 것이다. 분기문을 모두 없애는 것은 불가능하니까, enum 같이 타입을 분기하는 지점에 대해서 분기처리를 안하는 것을 연습해보면 된다. 그리고 어느정도 SRP를 지키기위해서 노력했던, 함수 100줄, 클래스 200줄 룰을 적용시키면, 어느정도 자연스럽게 OCP원칙을 고려하게 된다. 왜냐면 분기처리를 하는 것은 많은 코드라인을 차지하기 때문이다!

### if/switch를 대체할 수 있는 두가지 방법이 있다.

### 1. protocol 사용하기
프로토콜을 상속받아서 쓰는 방벙이다. 이는 직접적으로 OCP를 지키는 구조이다.

```swift
// ❌ enum을 이용한 분기처리
enum Animal {
    
    enum Size {
        case small
        case medium
        case large
    }
    
    case dog
    case cat
    case cow
    
    var noise: String {
        switch self {
        case .dog:
            return "woof"
        case .cat:
            return "meow"
        case .cow:
            return "moo"
        }
    }
    
    var size: Size {
        switch self {
        case .dog:
            return .medium
        case .cat:
            return .small
        case .cow:
            return .large
        }
    }
    
}

// ✅ 프로토콜로 분기문 대체해보기

enum AnimalSize {
    case small
    case medium
    case large
}

protocol Animal {
    var noise: String { get }
    var size: AnimalSize { get }
}

struct Dog: Animal {
    var noise = "woof"
    var size = AnimalSize.medium
}

struct Cat: Animal {
    var noise = "meow"
    var size = AnimalSize.small
}

struct Cow: Animal {
    var noise = "moo"
    var size = AnimalSize.large
}
```

프로토콜로 작성된 코드를 보자. 여기서 이제 새로운 유형을 추가하려면 어떻게 해야하는가? 그냥 밑에다가 Animal 프로토콜을 준수하는 새로운 Struct를 추가해주면된다. 무언가 새롭게 추가되었다고 코드가 수정되거나 하는 일이 발생하지 않는다. 즉, OCP원칙을 제대로!제대로! 지키는 방식이다.

```swift
// ✅ 새로운 유형 추가하기 -> 다른 어떠한 코드에도 영향을 주지 않음 (OCP 준수)
struct Fox: Animal {
    var noise = "wa-pa-pa-pa-pa-pa-pow"
    var size = AnimalSize.medium
}
```

실제로, 이렇게 굳이 분기처리를 하지 않아도 되는 코드를 protocol로 바꾸는 리팩토링 기술을, ['조건부를 다형성으로 바꾼다.'](https://sourcemaking.com/refactoring/replace-conditional-with-polymorphism)라고 말한다고 한다. 조건의 분기와 일치하는 하위 클래스를 만들어서, 객체 클래스에 따라 다형성을 통해 적절한 구현이 달라지게 하는 방식이라고 한다. 다형성은 위에서 배웠듯, 하위자식들이 모두 같은 자식은 아니다 라는 개념으로 배웠다. 자식들이 모두 다르다? 서브 클래스에서 각자의 구체적인 계산 로직을 정의하는 방식으로 조건부를 다형성으로 바꾼다 라고 말하는 것이다.

어쨋든, 이렇게 다형성으로 바꾸게되면, 깔끔한 코드를 만들 수 있다. 이렇게 바꿀 수 있는 스위프트 언어는 ```'프로토콜 지향 프로르래밍'```이라고 부르기도 한다. ✨

### 2. dictionary 자료형 사용하기
이는 직접적으로 ocp 를 지키는 구조는 아니다.
어차피 default 절이 있는 switch문과 동일한 약점을 갖는다. 
때문에 case 가 자주 변경될 것 같을때는 피해야하고, 분기문을 없애고 싶을 때만 제한적으로 사용해보자.

```swift
// ❌ switch 문으로 분기처리한 코드
switch reason {
  case .initializing:
    self.instructionMessage = "Move your phone".localized
  case .excessiveMotion:
    self.instructionMessage = "Slow down".localized
  case .insufficientFeatures:
    self.instructionMessage = "Keep moving your phone".localized
  case .relocalizing:
    self.instructionMessage = "Move your phone".localized
}

// ✅ dictionary를 이용하여 분기처리를 없앤 코드
let trackingStateMessages: [TrackingState.Reason : String] 
                         = [.initializing.        : "Move your phone".localized,
                            .excessiveMotion      : "Slow down".localized,
                            .insufficientFeatures : "Keep moving your phone".localized,
                            .relocalizing         : "Move your phone".localized]
//switch문 대체
self.instructionMessage = trackingStateMessages[reason]

```

## 3. LSP (Liskov Substitution Principle): 리스코프 치환 원칙

```
상위 타입 객체를 하위 타입의 객체로 치환해도 상위 타입을 사용하는 프로그램은 정상적으로 동작해야한다는 원칙
```

- B가 A의 자식타입이면, 부모 타입인 A객체는 자식타입인 B로 치환해도, 작동에 문제가 없어야한다.
- 부모클래스 타입인 A를 사용하는 기존의 프로그램 코드가 자식 클래스 B로 대입시켰을 때도 문제없이 작동하게 만들기 위해서, 자식 클래스는 부모 클래스가 따르던 제약사항을 모두 따라야한다.
- 즉, 자식이 부모의 동작을 방해해서는 안된다라는 의미이다.


### 👉 스위프트에서 LSP를 위반한 예시

직사각형을 상속받아서 만든 정사각형 클래스를 생각해보자.
정사각형은 너비와 높이가 같아야하기 때문에 너비와 높이를 자유롭게 바꿀 수 있는 직사각형 부모 클래스의 동작을 제한해야만 원하는 동작을 할 수 있다.
이런 경우가 LSP 위반이다.

#### 🤔 LSP원칙을 지키기 위해서는 어떻게 해야할까 (feat. swift)

LSP를 지키기 위해서는, 직사각형이 정사각형을 상속받거나, 너비와 높이를 아예 ```let```으로 만들어버리면 된다. ```let```으로 선언하면 되는 이유는, 값을 바꾸는 동작을 아예 없애버리면 제한할 동작이 없기 때문이다. (let은 항상 고정값이라는 특성을 이용한 것)

### 예시 1. 

```swift
var label = UILabel(frame: .zero)
var button = UIButton(frame: .zero)
var segmentedControl = UISegmentedControl(frame: .zero)
var textField = UITextField(frame: .zero)
var slider = UISlider(frame: .zero)
var switchButton = UISwitch(frame: .zero)
var activityIndicator = UIActivityIndicatorView(frame: .zero)
var progressView = UIProgressView(frame: .zero)
var stepper = UIStepper(frame: .zero)
var imageView = UIImageView(frame: .zero)

let views: [UIView] = [...] //위 뷰들을 UIView 어레이에 저장

views.forEach { $0.frame.size.height = 30 } //뷰들의 height를 30으로 변경

let height = views.reduce(0) { $0 + $1.frame.height } // 높이들을 전부 더해주자
print(height) //과연 결과는?
```

- 10개의 UIView의 높이를 30으로 바꿧으니까, 높이를 전부 합치면 300이 될 것이라고 예상할 수 있다.
- 실제 결과는 272 이다. 이유는???
- 일부 뷰들은 intrinsicSize를 마음대로 바꿀 수 없게 되어있기 때문이다. 이렇게 UIView(부모)의 동작(높이를 바꾸는것)을 제한하는 일부 뷰들 (UIProgressView, UISwitch)이 바로 LSP 위반이다. (하위 뷰들의 제한사항 때문에 views(부모)의 동작이 제대로 작동하지 않앗으므로)

### 예시 2.

또한 UIKit으로 개발하다보면, 아래와 같은 함수를 볼 수 가 있다.

```swift
required init?(coder aDecoder: NSCoder) {
    fatalError("init(coder:) has not been implemented")
}
```

이처럼 부모의 함수를 오버라이드 해서 퇴화시켜버리는 함수는 LSP 위반이다.

#### 🤔 그럼 LSP 는 어떻게 지키려고 노력해야할까?

사실 스위프트에서는 LSP를 절대 어기지 않고 하는 것은 어려운 일이다. 하지만 너무 많은 곳에서 LSP위반을 해버리면, 문제가 생긴다.
상위 클래스를 기준으로 코딩할 수 없어지는데, 이렇게 되면  상속 자체의 의미가 없어지며, OCP조차 지킬 수 없게 된다.

예를들어 UITableView는 UITableViewCell을 기준으로 만들어져 있기 때문에 우리가 만든 커스템 셀이 LSP를 지키지 않는다면 테이블 뷰도 제대로 작동하지 않을 것이다. 또한 protocol을 만드는 이유도 추상화된 인터페이스를 기준으로 코드를 작성하기 위해서인데, 상속받은 타입이 protocol의 메서드를 퇴화시킨다면 프로토콜을 기준으로 코드들이 줄줄이 망가질 수 있다.
이처럼 상속은 객체지향 프로그래밍에서 중요한 부분이고, 잘 쓰면 유용하지만, 상속을 잘못만들면 문제가 발생할 수 있다.

반면 때에 따라서는 LSP를 위반함으로써 편리함과 단순함을 얻게 될 수도 있다. 결론적으로, LSP를 모든 곳에서 지키려고만 하면 비효율적이고 너무 자주 위반하면 예상하지 못한 결과들 때문에 안정성을 해치게 된다. 그러므로 상속을 만들때는 LSP 위반인지 아닌지를 숙지하고 사용하는 것이 좋겠다.

## 4. ISP (Interface Segregation Principle): 인터페이스 분리 원칙

- 어떤 클래스를 인터페이스를 구현할 때, 사용하지 않는 메서드를 가지고 있는 인터페이스에 의존하게 하지 않아야 한다. 
- 클래스가 사용하는 기능만 제공하도록 인터페이스를 분리해야한다.
- 즉, 클라이언트는 자신이 사용하지 않는 메소드에 의존관계를 맺으면 안된다는 뜻이다.
- ISP는 SRP와 비슷하지만, 인터페이스를 통한 다른 해결책을 제시한다는 점에서 조금 차이가 있다.
  - 예시) ```class 사람 implements 군인``` 이면 군인 ```홍길동 = new 사람()``` 을 통해 군인 인터페이스의 메소드만을 사용하도록 제한하는 것이다. SRP였다면 class를 나눠버렸겠지만, 일반적으론 ISP보다 SRP 할 것이 권장된다.

## 5. DIP (Dependency Inversion Principle): 의존 역전 원칙

- 의존 관계를 맺을 때 변화하기 쉬운 것 또는 자주 변화하는 것 보다는 변화하기 어려운것, 거의 변화가 없는 것에 의존하라는 원칙
- 상위클래스일수록, 인터페이스일수록, 추상 클래스일수록 변하지 않을 가능성이 높기에 하위 클래스나 구체 클래스가 아닌 상위클래스, 인터페이스, 추상클래스를 통해 의존하라는 원칙
- DIP 를 어겼을 때의 해결 방법은, OCP와 비슷하다. 구체적인 클래스가 아닌, 인터페이스에 의존함으로써 DIP를 해결할 수 있을 것이다.

<br>
<br>

## 📖 Reference

- [oop란](https://velog.io/@dolarge/CS-%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5%EC%9D%B4%EB%9E%80)
- [스위프트가 지향하는 프로그래밍 패러다임](https://bite-sized-learning.tistory.com/550)
- [oop란, 사진출처](https://radait.tistory.com/4?category=836792)
- [override, overload에 대한 코드 및 개념 참고](https://babbab2.tistory.com/129)

#### 📝 SOLID를 만족하기 위해서,, 리팩토링의 개념이 사용된다. (좋은 코드 = 객체지향과 상당한 연관이 있구나)

- [oop의 solid 원칙 자세한 설명](https://sjh836.tistory.com/159)
- [리팩토링의 기초 - 단계, 단계와 분리, 다형성](https://becomereal.tistory.com/121)
- [Massive View에 대한 설명](https://jisoo.net/2018/11/24/why-mvc-destroyed.html)
- [조건부를 다형성으로 바꾸기 리팩토링 방식](https://sourcemaking.com/refactoring/replace-conditional-with-polymorphism)
- [✨swift의 SOLID, 그리고 피해야할 코딩 습관](https://soojin.ro/blog/solid-principles-in-swift)
