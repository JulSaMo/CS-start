본 글은 '생활코딩 linked list (1), (2), (3)'과 '소들이 블로그' 보고 작성하였습니다.

# 🟣 Linked List (연결 리스트)
Linked List 는 array List와는 다르게 element와 element간의 연결(link)를 이용해서 리스트를 구현하는 것을 의미한다. 
그래서 이름이 linked list 이다. 의미로 따져보면, linked list에서는 link 가 무엇을 의미하는지 파악하는게 가장 중요하다.

( ⚠️ array list와의 차이점은 아주 중요한 면접 질문 요소입니다. 다음 섹션에서 계속 설명할게요 이건)

## 🟪 Link란
연결(link)에 대해서 설명하기에 앞서, 컴퓨터가 동작하는 원리에 대해서 조금 살펴보고, array list와의 차이를 아주 잠깐 배워보자.

컴퓨터에는 4가지의 중요한 부품이 있다. cpu, 메모리, 그리고 스토리지 (storage) 이다. 

메모리는 보통 우리가 부르는 RAM과 같은 것이고, 스토리지는 SSD, HDD와 같은 것들이다.
메모리는 속도가 매우 빠르지만 용량이 매우 작다. 그리고 전기를 끄면 데이터가 사라지는 속성을 갖고있다. 이러한 이유때문에
데이터는 기본적으로 '스토리지'에 저장!!된다. 하지만 스토리지는, 매우 느리기 때문에 CPU와 함께 일을하기에 매우 부적절하다.
그래서 어떤 일을 하면, 그 프로그램과 데이터는 메모리로 옮겨지고, CPU는 메모리에 로드된 데이터를 이용해서 여러가지 일을 하게 된다.
이걸 그림으로 살펴보자. (반복학습 ^__^)

