# 트리와 이진트리 (Tree & Binary Tree)

자료구조에는 선형 자료구조와 비선형 자료구조가 있는데, 트리와 이진트리에 대한 개념은 비선형 자료구조에 속한다.

간단하게 선형 자료구조와 비선형 자료구조의 특징을 이야기하자면,
선형 자료구조는 요소가 일렬로 나열되어 있는 자료 구조를 말하고, 연결리스트 / 배열 / 벡터 / 스택 / 큐 등이 이에 속한다.
비선형 자료구조는 일렬로 나열하지 않고 자료 순서나 관계가 복잡한 구조를 말한다, 그래프 / 트리 / 힙 / 우선순위 큐 / 맵 / 셋(set) / 해시테이블 등이 이에 속한다.


## 그래프 (Graph)

그래프는 정점과 간선으로 이루어진 자료구조를 말한다.

정점(Vertex): 위치라는 개념, 노드라고도 불림
간선(Edge): 위치간의 관계, 노드를 연결하는 선


## 트리 (Tree)

트리는 그래프 중 하나로 그래프의 특징처럼 정점과 간선으로 이루어져 있고, 트리 구조로 배열된 일종의 계층적 데이터의 집합이다. 루트 노드, 내부 노드, 리프 노드 등으로 구성된다.
트리로 이루어진 집합을 숲이라고 한다.

