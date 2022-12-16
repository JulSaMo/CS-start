// 2022.09.27 Brown
<br>
<br>

# 🟣 어댑터 패턴 (Adapter Pattern)

```
- 서로 다른 인터페이스를 가진 객체를 함께 사용할 수 있도록 해주는 디자인 패턴
- 어댑터를 이용하여 인터페이스 호환성 문제를 해결할 수 있다.
```

# 🟣 어댑터 패턴이 왜 필요할까?

```
🤔 맥북에서 쓰이는 포트는 전부 C-Type이다. 만약 USB를 연결하고 싶으면? Adapter가 필요하다!
```

<p align="center"><img width="628" alt="image" src="https://user-images.githubusercontent.com/96969693/192475404-c2d7965b-2a50-4575-b2e0-5c8c147bfd13.png"></p>

이 어댑터를 이용하면 호환되지 않는 충전기도 사용할 수 있다.
이처럼 어댑터 디자인 패턴을 사용하는 이유는, ```서로 호환되지 않는 인터페이스를 사용하는 클라이언트를 그대로 활용할 수 있게``` 해준다.

인터페이스를 변환해주는 어댑터만 만들면 되니까 그대로 활용할 수 있게 된다. (충전기 어댑터와 정말 같은 맥락이다!)

이를 통해 클라이언트와 구현된 인터페이스를 분리할 수 있고, 나중에 인터페이스가 바뀌더라도 변경 내역은 어댑터에 캡슐화 되기 때문에 클라이언트는 바뀔 필요가 없어진다.

## 😈 어댑터는 언제 사용될까?

- 기존 클래스를 사용하고 싶은데, 인터페이스가 맞지 않을 때
- 이미 만든 것을 재사용하고자 하나, 이 재사용 가능한 라이브러리를 수정할 수 없을 때


# 🟣 어댑터 패턴의 역할

- 어떤 인터페이스를 클라이언트에서 요구하는 형태의 인터페이스에 적응 시켜주는 역할, 즉 중개인역할을 한다.
- 한 인터페이스를 다른 인터페이스로 변환하기 위한 용도이다.

# 🟣 어댑터 패턴의 주요 객체

<p align="center"><img width="1474" alt="image" src="https://user-images.githubusercontent.com/96969693/192480805-fc708ab4-57b7-4b66-b372-a2311f13ba4f.png"></p>

- ```Target```: 인터페이스를 정의하는 클래스 (Client가 사용중인 인터페이스), (다른 클래스가 현재로직에 포함되려면 따라야하는 프로토콜)
- ```Client```: Target 인터페이스를 만족하는 객체와 동작할 대상, 프로그램의 기존 로직을 포함하는 클래스
- ```Adaptee```: 현재 존재하는 클래스가 아닌 외부에서 가지고 온 유용한 클래스. 따라서 인터페이스가 다르기 때문에 바로 사용할 수 없음.
- ```Adapter```: 이러한 Client, Adaptee를 모두 사용할 수 있도록 도와줌. Adapter는 Client, Adaptee 객체를 모두 다룰 수 있고 Adaptee 객체를 Client 인터페이스로 래핑 하거나 Client 객체를 Adaptee 클래스가 사용할 수 있는 형식으로 변환해줌.

# 🟣 어댑터 패턴을 예시로 살펴보자. (Swift)

## 1️⃣ Target: 인터페이스 정의

```swift
protocol LightningPhone {
    func recharge()
    func useLightning()
}

protocol MicroUSBPhone {
    func recharge()
    func useMicroUSB()
}
```

## 2️⃣ Adaptee 정의

```swift
class Iphone: LightningPhone {
    var connector: Bool = false
    public func recharge() {
        if connector {
            print("Recharge Started")
            print("Recharge finished")
        } else {
            print("Connect Lightning first")
        }
    }
    
    public func useLightning() {
        connector = true
        print("Lightning connected")
    }
}

class Android: MicroUSBPhone {
    var connector: Bool = false
    
    func recharge() {
        if connector {
            print("Recharge Started")
            print("Recharge finished")
        } else {
            print("Connect MicroUSB first")
        }
    }
    
    func useMicroUSB() {
        connector = true
        print("MicroUSB connected")
    }
}
```

## 3️⃣ Adapter 정의

```swift
class LightningToMicroUSBAdapter: MicroUSBPhone {
    private final var lightningPhone: LightningPhone
    
    init(_ lightningPhone: LightningPhone) {
        self.lightningPhone = lightningPhone
    }
    
    public func lightningToMicroUSBAdapter(lightningPhone: LightningPhone) {
        self.lightningPhone = lightningPhone
    }
    
    func recharge() {
        lightningPhone.recharge()
    }
    
    func useMicroUSB() {
        print("MicroUSB connected")
        lightningPhone.useLightning()
    }
}
```

## 4️⃣ Client 정의

- 우선, 이 부분이 프로그램에서 동작할 부분이다.
- MicroUSBPhone과 LightningPhone 프로토콜을 따르는 충전 함수를 만들자.

```swift
func rechargeMicroUSBPhone(phone: MicroUSBPhone) {
    phone.useMicroUSB()
    phone.recarge()
}

func rechargeLightningPhone(phone: LightningPhone) {
    phone.useLightning()
    phone.recharge()
}
```

- 그다음 인스턴스를 생성하자.

```swift
let anroid = Android()
let iphone = Iphone()
```

- 각각의 인스턴스는 관련된 충전함수에 접근이 가능하다.

```swift
print("Recharging android with MicroUSB")
rechargeMicroUSBPhone(phone: android)
print("Recharging iphone with Lighting")
rechargeLightingPhone(phone: iphone)
```

- 하지만 ```rechargeMicroUSBPhone(phone: _)``` 에는 iphone이 접근할 수 없다. 다른 인터페이스이기떄문!
- 그래서 Adapter를 만들어서 접근해보려고 한다.
- Adapter는 Target(MicroUSBPhone 프로토콜)를 준수하는 인터페이스로 만들었다.
- 그래서 이제 Adaptee가 사용할 수 있는 형태가 되었다!!

```swift
print("Recharging iphone with MicroUSB")
rechargeMicroUSBPhone(phone: LightningToMicroUSBAdapter(iphone)
```

(💬 코드 결과 캡쳐 넣기!!)

# 🟣 어댑터 패턴의 장단점

## 😈 장점

- 기존 코드를 변경하지 않아도 된다.
- 기존코드를 변경하지 않기 때문에 클래스 재활용성을 증가시킨다.

## 😈 단점

- 구성요소를 위해 클래스를 증가시켜야 하기 때문에 복잡도가 증가한다.
- 클래스 Adapter의 경우 상속을 사용하기 때문에 유연하지는 못하다.
- 객체 Adapter의 경우는 대부분의 코드를 다시 작성해야 하기 때문에 효율적이지 못하다.


# 📖 Reference
- [어댑터 패턴 설명 및 이미지 및 코드](https://velog.io/@ellyheetov/%EC%96%B4%EB%8C%91%ED%84%B0-%ED%8C%A8%ED%84%B4AdapterWrapper-Pattern)
- [어댑터 패턴 기초 pingu님 블로그](https://icksw.tistory.com/241)
