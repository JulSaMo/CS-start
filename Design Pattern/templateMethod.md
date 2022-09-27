# 🔗 Template Method
## Template Method란?
#### Template Method(템플릿 메서드)는 부모 클래스에서 여러 메서드로 이루어진 알고리즘의 틀을 정의합니다. 이러한 알고리즘 틀을 Template Method라고 하며, 하위 클래스는 Template Method에서 단계별로 이루어진 메서드들을 override 할 수 있도록 만들어 구조를 변경하지 않고 알고리즘의 특정 단계를 재정의 할 수 있도록 하는 디자인 패턴입니다.

<img width="535" alt="스크린샷 2022-09-27 오후 4 29 11" src="https://user-images.githubusercontent.com/66079439/192461856-d875d77a-ea63-4c28-8047-6cb4ccfdc225.png">

  - Abstract Class: Abstract Class는 알고리즘을 단계적으로 작동하는 메서드들과 이들을 실제로 호출하는 Template Method를 정의합니다.
  - Concrete Class: Abstract Class에서 정의한 단계적으로 작동하는 메서드들은 override 할 수 있지만 Template Method는 override 할 수 없습니다.


## Template Method는 언제 쓰는 걸까?
#### 클라이언트가 알고리즘의 특정 단계만 제어하고 전체 알고리즘이나 구조를 변경할 수 없도록 하고 싶을 때 템플릿 메서드 패턴을 사용하면 좋습니다. 혹은 특정 단계에서의 구현만 다르고 다른 부분은 대부분 동일한 동작을 하는 알고리즘을 사용하는 경우에도 사용하면 좋습니다.
#### 예를 들어 여러 확장자의 파일들에서 원하는 데이터를 추출하는 작업을 한다고 가정해볼게요. PDF, Word, Excel 파일에서 원하는 데이터를 얻고 싶은 경우 어떤 과정으로 데이터를 얻을 수 있을까요? 일단 간단하게 생각해보면 아래와 같은 단계가 필요할 거 같습니다.

  - 1번. 특정 파일에서 데이터를 가지고 온다.
  - 2번. 가지고 온 데이터를 원하는 데이터로 처리한다.
  - 3번. 처리된 데이터를 분석한다.

#### 즉 1번 과정만 다르고 2,3번 과정은 모두 동일하게 작동되어도 문제가 없어보입니다. 하지만 만약 3개의 파일을 처리하기 위한 코드를 모두 따로 구현하면 비효율적이겠죠? 또한 다른 확장자를 분석하는 코드도 추가하려면 더 많은 작업이 필요하게 됩니다. 따라서 동일한 코드를 3번 쓰기보다는 템플릿 메서드 패턴을 사용해서 1번 과정만 3개 만들고 나머지 2,3번 과정은 동일한 코드로 구현하면 이와 같은 문제를 해결할 수 있습니다.

## Template Method의 장단점
#### 👍🏻 장점
  - 클라이언트가 알고리즘의 특정 부분을 구현해도 알고리즘의 다른 부분은 영향을 덜 받도록 할 수 있다.
  - 중복된 코드를 슈퍼 클래스에서 한 번만 정의해도 되기 때문에 효율적이다.
#### 👎🏻 단점
  - 일부 클라이언트는 이미 정의된 알고리즘만 사용할 수 있기 때문에 제한받는 상황이 올 수 있습니다.
  - Liskov Subsititution Priciple을 위반 할 수 있습니다.
  - 템플릿 메서드에 필요한 단계가 많다면 유지하기 어려울 수 있습니다.  
     
  
    
> 👀 LSP란?

#### 리스코프 치환 원칙(LSP): 자료형 S가 자료형 T의 하위형이라면 필요한 프로그램의 속성의 변경 없이 자료형 T의 객체를 자료형 S의 객체로 치환할 수 있어야 한다는 원칙


```
class Rectangle {
    var width: Int
    var height: Int

    init(width: Int, height: Int) {
        self.width = width
        self.height = height
    }

    func area() -> Int {
        return width * height
    }
}

class Square: Rectangle {
    override var width: Int {
        didSet {
            super.height = width
        }
    }

    override var height: Int {
        didSet {
            super.width = height
        }
    }
}
```

  - Rectangle class와 이를 상속한 Square class가 있다.
  - Square에서는 width와 height를 override 하고 있으며, didSet을 설정해 width 혹은 height가 set 될 때 다른 속성을 해당 값과 똑같이 set 하도록 해주었다.

#### 이는 LSP를 위반하는 예시이다. 만약 Rectangle 객체의 height 속성을 7로 설정하고, width 속성을 5로 설정했다고 해보자. 이러한 Rectangle 객체의 area() 메서드 결과는 35이다. 이런 상황에서 Rectangle 객체가 Square 객체로 변경되었다고 생각해보자. 그럼 width 설정과 함께 height 속성이 함께 설정되면서 결과는 25가 된다.

