// 2022.09.28 Rookie


SOLID란?

SOLID 원칙이란 객체지향 설계에 더 좋은 아키텍쳐를 설계하기 위해 지켜야하는 원칙들의 5가지를 앞의 약어만 따서 정리한 단어입니다. 
 
그렇다면 이런 원칙을 왜 알아야할까요? 🧐
 
아무래도 개발자가 좋은 제품을 생성하기 위해서는 기능을 구현하는 것도 중요하겠지만, 새롭게 어떤 기능이 추가되거나 유지 보수가 되어야 할 때 더욱 생산성 있고 유연하게 대처가 가능해야한다고 생각합니다. 이를 위해서 코드를 어떻게 설계하고 개발해나가는지가 중요하다고 생각합니다.  
 
SOLID 원칙은 이러한 좋은 설계를 위한 최소한의 원칙들을 정리해주기 떄문에, 중요하게 됩니다. 디저인 패턴 중, VIPER, MVVM들도 모두 이런 원칙에 입각하여 만들어진 패턴이라고 생각이 됩니다.
 
그렇다면 이제 5가지의 약어가 어떤 원칙들을 정의하고 있고 Swift 언어에서는 어떻게 적용되는지 알아보려고 합니다.
 
 
SRP(Single Responsibility Principle) - 단일 책임 원칙

: 클래스나 함수를 설계할 때, 각 단위들은 단 하나의 책임만을 가져야한다는 원칙입니다.
즉, 클래스나 함수가 새롭게 변해야한다면 하나의 역할을 가진 상태에서 새로운 것으로 변해야한다는 것입니다. (말이 어려운데, 강아지는 멍멍 - 고양이는 야옹 같은 느낌인 것 같아요 고양이가 멍멍 야옹하면 안되잖아요?)
 
한 번 예시를 간단히 들어서 보겠습니다.
 
### 나쁜 예

    class LoginService {
        func login(id: String, pw: String) {
            let userData = requestLogin()
            let user = decodeUserInform(data: userData)
            saveUserOnDatabase(user: user)
        }
    
        private func requestLogin() -> Data {
            // Call API
            return Data()
        }

        private func decodeUserInform(data: Data) -> User {
            // Decoding User Inform from Data
            return User(name: "", age: 10)
        }

        private func saveUserOnDatabase(user: User) {
            // Save User
        }
    }

위의 예를 보면 LoginService라는 클래스에서 DB, Decoder, APIHandler의 많은 역할을 중구난방으로 가지고 있는 것을 알 수 있습니다.
 
좋은 예
 
    protocol APIHandlerProtocol {
        func requestLogin() -> Data
    }

    protocol DecodingHandlerProtocol {
        func decode<T>(from data: Data) -> T
    }

    protocol DBhandlerProtocol {
        func saveOnDatabase<T>(inform: T)
    }

    class LoginService {
        let apiHandler: APIHandlerProtocol
        let decodingHandler: DecodingHandlerProtocol
        let dbHandler: DBhandlerProtocol

        init(apiHandler: APIHandlerProtocol,
             decodingHandler: DecodingHandlerProtocol,
             dbHandler: DBhandlerProtocol) {
            self.apiHandler = apiHandler
            self.decodingHandler = decodingHandler
            self.dbHandler = dbHandler
        }

        func login() {
            let loginData = apiHandler.requestLogin()
            let user: User = decodingHandler.decode(from: loginData)
            dbHandler.saveOnDatabase(inform: user)
        }
    }
    
    
나쁜 예와 비교해서 각각의 DB, Decoder, APIHandler 역할을 하는 프로토콜을 만들어주고 각자의 역할만하는 메소드만을 구현하게 하였습니다. 그리고 LoginService에서는 단지 이 프로토콜들을 활용해서 상효작용만을 하고 있습니다.
 
이전과 비교해서 확실히 LoginService는 로그인에 관련된 로직만을 다루는데 각각의 모듈들을 활용해서 로그인에 관한 책임만을 가지고 있다는 것을 알 수 있습니다.
 
 
## OCP(Open-Closed Principle) - 개방, 폐쇄 원칙

