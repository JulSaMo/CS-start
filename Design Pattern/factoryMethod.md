# Factory Method
## 🏭 Factory Method란?
##### 객체를 만들기 위한 인터페이스를 정의하지만, 어떤 클래스의 인스턴스를 생성할지에 대한 결정은 하위 클래스가 정하도록 하는 방법.
##### 간단하게 말해서 객체 생성을 서브 클래스가 하도록 처리하는 패턴.

##### 즉, 객체 생성을 캡슐화할 수 있으며 이로 인해 부모 클래스는 자식 클래스가 어떤 객체를 생성하는지 몰라도 된다.

<img width="598" alt="스크린샷 2022-09-27 오후 5 16 14" src="https://user-images.githubusercontent.com/66079439/192471989-42dd1e04-5907-44ea-ae1e-75a177d361da.png">

##### 팩토리 메서드 패턴은 위와 같은 구조를 갖는다.
  - Product
    - Creator와 하위 클래스가 생성할 수 있는 모든 객체에 동일한 인터페이스를 선언.
  - Concrete Product
    - Product가 선언한 인터페이스로 만든 실제 객체.
  - Creator
    - 새로운 객체를 반환하는 팩토리 메서드를 선언.
    - 여기서 반환하는 객체는 Product 인터페이스를 준수하고 있어야 함.
  - Concrete Creator
    - 기본 팩토리 메서드를 override 하여 서로 다른 Product 객체를 만든다.

> 즉, 팩토리 메서드 패턴은 객체를 만드는 Factory를 만드는 패턴이라고 할 수 있음.

## 🏭 Factory Method는 언제 쓰나?
##### 팩토리 메서드 패턴을 사용하는 예를 들어볼게요. 예를 들어 음악 재생 앱을 만들었다고 해보겠습니다. 처음 앱을 만들 땐 MusicPlayer라는 객체를 통해 음악만 재생 가능한 앱을 만들었는데, 앱이 잘 팔려서 비디오도 넣어야 하는 상황이 된거예요. 현재 음악만 재생할 수 있도록 만든 MusicPlayer만 있었기 때문에 만약 VideoPlayer를 추가하려고 한다면 코드 전체를 수정해야합니다. 또한 나중에 VR Player, AR Player 등과 같은 기능들이 추가된다면 추가 될 때 마다 코드 전체를 수정해야하는 문제가 생기겠죠?
##### 이럴 때 사용할 수 있는 패턴이 팩토리 메서드 패턴입니다. 객체를 직접 만드는 것이 아닌 팩토리 메서드를 통해서 만드는 거에요. 아까의 예로 다시 돌아가 보면, MusicPlayer가 필요한 곳에서는 MusicPlayer를 생성하는 메서드를 호출하고 VideoPlayer가 필요한 곳에서는 VideoPlayer를 생성하는 메서드를 호출하는 거죠.
##### 이렇게 된다면 새로운 유형의 Player를 만들어야 한다고 하더라도 팩토리 부분에 메서드를 추가해서 간단하게 처리할 수 있습니다. 하지만 각각의 Player들은 서로 다른 콘텐츠를 취급하더라도 궁극적인 기능은 같기 때문에 동일한 인터페이스를 사용해야 할 거예요.

> 새로운 기능이 추가되더라도 팩토리 메서드를 사용하여 새로운 객체를 만들 수 있음  

> 기존 객체에 수정이 생기더라도 팩토리 메서드만 수정하면 됨
  
  
## 🔡 예제
##### 그럼 실제로 팩토리 메서드 패턴을 간단한 에제를 통해 사용해보도록 하겠습니다.
##### 아까 예로 들었던 음악, 비디오 앱에 사용할 플레이어 객체를 만드는 것을 Swift 언어로 간단하게 만들어보겠습니다.

> 일단 Product에 해당하는 Player 프로토콜부터 만들어 볼게요
```
protocol Player {
    var content: String { get set }
    init(content: String)
    func play()
    func pause()
    func changeContent(name: String)
}
```

> 이렇게 만들어진 프로토콜을 채택하는 Concrete Product들이 바로 MusicPlayer, VideoPlayer겠죠?
```
class MusicPlayer: Player {
    var content: String
    required init(content: String) {
        self.content = content
    }
    
    func play() {
        print("MusicPlayer Play")
    }
    
    func pause() {
        print("MusicPlayer Pause")
    }
    
    func changeContent(name: String) {
        print("\(self.content)에서 \(name)로 음악 변경")
        self.content = name
    }
}

class VideoPlayer: Player {
    var content: String
    required init(content: String) {
        self.content = content
    }
    
    func play() {
        print("VideoPlayer Play")
    }
    
    func pause() {
        print("VideoPlayer Pause")
    }
    
    func changeContent(name: String) {
        print("\(self.content)에서 \(name)로 비디오 변경")
        self.content = name
    }
}
```
> 그럼 이젠 Creator를 만들어야 합니다. Creator는 특정 프로토콜을 채택한 객체만 반환할 수 있으니 지금 예제에서는 Player 프로토콜을 재책한 객체들을 반화하면 됩니다.
> 그리고 Music, Video를 구분하기 위해 열거형을 하나 정의 합니다.
```
protocol PlayerCreator {
    func createPlayer(content: String, contentType: ContentType) -> Player
}

enum ContentType {
    case music
    case video
}
```
> 이렇게 만들었다면 이제 Player 객체를 만들 때 Factory 객체를 통해서 만들면 됩니다.

<img width="1055" alt="스크린샷 2022-09-27 오후 5 29 24" src="https://user-images.githubusercontent.com/66079439/192475019-4c8c68fa-b0ef-4064-b8e8-30ed8f34f01b.png">

##### 이렇게 손쉽게 서로 다른 Player를 만들어서 사용할 수 있게 되었습니다. 만약 다른 Player를 추가하고 싶다면 위의 코드는 전혀 수정할 필요없이 팩토리 부분만 수정해주면 됩니다.
##### 만약 어떤 프로그램에서 100개의 플레이어를 사용한다고 한다면, 100번을 수정할 필요없이 팩토리 부분만 수정하면 되도록 해주는 패턴이 팩토리 메서드 패턴입니다.

## Reference
  - https://icksw.tistory.com/237
  - https://velog.io/@ryan-son/%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4-Factory-pattern-in-Swift
