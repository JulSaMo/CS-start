#### 2022.09.26 Rookie

## 디자인 패턴이란?

디자인 패턴이란 기존 환경 내에서 반복적으로 일어나는 문제들을 어떻게 풀어나갈 것인가에 대한 일종의 솔루션입니다. 개발을 하다보면 아시겠지만 일부 구조는 반복되서 사용되는 것을 경험했을 것입니다. 개발자들이 개발하면서 겪은 문제들을 정리해서 상황 별 솔루션 컨셉을 분류해놓았다고 이해하면 됩니다.

---

## 컴포지트 패턴이란??

컴포지트 패턴은 디자인 패턴의 일종입니다. 위 맥락에서 나온 디자인패턴의 의미로 봤을 때, 컴포지트 패턴도 특정 문제를 잘 풀 수 있게 정해놓은 솔루션 컨셉입니다. 어떤 상황에서 이런게 나오게 됬을까요?

**컴포지트 패턴은** 클라이언트가 객체 구성과 개별 객체 간 차이를 무시하고 싶을 때 사용합니다. 또한 일반적으로 객체 구조가 트리 구조일떄 사용합니다.

**객체는 클래스나 구조체 같은걸 뜻한다고 쳐도 객체 구성과 객체 간 차이를 무시한다는게 무슨의미일까여?? 그리고 객체를 트리 구조로 나타낸다는 건 또 뭔 말일까요?? 바로 예시를 알아보러 갑시다!**

---

### 대표적인 예시는 폴더입니다.

폴더는 일반적으로 파일들로 이루어져있습니다. 이처럼 비슷한 속성의 객체들이 상위 객체에 속해있는 구조를 트리 구조라고 합니다! 

 근데 폴더와 파일은 비슷한점이 많습니다. 이름도 잇고 용량도 있고, 삭제할 수도 잇고… 그래서 폴더라는 객체가 파일이라는 객체의 집합이지만, 파일과 폴더 두 객체의 차이는 트리구조밖에 없습니다. 이 경우, 파일과 폴더라는 객체는 구조적인 차이를 가지지만 그 특성은 같다고 볼 수 있습니다. 

 이런 경우 이 공통된 속성을 추출해서 코드를 짤 수 있는데 이것을 개별 객체와 객체 구성간 차이를 무시한다고 표현합니다. 이러면 하나의 로직 가지고 두 객체를 커버할 수 있으니 클린하면서도 유지보수가 용이한 코드가 될 수 있습니다! 

---

 **컴포지트 패턴은 일반적으로 3가지로 나눠서 작성합니다**

component: 객체(파일)과 객체집합(폴더) 의 공통 속성을 추출한 것입니다. 

leaf: 파일과 같은 개별 객체입니다.

composite: 폴더와 같이 하위 객체들의 집합입니다.

 Swift 예시를 한번 봐보겟습니다!

