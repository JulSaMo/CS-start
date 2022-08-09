//2022. 08. 09 Noel
 <br/>
 <br/>


# ❤️ 트라이(Trie)

트라이는 문자열을 저장하고 효율적으로 탐색하기 위한 트리형태의 자료 구조 (문자열에서 검색을 빠르게 도와줌)

- 검색 시의 자동완성 기능, 사전 검색 등 문자열을 탐색하는데 특화되어잇는 자료구조
- 래딕스 트리(Radix Tree), 접두사 트리(Prefix Tree), 탐색 트리(Retrieval Tree) 라고도 함
  - 트라이는 Re**trie**val Tree에서 나온 단어
- 사용예시 ) "Datestructure"라는 단어 검색 시, 제일 먼저 'D'를 찾은 후 'a', 't',...의 순서로 찾는 개념 
<br/>



### 트라이 장단점

- 트라이(Trie)는 문자열 검색을 빠르게 한다.
- 문자열을 탐색할 때, 하나하나 전부 비교하면서 탐색하는것보다 시간 복잡도 측면에서 훨씬 효율적
- 각 노드에서 자식들에 대한 포인터들을 배열로 모두 저장하고 있다는 점에서 저장공간의 크가기 크다는 단점도 있음 (= 메모리 측면에서 비효율적일수 있다.) 
 <br/>


### 예제를 통한 Trie 이해

트라이에 `abc`, `ab`,`car`을 넣고 싶을 때
 <br/>
 
<img width="1246" alt="image" src="https://user-images.githubusercontent.com/103012104/183664875-9bfa0065-9e49-4efd-ad59-639d7f185eb2.png">


#### ①  'abc' 트라이(Trie)에 삽입

1. 첫번째 문자 a : 초기에 `트라이` 자료구조 내에는 아무것도없음 -> Head의 자식노드에 'a'를 추가
2. `a` 노드 :  자식이 없으므로, `a`의 자식노드에  `b`를 추가해준다.
3. `b`노드 : 자식노드에 `c`를 추가해준다.
4. `c`노드 : `abc`단어가 여기서 끝남을 알리기 위해 현재 노드의 Date에 'abc'라고 표시해줌

 <br/>
 <br/>


<img width="1187" alt="image" src="https://user-images.githubusercontent.com/103012104/183664984-610d2c61-4b4a-49c6-a4af-64094ba8ccd3.png">


#### ② 'ab' 트라이(Trie)에 삽입

1. `Head` :  현재 Head의 자식노드로 `a`가 존재, 따라서 추가하지않고 기존의 `a`노드로 이동
2. `a` 노드: 이미 `a` 노드에 자식노드로 존재함으로, 기존의  `b`노드로 이동
3. `b`노드 : `ab`단어가 여기서 끝임으로  현재 노드의 Date에 'ab'라고 표시

 <br/>
 <br/>
 

<img width="1232" alt="image" src="https://user-images.githubusercontent.com/103012104/183665079-57f6249d-ee4c-470f-aac3-8c1a12e73c3d.png">


#### ③ 'car' 트라이(Trie)에 삽입

1. `Head` :  현재 Head의 자식노드로 `a`만 존재, 따라서  `c`를 자식노드로 추가
2. `c` 노드: 자식노드 없음,  `a` 자식노드로 추가
3. `a`노드 :  자식노드 없음,  `r` 자식노드로 추가
4. `r`노드 : `car`단어가 여기서 끝임으로  현재 노드의 Date에 'car' 표시

 <br/>
 <br/>



# ❤️ Swift를 이용한 트라이(Trie) 만들기

 <br/>

#### ① TrieNode부터 구현

``` swift
public class TrieNode<Key: Hashable> { //제네릭
    public var key: Key? //노드의 데이터
    public weak var parent: TrieNode?
    //부모노드의 정보를 가지고 있어야 삭제 연산을 구현가능한데
    // 부모와 자식이 서로 참조하고 있으면 강한 참조 문제가 발생할 가능성이 있어 Weak 키워드 사용
    public var children: [Key: TrieNode] = [:]
    //자식 노드가 많을 수 있어서 초기화..? / 딕셔너리 초기화 하려면 [:]를 작성함
    public var isTerminating = false
    //단어의 끝을 표시하는 용도
    public init(key:Key?, parant: TrieNode?) {
        self.key = key
        self.parent = parant
    }
}
```

💡 이해를 돕는 팁!

