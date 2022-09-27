// 2022.09.26 Noel🎸



# ❤️‍🔥 옵저버 패턴(Observer Pattern)<br/>

<br/>

### 🤔옵저버 패턴이란?<br/>

옵저버 패턴은 한 **주체 객체(Object)의 상태가 바뀌면** 그 객체에 **의존(구독) 하는  관찰 객체(Observer)들한테 연락이 가고 자동으로 내용이 갱신**되는 방식으로 운영되는 패턴<br/>

<br/>

<br/>

### 📱 IOS에서 Observer Pattern 사용 <br/>

아래에서 Observer Pattern을 사용함<br/>

- **Foundation framework<br/>**
  - `NotificationCenter` *<br/>
  - `KVO(Key Value Observing)`<br/>
  - `Property Observer`<br/>

<br/>

- **Combine framework**<br/>
  -  `Publisher` * (Swift5.1 버전부터 Combin에 `Publisher` 가 추가됨)<br/>
  - `Subscriber`  *<br/>

```
*(별표) 참고!

Combine framework의 Publisher(Observable),Subscriber(Observer)과 Notification Center는 Observer Pattern과 비슷하지만 약간의 차이를 가진 Pub/Sub Pattern을 사용함!
```

<br/>

<br/>

### Observer Pattern 구조<br/>

> 크게 Subject(publisher), Observer(subscriber)로 구성!<br/>

- 알림주체가 되는 객체(Subject)는 자신을 관찰하는 1:N(1대다) 관계를 맺을 수 있음<br/>

<img width="1083" alt="image" src="https://user-images.githubusercontent.com/103012104/192536507-c5391cb5-7ca7-4857-a400-58aab1d33ed9.png">

#### Subject(publisher)😎<br/>

- 이벤트 발생 시 구독자가 알림을 받고 싶어하는 주체<br/>
- Subject는 자신을 구독한 Observer 목록을 가지고 있음<br/>
- Observere들을 추가, 제거, 알림을 주는 인터페이스를 제공<br/>
   - `register` : observer 등록<br/>
   - `remove` : observer 등록 취소(제거)<br/>
   - `notify` : 변화가 있을 때 observer 에게 알림<br/>

<br/>

#### Observer(subscriber)😍<br/>

- Subject를 관찰하는 구독자, Subject 변경 될때마다 알림을 받아 그에 맞는 처리를 해야하는 object<br/>
- Subject를 관찰하고 알림을 감지했을 때, 구독자가 해야할 일을 담은 update 메소드를 가짐<br/>
  - update : subject로 부터 알림을 받으면 취하는 행동<br/>
- Concrete Observer의 부모가 되는 인터페이스<br/>

<br/>

#### Concrete Observer<br/>

- Observer 인터페이스를 상속받고, Subject에 등록이 될 객체 <br/>
- Subject에 등록(구독)이 되면 이벤트를 받음<br/>

<br/>

<br/>

#### 🧐 언제 써야할까?<br/>

- 다른 개체의 상태가 변경될 떄마다 어떤 이벤트를 실행하고 싶을 때, 주로 사용<br/>

  - 주로 Swift에서는 **MVC 패턴에서 사용**<br/>

    ```예시
    ViewController 👉 Observer(Subscriber) & Model 👉 Subject(Publisher)
    
    - Model은 View Controller의 타입에 대해 알 필요 없이 상태가 변경될 때마다 이를 View Controller에 전달
    - 여러 개의 View Controller가 하나의 Model의 변경사항을 받을 수 있음(1:N)
    ```

<br/>

#### ⁉️ 옵저버 패턴의 장단점<br/>

##### 👍 장점<br/>

두 객체가 서로 **느슨하게 연결(Loose Coupling)**되어있는게 장점!<br/>

- 느슨한 연결은 두 연결된 객체들 사이에 결합도가 낮다는 것을 의미 (상호의존성이 낮음)<br/>
- => 고로 변경사항이 생겨도 무난히 처리할 수 있는 유연한 **객체지향 시스템** 구축 가능<br/>

```용어
💡이해를 돕기 위한 용어 설명!

느슨한 결합(Loose Coupling)
- 두 객체가 상호작용은 하지만, 서로에 대한 최소한의 정보만으로 연결되어 있다는 것을 의미!

객체지향 프로그래밍(OOP)
- 프로그래밍에서 필요한 데이터를 추상화 시켜 상태와 행위를 가진 객체를 만들고
- 그 객체들 간의 유기적인 상호작용을 통해 로직을 구성하는 프로그래밍 방법
- 장점 : 코드 재상용 용이/ 유지보수 쉬움/ 대형 프로젝트에 적합
- 단점 : 처리속토가 상대적으로 느림 / 객체 많음 = 용량 커짐/ 설계시 많은 시간과 노력 필요 

```

<br/>

##### 👎단점<br/>

-  관찰 객체(Observer)에게 **알림이 가는 순서를 보장 할 수 없음<br/>**
- 주체 객체(Object), 관찰 객체(Observer)의 **관계가 잘 정의되지 않으면 원하는 동작이 발생** <br/>

<br/>

<br/>

## 🖥 Swift로 만들어보자!<br/>