: 확장에는 열려있으나 변경에는 닫혀있어야 한다는 원칙입니다.
어떤 기능을 추가할 때, 기존의 코드는 만지지 않고 새로 동작하는 기능에 대해서만 코드가 작성이 되어야합니다. 이러한 원칙을 지키기 위해서는 다양한 방법들이 있을 것 같다고 생각이 듭니다.
 
우선 생각이 든 예로는 프로토콜을 활용하는 것입니다. 만약 동물의 소리를 내는 동물원이라는 변수가 있는데 여기에 새로운 동물이 추가된다고 생각을 하면 어떻게 구현했냐에 따라 OCP를 지키느냐 안지키느냐로 나뉠 수 있을 것 같습니다.
(위 SRP의 예제도 역시 프로토콜을 이용해서 OCP의 원칙을 잘 지키고 있습니다. 만약 새롭게 DB, API Call, Decoding의 로직을 수행하고 싶으면 단지 각각의 프로토콜을 구현하고 있는 객체를 외부에서 주입하면 되기 때문에 새로운 기능에도 변화없이 대응이 가능하게 됩니다.)
 
이번에도 예시로 알아보겠습니다.
 
### 나쁜 예


    class Dog {
        func makeSound() {
            print("멍멍")
        }
    }

    class Cat {
        func makeSound() {
            print("야옹")
        }
    }

    class Zoo {
        var dogs: [Dog] = [Dog(), Dog(), Dog()]
        var cats: [Cat] = [Cat(), Cat(), Cat()]

        func makeAllSounds() {
            dogs.forEach {
                $0.makeSound()
            }

            cats.forEach {
                $0.makeSound()
            }
        }
    }
    
    
여기서 만약 새로운 동물을 추가하면 어떻게 될까요?
 
class로 새로운 동물을 정의하고 Zoo에 또 기존의 코드를 만져야하고 수정을 진행하게 되겠죠...? 이렇게 되면 OCP의 원칙을 어기고 설계가 진행되게 되는 것입니다.
 
### 좋은 예


    protocol Animal {
        func makeSound()
    }

    class Dog: Animal {
        func makeSound() {
            print("멍멍")
        }
    }

    class Cat: Animal {
        func makeSound() {
            print("야옹")
        }
    }

    class Zoo {
        var animals: [Animal] = []

        func makeAllSounds() {
            animals.forEach {
                $0.makeSound()
            }
        }
    }
    
    
이렇게 프로토콜을 활용해서 설계를 진행하게 되면 새롭게 동물이 추가되면 기존의 코드는 만지지 않고 그저 class 새로운동물: Animal으로 선언하여 구현만하면 될 것 같습니다. 그렇게 되면 Zoo 클래스에서는 기존의 코드는 만지지 않고 새로운 동물들을 추가하여 함수를 동작할 수 있게 될 것입니다.
 
확장에는 열려있지만 수정에는 닫혀있는 OCP를 지키는 코드가 되는 것이죠.
 
 
## LSP(Liskov Substitution Principle) - 리스코프 치환 원칙

: 부모(super class)로 동작하는 곳에서 자식(sub class)를 넣어주어도 대체가 가능해야한다는 원칙입니다.
자식 클래스를 구현할 때, 기본적으로 부모 클래스의 기능이나 능력들을 물려받는다. 여기서 자식 클래스는 동작을 할 때, 부모 클래스의 기능들을 제한하면 안된다는 뜻입니다.
 
즉, 부모 클래스의 타입에 자식 클래스의 인스턴스를 넣어도 똑같이 동작하여야 합니다.
그렇다면 이번에도 잘못된 예와 올바르게 작성된 예로 알아보겠습니다.
 
### 나쁜 예


    class Rectangle {
        var width: Float = 0
        var height: Float = 0

        var area: Float {
            return width * height
        }
    }

    class Square: Rectangle {
        override var width: Float {
            didSet {
                height = width
            }
        }
    }

    func printArea(of rectangle: Rectangle) {
      rectangle.height = 3
      rectangle.width = 6
      print(rectangle.area)
    }

    let rectangle = Rectangle()
    printArea(of: rectangle)
    // 18

    let square = Square()
    printArea(of: square)
    // 36
    
    