<img width="503" alt="image" src="https://user-images.githubusercontent.com/96969693/183289561-ca22cc3c-6ab5-49bb-baac-9405f287738a.png">
(그림출처 - 생활코딩 https://opentutorials.org/module/1335/8821)

그러므로 실행속도를 결정하는 것은 대체로 메모리읻. 우리가 Data Structure를 배우는 이유는 이러한 메모리를 효율적으로 사용하기 위함이다!

### 🔗 메모리를 '건물'에 비교해보자
메모리의 구조는 나중에 자세히 살펴보도록 하고, 우리는 메모리를 '건물'에 비교해 보자. 

<img width="504" alt="image" src="https://user-images.githubusercontent.com/96969693/183289678-d020ea9a-e727-46c7-9e18-4f3d0e2fcdd1.png">
(그림출처 - 생활코딩 https://opentutorials.org/module/1335/8821)

#### 📌 Array List
왼쪽 회사는 모든 직원이 한 층에 모여있다. 배열은 이렇게 건물을 사용하는 것과 비슷하다. 만약 회사가 성장해서 사무실이 좁아지면, 더 이상 새로운 직원을 뽑을 수 없다. 붙어있는 공간이 부족하기 때문이다. 더 많은 공간이 필요하다면, 더 많은 사람을 수용할 수 있는 공간을 찾아서 전체가 이사가야한다.

#### 📌 Linked List

<img width="273" alt="image" src="https://user-images.githubusercontent.com/96969693/183289746-9e936a62-1921-4b1d-a365-591a2dfe7283.png">
(그림출처 - 생활코딩 https://opentutorials.org/module/1335/8821)

linked list 는 한 건물 내에서 한 회사가 임대한 사무실이 여러군데로 떨어져있다. 덕분에 인원이 늘어나도, 회사가 부족할 걱정은 없다. 하지만, 방문자가 사무실을 찾아가야할 때 사무실을 찾는 방식이 조금 비효율적일 수 있다. 이 그림에서처럼, 방문자가 3번째 사무실을 찾아가려면, 1번째부터 방문해서, 다음, 다음 연결된 사무실로 찾아가야 한다.

이렇게 물어물어 사무실을 찾아가는 방식이 바로 linked list 이다. 그래서 linked list 는 몇번째 element를 찾는 것이 굉장히 느리다는 단점이 있다.

반면에 array list 는 한 군데 모여 있기 때문에 index로 접근하면, 바로 3번째 사무실에 접근이 가능하다는 점이 장점이기도 하다.


#### 📌 연결
linked list 의 연결이 어떤 의미인지 이제 대충은 알았을 것이다. 배열과는 다르게, linked list 는 그 위치가 흩어져 있기 때문에 서로 연결되어 있어야만 한다. 바로 이런점에서 연결이라는 개념이 사용된다.

linked list는 다양한 데이터 스트럭쳐에서 광범위하게 사용되는 개념이다. 고로 꼭 알고 넘어가야한다!!

### 🔗 linked list 에서의 용어
linked list에서 서로 연결된 element들은 'node (노드)' 혹은 'vertex (정점)'이라고 부른다. 


## 🟪 Linked list 의 구조

linked list 의 노드는 최소 두 가지의 정보를 알고 있어야 한다. '노드의 값'과 '다음노드'이다. 각각의 노드가 다음 노드를 알고 있기 때문에 하나의 연결된 list 를 구성할 수 있기 때문이다. 그래서 linked list의 구조는 아래와 같이 생겼다.

<img width="504" alt="image" src="https://user-images.githubusercontent.com/96969693/183290081-829592b8-df20-473b-ae13-8b8d43f0ee45.png">

linked list 는 이렇게 데이터 필드와 다음 노드에 대한 참조를 포함하는 노드로 구성되어 있다. Head는, 첫번째 노드를 의미한다. 취향에 따라 first라고 변수명을 붙이기도 한다.

### 🔗 왜 linked list 를 사용할까?
배열은 비슷한 유형의 선형데이터를 저장하는데 사용될 수 있지만, 제약사항이 있다. 배열의 크기가 고정되어있어서, 미리 요소의 수에 대해 할당을 받아야한다거나, 새로운 요소를 삽입하는데 많은 비용이 든다는 점이다. (배열은 새로운 요소를 추가할 때, 공간을 만들고 나머지 요소들을 전부 옮기는 식으로 삽입하게 된다. cost가 크다 그리고 오버헤드가 발생할 수 있다,,!) 그래서 연속적이지 않은 위치에 데이터를 저장할 수 있는, 선형 데이터 구조인 linked list 를 사용하는 것이다 (배열의 단점 보완). linked list 는 포인터를 사용하여 연결되어있다.

### 🔗 장점과 단점
| - | 배열 | linked list |
|---|---|---|
|장점| 인덱스 값을 미리 알고있는 경우, 데이터에 신속한 접근 가능 | 데이터 삽입 및 삭제 속도가 빠름 (원하는 때에 메모리 공간을 할당에서 사용하고, 연결만 바꿔주면 되기 때문에!)|
|단점 | 크기가 고정되어있음 / 새로운 요소를 삽입하는 과정이 비효율적임 (오버헤드 발생 가능) | 검색 속도가 느림 / 저장공간 효율이 높지 않음 (연결정보를 저장하는 저장공간이 별도로 필요하기 때문) |


# 🟣 단방향 연결리스트 
먼저 단방향 연결리스트에 대해서 알아보자. 앞에서 설명했듯, 연결 리스트는 연속되지 않은 메모리에 저장된 데이터들을 연결시켜 놓은 것이다. '연결'은, '내 다음 순서 데이터의 주소값'을 가지고 있어야 연결된다. 따라서 단방향 연결 리스트의 경우, 데이터는 아래와 같이 생겼다.
<img width="238" alt="image" src="https://user-images.githubusercontent.com/96969693/183290709-dbbf9878-4470-4692-9e16-e6127995cdf5.png">

data는 내 데이터 값을 저장하는 공간이고, next는 다음 노드의 주소값을 저장하는 공간이다. 우리는 이 네모 두칸을 'node'라고 부른다.

## 💻 코드로 Node 생성하기

[참고 - 소들이 블로그!](https://babbab2.tistory.com/86)

해당 그림의 연결리스트를 코드로 구현해볼 것이다.

<img width="671" alt="image" src="https://user-images.githubusercontent.com/96969693/183290974-f34a1f5e-a8e4-4b78-b4cc-2b36a4a2f549.png">


```swift
class Node<T> {
    var data: T?
    var next: Node?
    
    init(data: T?, next: Node? = nil) {
        self.data = data
        self.next = next
    }
}
```
데이터의 타입에 국한되지 않도록 generic을 사용해서 타입을 넣어주었다. 이제 우리는 데이터를 저장하고 싶을 때마다 배열의 element가 아니라, node를 생성해서 연결해주면 된다.

매번 노드를 생성하고 이전의 노드와 연결해주는 것을 일일히 코딩할 수 없으니, Node를 관리해주는 클래스를 하나 더 만들자.

```swift
class LinkedList<T> { }
```

### 🔗 head: 첫 노드
먼저 head 프로퍼티를 추가해주자. 앞에서 말했듯, 연결리스트는 무조건 첫번째 노드부터 순차적으로 접근해야한다고 헸기 때문이다.
우리가 구현하려고 하는 연결리스트에서 head는 3이라는 data를 가진 노드이다.

```swift
class LinkedList<T> {
    private var head: Node<T>?
}
```

이렇게 추가해주었다.

### 🔗 append(data) 연결리스트 맨 마지막에 노드 추가하기

<img width="627" alt="image" src="https://user-images.githubusercontent.com/96969693/183291027-be93d004-699f-4fcd-9a74-6a37707b483e.png">

배열에서, append의 경우, 가장 마지막 노드를 찾아내어서 그 뒤에 요소를 추가해준다. 연결리스트에서의 append도 마찬가지로 가장 마지막 노드를 찾아내고, 넣어주면 되는데, head 노드부터 순회하며 node.next가 nil 인 경우를 찾으면 된다.

```swift
func append(data: T?) {
    
    //head가 없는 경우 Node를 생성 후 head로 지정해준다
    if head == nil {
        head = Node(data: data)
        return
    }
    
    var node = head
    while node?.next != nil {
        node = node?.next
    }
    node?.next = Node(data: data)
}
```

### 🔗 insert(data: at: ) 연결리스트 중간에 노드 추가하기

연결리스트의 경우 중간에 노드를 추가하기 위해서는 index가 없기 때문에, 직접구현해서 해줄 수 있다.

```swift

func insert(data: T?, at index: Int) {
    
    //head가 없는 경우 Node를 생성 후 head로 지정한다
    if head == nil {
        head = Node(data: data)
        return
    }
    
    var node = head
    for _ in 0..<(index - 1) {
        if node?.next == nil { break }
        node = node?.next
    }
    
    let nextNode = node?.next
    node?.next = Node(data: data)
    node?.next?.next = nextNode
    
}
```

만약 찾는 index가 node의 범위를 넘어가면, 가장 마지막에 추가해주었다. 중간에 삽입하는 경우 이렇게 노드간 연결만 바꿔주면 되니까, 원하는 삽입 방식으로 커스텀하게 구현이 가능할 듯 하다.

### 🔗 removeLast : 연결리스트 맨 마지막 노드 삭제하기

<img width="645" alt="image" src="https://user-images.githubusercontent.com/96969693/183291280-a6a80883-df13-46a7-b3cf-c5cedfc96fdd.png">
<img width="391" alt="image" src="https://user-images.githubusercontent.com/96969693/183291289-a898bb27-58e3-4434-9e31-2ea25c33796a.png">

위 그림처럼, 마지막 노드와의 연결을 끊고, 그 전의 node의 next 주소값을 nil로 만들어주어야한다.

```swift
func removeLast() {
    
    if head == nil { return }
    
 // head를 삭제하는 경우
    if head?.next == nil {
        head = nil
        return
    }
    
    var node = head
    while node?.next?.next != nil {
        node = node?.next
    }
    
    node?.next = node?.next?.next
    
}
```

### 🔗 remove(at: ) 연결리스트 중간 노드 삭제하기

<img width="527" alt="image" src="https://user-images.githubusercontent.com/96969693/183291329-d125206c-b5a5-4b86-94d3-a0044b6d1a4c.png">

delete할 노드 바로 이전의 노드 next를 delete할 node의 next로 바꾸어주면 된다.

```swift
func remove(at index: Int) {
    
    if head == nil { return }
    
    // head를 삭제하는 경우
    if index == 0 || head?.next == nil {
        head = head?.next
        return
    }
    
    var node = head
    for _ in 0..<(index - 1) {
        if node?.next?.next == nil { break }
        node = node?.next
    }
    
    node?.next = node?.next?.next
    
}
```

만약 삭제하려는 index가 node의 범위를 넘어가면, 가장 마지막을 삭제해주었다.

### 🔗 searchNode(from: ) data로 노드찾기

<img width="598" alt="image" src="https://user-images.githubusercontent.com/96969693/183291378-56dd4afe-b308-46df-adb6-520a51c9640a.png">

이번에는 노드에 저장된 데이터를 직접 검색해서, 해당 노드를 반환하는 기능을 만들어보자. head에서 순차적으로 찾야함을 명심하자.

```swift

func searchNode(from data: T?) -> Node<T>? {
    
    if head == nil { return nil }
    
    var node = head
    while node?.next != nil {
        if node?.data == data { break; }
        node = node?.next
    }
    
    return node
}
```

# 🟣 양방향 연결리스트 
단방향 연결 리스트를 지금까지 구현해보고, 공부해보았는데, 단방향 연결리스트의 가장 큰 단점은 '탐색'을 할 수 없다는 것이다. 순차적으로 탐색해야하기 때문에 효율성이 매우 떨어진다. 이를 보완하고자 나온 것이 바로 양방향 연결리스트이다. 

<img width="676" alt="image" src="https://user-images.githubusercontent.com/96969693/183291555-78acdf08-604e-4631-9a74-dd577d8df547.png">

가장 첫 노드를 가르키는 head 뿐만 아니라, 가장 마지막 노드를 가르키는 tail도 가지고 있어서, 양방향으로 접근이 가능하다.
양방향 연결리스트를 구현하는 내용은, 해당 포스팅을 보면 이해가 갈 것이다!
[소들이 양방향 연결 리스트 참고글](https://babbab2.tistory.com/87)


## 📖 References
사진과 코드 출처: [소들이 블로그 - 단방향 연결리스트](https://babbab2.tistory.com/86)
초반의 개념과 사진 출처: [생활코딩](https://opentutorials.org/module/1335/8821)