![440px-Tree_(computer_science) svg](https://user-images.githubusercontent.com/66079439/182035544-b38c3bca-09ce-407e-879c-74effa651f7c.png)


### 트리의 특징
  - 부모, 자식 계층 구조를 가진다.
  - 간선 수 = 노드 수 - 1 (V - 1 = E)
  - 트리 내의 어떤 노드와 어떤 노드까지의 경로는 반드시 존재한다.

### 트리의 구성
  - 루트 노드: 가장 위에 있는 노드. 보통 트리 문제가 나오고 트리를 탐색할때 루트 노드를 중심으로 탐색하면 문제가 쉽게 풀리는 경우가 많다.
  - 내부 노드: 루트 노드와 내부 노드 사이에 있는 노드를 뜻함.
  - 리프 노드: 리프 노드는 자식 노드가 없는 마지막 노드를 뜻함

### 트리의 높이와 레벨

![트리 이미지 상세](https://user-images.githubusercontent.com/66079439/182062306-38df9a34-2fc9-41b9-b544-e5a12ff12a74.png)

  - 깊이: 트리에서의 깊이는 각 노드마다 다르며, 루트 노드부터 특정 노드까지 최단 거리로 갔을 때의 거리를 말한다. 예를 들어 D 노드의 깊이는 2이다.
  - 높이: 트리의 높이는 루트 노드부터 리프 노드까지 거리 중 가장 긴 거리를 의미하며, 앞 그림의 트리 높이는 3이다.
  - 레벨: 트리의 레벨은 보통 깊이와 같은 의미를 지닌다. A 노드를 0레벨, B / C 노드를 1레벨... 로 본다.
  - 서브트리: 트리 내의 하위 집합을 서브트리라고 한다.

### 그래프와 트리의 차이

<img width="723" alt="GraphVSTree" src="https://user-images.githubusercontent.com/66079439/182036382-f9d15f22-d2af-4495-947f-46ce4f94ca5f.png">

### 트리구조는 왜 사용할까?

**트리구조에 저장하면 더 효율적인 자료들이 존재하기 때문**  
  예를들면, 계층적인 자료들은 트리구조를 이용하여 나타낼 경우 더 효율적이다.  
  - 회사나 정부의 조직 구조
  - 나라, 지방, 시군별 계층적 데이터
  - 인덱스(인덱스는 계층적 자료 구조로 검색을 쉽게 해준다.)

## 이진트리 (Binary Tree)

이진 트리는 자식의 노드 수가 두 개 이하인 트리를 의미한다.


### 이진트리의 분류

![트리 4종류](https://user-images.githubusercontent.com/66079439/182063738-b2776707-353f-4320-a057-485426a79edb.png)
![균형이진](https://user-images.githubusercontent.com/66079439/182036852-a17d600e-0f58-4244-9cfc-f9a8e9ff01a2.jpeg)
![정이진](https://user-images.githubusercontent.com/66079439/182036859-13fd8422-bf89-4b17-9bfb-ae65710c5c96.jpeg)

  - 정이진 트리(Full Binary Tree): 자식 노드가 0 또는 두 개인 이진 트리를 의미한다.
  - 완전 이진 트리(Complete Binary Tree): 왼쪽에서부터 채워져 있는 이진 트리를 의미한다. 마지막 레벨을 제외하고는 모든 레벨이 완전히 채워져 있으며, 마지막 레벨의 경우 왼쪽부터 채워져있다.
  - 변질 이진 트리(Degenerate Binary Tree): 자식 노드가 하나밖에 없는 이진 트리를 의미한다.
  - 포화 이진 트리(Perfect Binary Tree): 모든 노드가 꽉 차 있는 이진 트리를 의미한다.
  - 균형 이진 트리(Balanced Binary Tree): 왼쪽과 오른쪽 노드의 높이 차이가 1 이하인 이진 트리를 의미한다. map, set을 구성하는 레드 블랙 트리는 균형 이진 트리중 하나이다.

### 이진 탐색 트리

이진 탐색 트리는 노드의 오른쪽 하위 트리에는 '노드 값보다 큰 값'이 있는 노드만 포함되고, 왼쪽 하위 트리에는 '노드 값보다 작은 값'이 들어 있는 트리를 말한다.
이때 왼쪽 및 오른쪽 하위 트리도 해당 특성을 가진다. 이러면 '검색'을 하기가 용이하다.
보통 요소를 찾을 때 이진 탐색 트리의 경우 O(logn)이 걸린다. 하지만 최악의 경우 O(n)이 걸린다.
그 이유는 이진 탐색 트리는 삽입 순서에 따라 선형적일 수 있기 때문이다.

### 이진 트리 순회 방식

![이진나무트리 예시](https://user-images.githubusercontent.com/66079439/182061281-e82deab7-0b5b-4bc6-b861-92d0f4159f36.jpeg)

  - 1. 전위 순회(Preorder Traverse): 뿌리(root)를 먼저 방문
  - 2. 중위 순회(Inorder Traverse): 왼쪽 하위 트리를 방문 후 뿌리(root)를 방문
  - 3. 후위 순회(Postorder Traverse): 하위 트리 모두 방문 후 뿌리(root)를 방문
  - 4. 층별 순회(Level Order Traverse): 위 쪽 node들 부터 아래방향으로 차례로 방문

  - 1. 전위 순회: 0 -> 1 -> 3 -> 7 -> 8 -> 4 -> 9 -> 10 -> 2 -> 5 -> 11 -> 6
  - 2. 중위 순회: 7 -> 3 -> 8 -> 1 -> 9 -> 4 -> 10 -> 0 -> 11 -> 5 -> 2 -> 6
  - 3. 후위 순회: 7 -> 8 -> 3 -> 9 -> 10 -> 4 -> 1 -> 11 -> 5 -> 6 -> 2 -> 0
  - 4. 층별 순회: 0 -> 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 -> 10 -> 11


### 실전 코딩

```swift
class Node {
    let value: Int
    var leftChild: Node?
    var rightChild: Node?
    
    init(value: Int, leftChild: Node?, rightChild: Node?) {
        self.value = value
        self.leftChild = leftChild
        self.rightChild = rightChild
    }
}

//left branch
let oneNode = Node(value: 1, leftChild: nil, rightChild: nil)
let fiveNode = Node(value: 5, leftChild: oneNode, rightChild: nil)

//right branch
let elevenNode = Node(value: 11, leftChild: nil, rightChild: nil)
let twentyNode = Node(value: 20, leftChild: nil, rightChild: nil)
let fourteenNode = Node(value: 14, leftChild: elevenNode, rightChild: twentyNode)

let tenRootNode = Node(value: 10, leftChild: fiveNode, rightChild: fourteenNode)

func search(node: Node?, searchValue: Int) -> Bool {
    if node == nil {
        return false
    }
    
    if node?.value == searchValue {
        return true
    } else if searchValue < node!.value {
        return search(node: node?.leftChild, searchValue: searchValue)
    } else {
        return search(node: node?.rightChild, searchValue: searchValue)
    }
}

search(node: tenRootNode, searchValue: 14)


//What is the point of all this?
//Let's talk about efficiency
let list = [1,5,10,11,14,20]
let index = list.firstIndex(where: {$0 == 14})
```


## < Reference >

  - 트리 이미지: https://en.wikipedia.org/wiki/Tree_%28data_structure%29
  - 그래프와 트리의 차이: https://gmlwjd9405.github.io/2018/08/13/data-structure-graph.html
  - 순회 방식: https://m.blog.naver.com/rlakk11/60159303809

