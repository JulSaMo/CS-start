// 2022.09.27 Brown
<br>
<br>

# 🟣 싱글톤 패턴이란 (Singleton pattern)

```
하나의 프로그램에서 단 하나의 객체만 있어도 되는 경우 해당 객체를 한 번만 생성하고,
모든 곳에서 접근 가능하게 해주는 패턴
```
## 😈 간단한 예시로 살펴보자.

```swift
class UserInfo {
    var id: String?
    var password: String?
    var name: String?
}
```

이렇게 User의 정보를 저장하는 클래스가 있다.
그리고 이제 여기서 

A ViewController에서 id, 
B ViewController에서 password, 
C ViewController에서 name을 입력받아서 UserInfo라는 클래스에 저장해야한다고 생각해보자.

아래와 같은 세 개의 코드를 각각의 ViewController에서 작성할 것이다.

```swift
// A ViewController
let userInfo = UserInfo()
userInfo.id = "brown"
```

```swift
// B ViewController
let userInfo = UserInfo()
userInfo.password = "123"
```

```swift
// C ViewController
let userInfo = UserInfo()
userInfo.name = "brown"
```

이런식으로 각각 객체를 만들어서 저장을 한다면, 각 instance의 프로퍼티에만 (세 가지의 인스턴스로 저장) 될 것이다,,,
우리는 하나의 인스턴스 안에 id, passowrd, name을 넣어야하는데 말이다.

<p align="center"><img width="600" alt="image" src="https://user-images.githubusercontent.com/96969693/192494794-26b2fe0a-8dcd-444a-aa23-35c8fc48f1bc.png"></p>

```
💬 다른 방법으로는

인스턴스는 참조 타입이기 때문에 UserInfo 인스턴스를 한 번 생성한 후,
이 인스턴스를 A -> B -> C 로 필요할 때마다 참조로 넘겨주어 하나의 인스턴스로 구성할 수 있음.

⁉️ 근데 이렇게 하게되면!!!
참조 되어야 할 때마다 인스턴스를 넘겨주어야해서 코드가 지저분해진다.
```

#### ☝️😃 따라서, 이 클래스에 대한 instance는 최초 생성될 때 한번만 생성해서 전역에다가 두고, 그 이후로는 이 instance만 접근 가능하게 하면 된다. 이것이 바로 싱글톤 패턴,,,

싱글톤패턴으로 개발하면, 위의 그림이 아래처럼 수정된다.

<p align="center"><img width="300" alt="image" src="https://user-images.githubusercontent.com/96969693/192495748-4625841b-c398-44f6-9a93-7d7ae02b52fb.png"></p>

이렇게 한 인스턴스에 어디 클래스에서든 접근 가능하게 만드는 것이 바로 싱글톤 패턴이다 ^____^





# 📖 Reference

- [싱글톤 소들이](https://babbab2.tistory.com/66)