실제로 정사각형은 직사각형이라고 할 수 있습니다. 이 원리에 따라 프로그램을 다음과 같이 설계하게 되면 문제가 생기게 됩니다. 바로 정사각형의 넓이를 출력해야할 때, height = width라는 구문으로 인해 printArea(_: Rectangle)에서 원하는 결과를 얻지 못하게 됩니다.

! 이 예제가 좀 이해가 안되서 다음을 참고하면 더 좋을 것 같다!
https://github.com/Tedigom/Swift/blob/master/pattern/lsp.md

 
즉, 부모(super class)의 역할을 자식(sub class)에서 대신하지 못하고 있는 상황이 발생하게 된다.
 
### 좋은 예


    protocol Shape {
        var area: Float { get }
    }

    class Rectangle: Shape {
        let width: Float
        let height: Float

        var area: Float {
            return width * height
        }

        init(width: Float,
             height: Float) {
            self.width = width
            self.height = height
        }
    }

    class Square: Shape {
        let length: Float

        var area: Float {
            return length * length
        }

        init(length: Float) {
            self.length = length
        }
    }
    
    
다음과 같은 방법으로 Rectangle, Square 모두 Shape이라는 protocol을 채택할 수 있게 설계하고 실제 구현부는 채택하는 하위 클래스로 넘기면은 LSP의 원칙에 어긋나지 않는 프로그램을 설계할 수 있게 됩니다.
 
즉, Shape의 역할을 Square, Rectangle 모두가 기존의 룰을 위반하지 않고 동작하는 프로그램이 만들어지게 됩니다. 이러한 상황을 LSP를 지킨 설계라고 하게 됩니다.
 
 
## ISP(Interface Segregation Principle) - 인터페이스 분리 원칙

: 인터페이스를 일반화하여 구현하지 않는 인터페이스를 채택하는 것보다 구체적인 인터페이스를 채택하는 것이 더 좋다는 원칙입니다.
 
인터페이스를 설계할 때, 굳이 사용하지 않는 인터페이스는 채택하여 구현하지 말고 오히려 한 가지의 기능만을 가지더라도 정말 사용하는 기능만을 가지는 인터페이스로 분리하라는 것입니다.
 
### 나쁜 예
    protocol Shape {
        var area: Float { get }
        var length: Float { get }
    }

    class Square: Shape {
        var width: Float
        var height: Float

        var area: Float {
            return width * height
        }

        var length: Float {
            return 0
        }

        init(width: Float,
             height: Float) {
            self.width = width
            self.height = height
        }
    }

    class Line: Shape {
        var pointA: Float
        var pointB: Float

        var area: Float {
            return 0
        }

        var length: Float {
            return pointA - pointB
        }

        init(pointA: Float,
             pointB: Float) {
            self.pointA = pointA
            self.pointB = pointB
        }
    }
    
    
Line, Square 모두 Shape을 상속받는 객체이지만 실제로 Square는 length라는 변수가 필요가 없고 Line은 area라는 변수가 필요없게 됩니다. 그럼에도 단지 Shape이라는 프로토콜을 채택한다는 이유만으로 필요없는 기능을 구현하고 있습니다.
 
이런 경우에 ISP의 원칙을 지키지 않고 있다고 할 수 있을 것 같습니다.
 
### 좋은 예

    protocol AreaCalculatableShape {
        var area: Float { get }
    }

    protocol LenghtCalculatableShape {
        var length: Float { get }
    }

    class Square: AreaCalculatableShape {
        var width: Float
        var height: Float

        var area: Float {
            return width * height
        }

        init(width: Float,
             height: Float) {
            self.width = width
            self.height = height
        }
    }

    class Line: LenghtCalculatableShape {
        var pointA: Float
        var pointB: Float

        var length: Float {
            return pointA - pointB
        }

        init(pointA: Float,
             pointB: Float) {
            self.pointA = pointA
            self.pointB = pointB
        }
    }
    
    
기존에 필요없는 기능들을 구현하고 있던 인터페이스들을 더욱 세분화하여 나누어주었습니다.
 