그럼 이제 Swift를 이용해서 Observer Pattern을 만들어 보도록 하겠습니다.<br/>

이해하기 쉽도록 유튜버와 구독자간의 상호작용을 이용한 예제입니다.<br/>

Dana님의 블로그를 기반으로 작성햇습니다!<br/>

https://daheenallwhite.github.io/design%20pattern/2019/07/02/Observer-Pattern/<br/>

<br/>

<br/>

### 👩‍🎤 인기 유튜버가 영상을 올리면!?<br/>

유투버가 영상을 올리는 이벤트가 발생하면!<br/>

- 구독자들에게 이벤트가 발생했다는 알림이 가고<br/>
- 이벤트가 발생하면, 구독자들은 영상을 시청하고 반응을 하는 예제입니다.<br/>

<img width="959" alt="image" src="https://user-images.githubusercontent.com/103012104/192536587-6949b3f6-f129-4c14-b33d-41ce9f643862.png">

<br/>

#### ① `Subject`, `Observer` protocol 정의<br/>

- `Subject`는 Observer를 추가, 삭제, 알림을 줄 수 있음
- `Observer`는 `Subject`에서 이벤트 발생 시, 구독자가 할 일이 들어갈 `update` 메소드 정의

```swift
// 감시당하는 Subject의 메소드들을 정의해줌
protocol Subject {
    func register(observer: Observer)
    func remove(observer: Observer)
    func notify(with data: String)
}

// 이벤트 발생 시, 구독자인 Observer가 할 일이 들어갈 update 메소드 정의
protocol Observer {
    var id: String { get }
    func update(_ updatedValue: String)
}
```

<br/>

#### ②`Subject` protocol을 따르는 `Youtuber` class 생성

- func `register`, `remove`, `notify`에 기능 추가
-  `uploadVideo` : 유튜버가 영상을 올리면 `subscribers`에게 알림이  감

```swift
//Subject protocol을 따르는 Youtuber class 생성
class Youtuber: Subject {
    let name: String
    var subscribers = [Observer]()
    //Subject는 자신을 관찰하는 Observer list를 가짐
   
    init(name: String) {
           self.name = name
       }
    
    func register(observer: Observer) {
            subscribers.append(observer)
        }
          
        func remove(observer: Observer) {
            subscribers.removeAll(where: {$0.id == observer.id})
        }
          
        func notify(with videoTitle: String) {
            for subscriber in subscribers {
                subscriber.update(videoTitle)
            }
        }
          
        func uploadVideo(title: String) {
            print("\(self.name)이 새로운 영상 \(title)을 업로드 했습니다.")
            notify(with: title)
        }
}

```

<br/>

#### ③ `Observer` Protocol을 따르는 `Subscriber` class 생성 <br/>

- 알림을 받으면, 영

```swift
class Subscriber: Observer {
    var id: String
    var nickname: String
    
    init(id:String, nickname: String){
        self.id = id
        self.nickname = nickname
    }
    
  // 이벤트를 감지하고 할일 : 영상시청 내용 프린트 & 좋아요
    func update(_ videoTitle: String) {
        print("\(self.nickname)이 \(videoTitle) 시청")
        thumbsUp(for: videoTitle)
    }
    
    func thumbsUp(for videoTitle: String){
        print("\(self.nickname)이 좋아요를 눌렀습니다.")
    }
}
```

<br/>

#### ④ 유투버와 구독자 생성

```swift
let Noel = Youtuber(name: "인기유튜버 노엘🎸")
let Brown = Subscriber(id: "brown123", nickname: "보라온🐻")
let Jack = Subscriber(id: "jack123", nickname: "jack🦭")
let Rookie = Subscriber(id: "rookie111", nickname: "루58🍪")
  
// 구독
Noel.register(observer: Brown)
Noel.register(observer: Jack)
Noel.register(observer: Rookie)
```

<br/>

#### ⑤ 유튜버가 새로운 영상을 올리면?<br/>

```swift
// 새로운 영상 올림
Noel.uploadVideo(title: "[❤️‍🔥인기스타로 살아보기❤️‍🔥]")

//결과
인기유튜버 노엘🎸이 새로운 영상 [❤️‍🔥인기스타로 살아보기❤️‍🔥]을 업로드 했습니다.
보라온🐻이 [❤️‍🔥인기스타로 살아보기❤️‍🔥] 시청
보라온🐻이 좋아요👍를 눌렀습니다.
jack🦭이 [❤️‍🔥인기스타로 살아보기❤️‍🔥] 시청
jack🦭이 좋아요👍를 눌렀습니다.
루58🍪이 [❤️‍🔥인기스타로 살아보기❤️‍🔥] 시청
루58🍪이 좋아요👍를 눌렀습니다.

```

<br/>

<br/>

<hr/>

출처

https://noah0316.github.io/Design%20Pattern/observer-pattern/

https://icksw.tistory.com/257

https://jiseok-zip.tistory.com/entry/iOS%EC%98%B5%EC%A0%80%EB%B2%84-%ED%8C%A8%ED%84%B4Observer-Pattern#toc-%EC%98%B5%EC%A0%80%EB%B2%84%20%ED%8C%A8%ED%84%B4%20%E2%9D%93

https://jeonyeohun.tistory.com/215