```null
🤔 코드를 보면서 궁금한 점

- Dictionary 사용 이유 : 자식 노드들을 표현하기 위해
- class 뒤에 <Key: Hashable> 의미 : Key에 Hashable 프로토콜 채택 (= Key에 Hashable에 해당하는 타입만 가능하단 뜻) 
(참고 : https://boidevelop.tistory.com/11)
 
💡 여기서 잠깐? Hashable이 뭐야?
- Hashable : 정수 Hash 값을 제공하는 타입의 프로토콜
- Dictionary 자체가 Hash Table!!
		- HashTable은 <Key, Value> 쌍으로 1:1 매핑 되어 있는 데이터 구조
		- Key에 해당 하는 값에 정해진 해쉬함수를 적용해서 인덱스를 뽑아내고 Bucket(또는 Slot)이라고 불리는 Storage에 해당 인덱스에 Value 값을 저장하는 방식
		- 정수 Hash(=hashValue)가 있기 때문에 우리가 찾으려는 원소를 빨리 찾을 수 있음

📕 Swift 딕셔너리 특징
- Key : Value 형식으로 저장된 자료구조
- 정렬되지 않은 컬렉션
- Key = 중복불가 / Value = 중복가능
- 모든 Key의 자료형은 같아야하고, 마찬가지로 모든 Value의 자료형도 같아야함
- Dictionary의 Key 값으로 Hashable을 준수한 모든 타입을 사용할 수 있음
  - swift에서 dictionary는 Dictionary<Key Type, Value Type>의 형태로 쓰임
  - 이때의 유일한 제약사항은 Key Type이 반드시 해시가능한 타입이어야함(Hashable)
  - 즉, 그 자체로 유일하게 표현이 가능한 방법을 제공해야함

```

 <br/>
 <br/>

#### ② Trie을 구현하자

``` swift
//trie 구현
public class Trie<CollectionType: Collection> where CollectionType.Element: Hashable {
    // Trie 클래스의 제네릭에 Collection 프로토콜을 채택하는 CollectionType 을 만들어준 이유는
    //반복문을 사용하기 위해... Collection 프로토콜을 채택하고 있는 객체만 반복문을 수행할 수 있음
    public typealias Node = TrieNode<CollectionType.Element> //너무길어서 별명을줘서 코드를 요약
    private let root = Node(key: nil, parant: nil) //루트 노드는 빈값이여야함
    public init(){ }
}
```

이해를 돕는 팁!

```null
🤔 코드를 보면서 궁금한 점

💡Collection 프로토콜
	- Collection은 일반적인 “집합 컨테이너”를 묘사하는 프로토콜
	-  Sequence와 마찬가지로 각 원소들을 순회할 수 있는 연속열의 일종 (Sequence를 상속받음)
	- 모든 원소는 고정된 고유의 위치를 가지며, 이는 인덱스를 통해서 액세스할 수 있다.
	- 두 원소간의 거리는 인덱스의 거리로 표현할 수 있고, 두 인덱스간의 범위를 통해 처음과 끝이 아닌 중간 부분의 부분열을 얻을 수 있음
	- 개별 원소를 소모하지 않고 인덱스를 조작하여 순회하는 것이 가능

💡제네릭의 타입제한 Where절
	- 추가 필요
	
💡typealias
	- 기존에 선언되어 있는 유형에 새로운 유형의 별칭을 사용함으로써 코드를 더 가독성있고 이해하기 쉽도록 바꾸는 문법
	- typealias는 새로운 타입을 생성하는 것은 아님
	(참고 : https://0urtrees.tistory.com/126)

```

 <br/>
 <br/>


#### ③Trie에 추가하는 메소드 작성

```swift
public func insert(_ collection: CollectionType) {
        var current = root // 루트를 시작으로 추적하겠다는 아이디어
        
        for element in collection { // 추가하는 과정.
            // for loop 에 collection 쓸 수 있는 이유는 Collection protocol 채택했기 때문
            if current.children[element] == nil {  // 없는 거면 새로운 인스턴스 만든다.
                current.children[element] = Node(key: element, parent: current)
            }
            current = current.children[element]! //반복문 다음입력으로
        }
        current.isTerminating = true // 단어 완성 시켰으면 마지막 알파벳에 점찍어주기(단어의 끝인것을 알리기 위해)
    }
```

이해를 돕는 팁!

```
🤔 코드를 보면서 궁금한 점

```

 <br/>
 <br/>


#### ④ Trie에 해당 단어가 있는지 확인 하는 메소드 작성