```
func main() {
    let square = Square(width: 10, height: 10)

    let rectangle: Rectangle = square

    rectangle.height = 7
    rectangle.width = 5

    print(rectangle.area())
}
```
#### 이러한 변화가 별 문제가 없어보일 수도 있다. Square라는 사실을 알고만 있으면 정상적으로 동작하는 것으로 볼 수도 있기 때문이다. 하지만 추상화라는 개념에서 보면 우리는 해당 객체가 Rectangle인지, Square인지 전혀 모르고 있어야 한다. 우리는 그저 이를 Rectangle로만 판단해야 한다. 이는 Rectangle로 판단해도 전혀 문제가 발생해선 안된다. 하지만 위의 예시에선 Rectangle과 전혀 다르게 동작한다. 그래서 LSP를 위반한 것으로 보아야 한다.

```
protocol Geometrics {
    func area() -> Int
}

class Rectangle: Geometrics {
    var width: Int
    var height: Int

    init(width: Int, height: Int) {
        self.width = width
        self.height = height
    }

    func area() -> Int {
        return width * height
    }
}

class Square: Geometrics {
    var edge: Int

    init(edge: Int) {
        self.edge = edge
    }

    func area() -> Int {
        return edge * edge
    }
}
```

#### Geometrics라는 새로운 protocol을 이들이 상속하도록 하여, 간단하게 문제를 해결했다. 이렇게 되면 우리가 객체를 Geometrics로 추상화하여 판단해도 문제 되지 않는다.

## 🔡 Template Method 예제
#### 아까 본 다양한 확장자 파일에서 데이터를 가져와서 분석하는 상황을 만들어보도록 할게요. 먼저 아까 정의해본 과정을 한 번 다시 보겠습니다.

  - 1번. 특정 파일에서 데이터를 가지고 온다.
  - 2번. 가지고 온 데이터를 원하는 데이터로 처리한다.
  - 3번. 처리된 데이터를 분석한다.

여기서 각각의 Concrete Class에서 override 할 메서드는 1번에 해당하는 메서드입니다.  
그럼 먼저 Template Method 및 다른 메서드들을 구현한 Abstract Class를 먼저 구현해볼게요.  

```
// Abstract Class
class DataMining {
    // Template Method
    final func dataMining() {
        getData()
        dataProcess()
        dataAnalysis()
    }
    
    func getData() {
        print("데이터를 불러옵니다.")
    }
    func dataProcess() {
        print("데이터 처리완료")
    }
    func dataAnalysis() {
        print("데이터 분석완료\n")
    }
}
```
Template Method 역할을 하는 dataMining()메서드는 더 이상 override 할 수 없도록 만들어 줬습니다.  
그럼 이제 Concrete Class를 구현해야하는데요, 각각의 Concrete Class에서 override 할 메서드는 getData()뿐입니다.  

```
// Concrete Class
class PDFFileDataMining: DataMining {
    override func getData() {
        print("PDF File 데이터를 불러옵니다.")
    }
}
// Concrete Class
class WordFileDataMining: DataMining {
    override func getData() {
        print("Word File 데이터를 불러옵니다.")
    }
}
// Concrete Class
class ExcelFileDataMining: DataMining {
    override func getData() {
        print("Excel File 데이터를 불러옵니다.")
    }
}
```
이렇게 3개의 Concrete Class를 구현했지만 실제로 각각의 class에서 구현한 메서드는 getData() 하나뿐인 것을 볼 수 있습니다.  
  
  
이젠 실제로 이를 사용할 Client를 구현해볼게요.
```
enum FileType {
    case pdf
    case word
    case excel
}
class Client {
    static func dataMining(fileType: FileType) {
        switch fileType {
        case .pdf:
            PDFFileDataMining().dataMining()
        case .word:
            WordFileDataMining().dataMining()
        case .excel:
            ExcelFileDataMining().dataMining()
        }
    }
}
```
3개의 파일 타입이 있기 때문에 열거형도 하나 만들어줬습니다.  
  
  
<img width="925" alt="스크린샷 2022-09-27 오후 4 59 21" src="https://user-images.githubusercontent.com/66079439/192468378-36914527-37d6-4162-97f7-1692753fd91e.png">
#### 이렇게 3개의 파일 타입을 처리 할 수 있는 코드를 만들었지만 데이터 처리와 분석 코드는 모두 Abstract Class에서 구현한 메서드를 그대로 사용하고 getData()만 각각의 서브 클래스에서 구현해준 것을 볼 수 있습니다.
  
  
  
  


## Reference
  - https://icksw.tistory.com/260
  - https://huisam.tistory.com/entry/LSP
  - https://medium.com/movile-tech/liskov-substitution-principle-96f15559e363
  - https://inuplace.tistory.com/943