AreaCalculatableShape, LenghtCalculatableShape으로 각각 인터페이스를 세분화시켜 넓이를 구해야하는 Shape에만 AreaCalculatableShape 채택하여 구현하고 길이를 구해야하는 Shape에만 LenghtCalculatableShape 채택하여 각각을 ISP의 원칙을 지키는 프로그램의 설계가 되었습니다.
 
 
## DIP(Dependency Inversion Principle) - 의존관계 역전 원칙

: 상위 모듈이 하위 모듈에 의존하면 안되고 두 모듈 모두 추상화에 의존하게 만들어야 한다는 원칙입니다.
 
어떤 상위의 모듈에서 하위 모듈을 가지고 있을 때, 상위 모듈의 기능이 하위모듈에 의존해서 기능을 수행하면 안된다는 뜻입니다. 말이 어려울 수 있는데 즉, 추상화를 진행하여 각각의 모듈에 더 추상화된 것에 의존하게 만들어야 한다는 뜻입니다. 이렇게 코드를 설계해야 재사용에도 유용하고 하나를 수정했을 때 더욱 수정사항이 많이 없는 훌륭한 프로그램을 설계할 수 있게 됩니다.
 
(DIP 원칙은 나중에 Unit Test를 진행할 때, 더욱 중요하게 될 원칙인 것 같은데 여기서 의존성 주입이라는 용어를 쓸 수 있을 것 같습니다. 상위 모듈에 어떤 하위 모듈을 사용할 때, 상위 모듈에서 직접적으로 하위 모듈을 초기화하지 않고 외부에서 하위 모듈을 초기화 할 수 있게 하라는 뜻입니다. 그리고 이 상위 모듈, 하위 모듈은 모두 추상화된 객체에 의존할 수 있게 해야합니다.)
 
### 나쁜 예
    class APIHandler {
        func request() -> Data {
            return Data(base64Encoded: "This Data")!
        }
    }

    class LoginService {
        let apiHandler: APIHandler = APIHandler()

        func login() {
            let loginData = apiHandler.request()
            print(loginData)
        }
    }
    
    
현재 상위 모듈인 LoginService가 하위 모듈인 APIHandler에 의존하고 있는 관계로 만약 APIHandler의 구현 방법이 변화하게 되면 프로그램에 영향을 미치게 되고 새롭게 LoginService라는 상위모듈을 수정해야하는 상황이 일어날 수 있습니다. 이러한 상황이 DIP의 원칙을 어긴 프로그램의 설계라고 할 수 있습니다.
 
이를 수정하기 위해 의존성 주입이라는 것을 사용해서 수정을 해보겠습니다.
 
### 좋은 예
      protocol APIHandlerProtocol {
          func requestAPI() -> Data
      }

      class LoginService {
          let apiHandler: APIHandlerProtocol

          init(apiHandler: APIHandlerProtocol) {
              self.apiHandler = apiHandler
          }

          func login() {
              let loginData = apiHandler.requestAPI()
              print(loginData)
          }
      }

      class LoginAPI: APIHandlerProtocol {
          func requestAPI() -> Data {
              return Data(base64Encoded: "User")!
          }
      }

      let loginAPI = LoginAPI()
      let loginService = LoginService(apiHandler: loginAPI)
      loginService.login()
      
이렇게 작성하게 되면 LoginService는 기존에 APIHandler에 의존하지 않고 추상화 시킨 객체인 APIHandlerProtocol에 의존하게 됩니다. 그렇기 때문에 APIHandlerProtocol의 구현부는 외부에서 변화에 따라 지정해서 지정해주면 되기 때문에 LoginService는 구현부에 상관없이 좀 더 변화에 민감하지 않은 DIP의 원칙을 지킨 프로그램을 설계할 수 있게 됩니다.
 
이렇게 외부에서 내부의 변수를 초기화해서 의존관계를 가지는 경우를 의존성 주입이라고 하게 됩니다. 이 때, 의존성 주입을 추상화시켜 진행하게 되면 더욱 변화에는 안전한 프로그램을 설계할 수 있게 됩니다.
 

## Reference
https://dongminyoon.tistory.com/49 