```swift
//contains 메소드 구현 : 트라이에 해당 단어가 포함되어 있는지 확인 할 수 있는 메소드
    public func contains(_ collection: CollectionType) -> Bool{
        var current = root
        
        for element in collection{
            guard let child = current.children[element] else { //노드가 nil면 없는거니까
                return false //끝까지 와서 일치하는게 없으면 false 반환
            }
            current = child //입력 다음으로 입력 변화
        }
        return current.isTerminating //있다면 끝 부분 isTerminating 반환
    }

```

이해를 돕는 팁!

```
🤔 코드를 보면서 궁금한 점

```

 <br/>
 <br/>


#### ⑤ Trie에 단어를 삭제하는 메소드 구현

```swift
    //remove 메소드 구현 : 트라이의 단어를 지워주는 메소드
    public func remove(_ collection: CollectionType) {
        var current = root
        
        for element in collection {
            guard let child = current.children[element] else { return }
            current = child
        }
        guard current.isTerminating else { return print("완성 단어가 아님") }
        // 점을 짝었는지 여부와 정확한 단어를 찾은건지 여부를 확인할 수 있음
        // 동시에 루트노드가 아니라는 것도 알 수 있음
        current.isTerminating = false
        //점 찍은것을 먼저 해제시켜줌
        
        while current.children.isEmpty && !current.isTerminating {
            //1. 자식노드가 비어있지 않으면, 중복되지만 더 긴 단어가 있다는 뜻임으로 삭제하면 안됨!
            //2. dot이 찍혀있으면 다른 단어가 있는것이니 지우면 안됨
            current.parent!.children[current.key!] = nil
            current = current.parent!
        }
    }
}

```

 이해를 돕는 팁!

```
🤔 코드를 보면서 궁금한 점

```

 <br/>
 <br/>


#### ⑥ 검색 시 Trie에 해당 문자열이 있는지 검색하는 메소드

```swift
  	//collections 메소드 구현 : 검색 시 해당 문자열이 있는 단어 검색
	extension Trie where CollectionType: RangeReplaceableCollection {
    // RangeReplaceableCollection 프로토콜은 Collection 프로토콜을 상속한 프로토콜
    // Array 의 append 메소드는 Array가 RangeReplaceableCollection 프로토콜을을 상속해서 쓸 수 있는 것!
    public func collections(startingWith prefix: CollectionType) -> [CollectionType] {
        var current = root
        for element in prefix {
            guard let child = current.children[element] else { return [] } // if 문 실행해보기
            current = child
        }
        return collections(startingWith: prefix, after: current)
        // 접두어 끝이 현재의 현재 노드니까 현재 노드에 딸려있는 단어들 배열로 가져올 메소드 따로 만들자.
    }
    
    private func collections(startingWith prefix: CollectionType,
                             after node: Node)                     
                             -> [CollectionType] 
    {
        var result = [CollectionType]() // 검색 된 단어들을 담을 곳
        if node.isTerminating { // prefix 자체가 한 단어이면 반환배열에 포함시켜야지?
            result.append(prefix) 
        }
        for child in node.children.values { 
            // values 는 dictionary 구조체의 프로퍼티
            // 자식 노드의 수만큼만 반복 => 자식노드 없으면 반복 안함.
            var prefix = prefix
            prefix.append(child.key!) 
            // 자식노드 있는지 확인 안하고 강제 언래핑 가능. 반복 횟수가 이미 정해저 있으니까.
            // prefix 는 RangeReplaceableCollection 프로토콜을 채택한 타입이기 때문에 append 메소드 사용 가능.
            result.append(contentsOf: collections(startingWith: prefix, after: child)) 
            // 재귀호출 시작, 1. 종료조건 : 반복문의 node.children.values 이 0 이면 종료 -> 만족
            // 2. 작은 방향으로 이루어 지는지 : prefix 가 커져서 트리의 자식노드인 하위로 이동하므로 문제의 범위는 작아짐. -> 만족
        }
        return result
    }
}

```

 이해를 돕는 팁!

```
🤔 코드를 보면서 궁금한 점

```

 <br/>
 <br/>


#### 결과 화면

<img width="743" alt="image" src="https://user-images.githubusercontent.com/103012104/183665403-d28221c6-b218-4b7b-a682-463d4b559551.png">


 <br/>
 <br/>

출처

https://www.raywenderlich.com/892-swift-algorithm-club-swift-trie-data-structure

https://velog.io/@kimdukbae/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%8A%B8%EB%9D%BC%EC%9D%B4-Trie

https://the-brain-of-sic2.tistory.com/40

딕셔너리 해쉬에이블

 https://babbab2.tistory.com/149

https://zeddios.tistory.com/498

Collection

https://soooprmx.com/swift-array-03-collection-%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C/