```swift

#1 Component 만들기

protocol FileComponent {
    var size: Int { get set }
    var name: String { get set }
    func open()
    func getSize() -> Int
}

재가 느끼기에 Component 추출이 컴포지트 패턴의 가장 중요한 부분입니다. 
먼저 객체집합과 개별 객체의 공통 속성을 추출하여 component를 만듭니다. 이러한 작업을 추상화라고 하며 스위프트에서는 프로토콜을 사용할 수 있습니다.

#2 Composite 만들기

final class Directory: FileComponent {
    var size: Int
    var name: String
    var files: [FileComponent] = []
    func open() {
        print("\(self.name) Directory의 모든 File Open")
        for file in files {
            file.open()
        }
        print("\(self.name) Directory의 모든 File Open 완료\n")
    }

    func getSize() -> Int {
        var sum: Int = 0
        for file in files {
            sum += file.getSize()
        }
        return sum
    }

    func addFile(file: FileComponent) {
        self.files.append(file)
        self.size += file.size
    }

    init(size: Int, name: String) {
        self.size = size
        self.name = name
    }
}

디렉토리이니까 File들을 모을 수 있는 배열을 하나 가지고 있어야 합니다.(디렉토리를 폴더라고 생각하시면 편할 듯 합니다). 디렉토리의 size는 자신이 가지고 있는 모든 파일,size의 합을 반환해줘야 합니다. 파일은 여러 종류가 존재할 수 있겠죠?

#3 leaf 만들기

final class MusicFile: FileComponent {
    var size: Int
    var name: String
    var artist: String

    func open() {
        print("\(self.name) Music Artist  : \(self.artist)")
    }

    func getSize() -> Int {
        return self.size
    }

    init(size: Int, name: String, artist: String) {
        self.size = size
        self.name = name
        self.artist = artist
    }
}

final class CodeFile: FileComponent {
    var size: Int
    var name: String
    var language: String

    func open() {
        print("\(self.name) Code Language : \(self.language)")
    }

    func getSize() -> Int {
        return self.size
    }

    init(size: Int, name: String, language: String) {
        self.size = size
        self.name = name
        self.language = language
    }
}

파일은 여러 개의 종류가 존재할 수 있고 각각의 종류마다 갖는 프로퍼티도 다를 수 있습니다.저는 Music, Code 파일을 만들어봤어요. 이렇게 하면 컴포지트 패턴에 필요한 모든 요소를 구현한 거예요.바로 한 번 사용해볼게요!

import Foundation

// 디렉토리 만들기
let rootDirectory = Directory(size: 0, name: "Root")
let musicDirectory = Directory(size: 0, name: "Music")
let codeDirectory = Directory(size: 0, name: "Code")

// 여러 종류의 파일 만들기
let iUMusicFile = MusicFile(size: 10, name: "Lilac", artist: "IU")
let pinguMusicFile = MusicFile(size: 12, name: "PinguBGM", artist: "Pingu")

let swiftCodeFile = CodeFile(size: 3, name: "iOS", language: "Swift")
let kotlinCodeFile = CodeFile(size: 5, name: "Android", language: "kotlin")

// 디렉토리 안에 파일 넣기 (트리 구조 만들기)
musicDirectory.addFile(file: iUMusicFile)
musicDirectory.addFile(file: pinguMusicFile)

codeDirectory.addFile(file: swiftCodeFile)
codeDirectory.addFile(file: kotlinCodeFile)

rootDirectory.addFile(file: musicDirectory)
rootDirectory.addFile(file: codeDirectory)

rootDirectory.open()

// 디렉토리 크기 구하기 
print("RootDirectory Size : \(rootDirectory.getSize())")
print("MusicDirectory Size : \(musicDirectory.getSize())")
print("CodeDirectory Size : \(codeDirectory.getSize())")
```

### 결론

컴포지트 패턴을 적용해서 getSize함수로 파일(개별 객체)과 디렉토리(객체 집합)의 용량을 같은 함수를 적용해서 구할 수 있게되었습니다!

### More

swift에서는 프로토콜을 사용하는데 다른 함수는 클래스로 선언하고 override 하는 방식으로 구현할 수 있을 것 같습니다. 

---

## **[#](https://gyoogle.dev/blog/design-pattern/Composite%20Pattern.html#%E1%84%80%E1%85%AA%E1%86%AB%E1%84%85%E1%85%A7%E1%86%AB-%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB)관련 패턴**

### **[#](https://gyoogle.dev/blog/design-pattern/Composite%20Pattern.html#decorator)Decorator**

공통점 : composition이 재귀적으로 발생한다.

차이점 : decorator 패턴은 responsibilites를 추가하는 것이 목표이지만 composite 패턴은 hierarchy를 표현하기 위해서 사용된다.

### **[#](https://gyoogle.dev/blog/design-pattern/Composite%20Pattern.html#iterator)Iterator**

공통점 : aggregate object을 순차적으로 접근한다.

---

## Reference

[https://icksw.tistory.com/243](https://icksw.tistory.com/243) (컴포지트 디자인패턴)

[https://github.com/iDevPingu/Swift_Design_Pattern_Study](https://github.com/iDevPingu/Swift_Design_Pattern_Study)

[https://readystory.tistory.com/114](https://readystory.tistory.com/114) (디자인 패턴이란)

https://github.com/Rookie0031/WWDC_Study/issues/3   
(protocol과 추상화 관련하여 제가 공부했던 자료를 공유합니다)
