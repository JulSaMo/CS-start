
Array, Array List, Linked List 의 차이점을 공부해보자.

# 🟣 개념 살펴보기

## ⚠️ swift에서도 Array vs. List , Array vs. Array List 를 비교하는 것이 맞는 것일까?
잠깐, 인터넷을 찾아보니 Swift에서는 Array와 ArrayList를 구별해서 사용하지 않는 것 같다. 기본적으로 JAVA에서는 Array는 크기가 정해져있는 배열, Array List는 크기가 동적으로 움직이는 배열을 의미하는데, Swift에서는 Array의 capacity는 동적으로 움직인다. 그리고 크기가 정해진채로 Array를 선언 가능하지만, append로 자유롭게 데이터를 삽입할 수 있고, 이에 따라 capacity가 동적으로 움직일 수 있다.

더불어 타 언어는 List와 Array가 따로 존재하는데, swift는 List 자료형이 따로 있지 않다. 보통 List와 Array는 'index'가 무엇을 의미하는가에 차이가 있다.

### ⁉️ 여기서 궁금한건, 진짜로 Swift에서는 이런 비교가 무의미한 것인가? 


일단 기본적인 개념은 알고 가야 자료구조를 이해하기 편할 것 같으니, 마저 공부해보자.

## 🟪 Array 란?
##### 👉 Array 섹션 보러가기 (머지되면 링크 붙여넣기)

- 데이터가 많아지고 그룹 관리의 필요에 따라 배열을 사용
- 고정된 크기를 갖는 같은 자료형의 원소들이 연속적인 형태로 구성된 자료구조
  - 인덱스에 따라 값을 유지하므로, 원소가 삭제되어도 빈자리가 남게되어 메모리가 낭비될 수 있다.
  - 처음 크기를 10으로 지정했다면, 5개의 데이터만 저장하더라도 실제 크기는 10이다
- Index의 의미: 각 원소의 번호로 0부터 시작하며, 해당 원소에 접근할대 이용한다. (해당 값의 고유 식별자)
- 데이터의 갯수가 확실하게 정해져 있다.
- 연속적인 만큼 인덱스로 random access가 가능하다.
- 삽입과 삭제의 경우, 연속적인 형태 유지를 위해 shift연산을 수행해야하므로 O(n)의 시간복잡도를 갖는다.

앞에서 공부했듯이, 배열은 새로운 데이터를 추가할 수 없다는 한계를 갖고 있다. (수정과 삭제는 가능)
그럼, 이런 배열의 처음, 중간, 끝에 데이터를 추가하기 위해서는 어떻게 해야할까?

바로 list를 사용하는 방법이 있다.


## 🟪 List 란?

- 배열의 문제점을 해결하기 위한 자료구조
- 빈틈없는 데이터의 적재
  - 원소를 삭제했을 때, 삭제된 데이터 뒤 원소로 빈틈없이 연속적으로 위치 -> 메모리낭비 X
- Index의 의미: 배열에서는 인덱스가 유일무이한 식별자이지만, 리스트에서는 몇번째에 위치하는지 정도의 의미만 갖는다.
- 빈 element를 허용하지 않음.
- 언어별로 지원하는 list가 다르다.
  - **최근언어: 리스트를 기본으로 제공**
    - 아무래도 swift는 array라고 칭하는 것이 모두 list의 특징을 갖는것 같다. 즉, list로 제공된다.
  - C: list지원 x
  - JS: 배열에 리스트 기능 포함
  - Python: 기본 리스트, 배열을 지원하지 않음. (배열과 리스트 구분이 없음)
  - JAVA: 배열과 리스트 모두 지원, ArrayList, LinkedList로 나뉜다.

List는 배열과 같이 그룹화된 자료구조이지만, 순서가있다. 배열의 index도 순서가 있지만, 배열의 index는 위치를 나타내는 개념이 강하다. 하지만 List의 index는 '몇번째 데이터인가'에 대한 개념이다. 즉, array에서의 index는 유일무이 식별자, List에서는 데이터의 순서를 나타내는 수!


## 🟣 List를 만드는 방법
List를 만드는 방법은 두 가지가 있다.

### 🟪 Array List
Array의 주요 특성인 index 라는 특성을 이용해서 데이터에 접근 및 조작한다. 이 index를 활용하면 해당 index의 element값을 바로 반환해줄 수 있는 장점이 있다.

하지만 Array 의 특성을 그대로 가져오기때문에, 메로리에 일렬로 저장된다. 그래서 추가 및 삭제 시 해당 인덱스 뒤에있는 모든 값들을 당겨주거나, 밀어주면서 동작한다. (비효율!)


### 🟪 Linked List
👉 Linked List 섹션 보러가기 (여기서는 간단하게 설명) (머지되면 링크 업로드하기)
Linked List는 array처럼 일렬로 메모리에 저장되지 않는다. 하나의 '노드'라는 객체로 구성되며, 객체는 본인의 value와, 다음 노드에 대한 정보를 가지고 있다. 그래서 추가 및 삭제가 발생했을때, 다음 노드에 대한 정보만 바꿔주면 되기 때문에 array보다 효율적이다. 하지만 head부터 순차적으로 탐색해야한다는 단점이 있다.

# 🟣 비교하기

## 🟪 Array vs. ArrayList , Array vs. Linked List (Array를 기준으로만 비교)
해당 비교는 자바 기준으로, '자료구조 관점'에서만 비교한 내용이다. Swift에는 해당하지 않을 수 있다.

| **-** | **Array** | Array List | Linked List |
| --- | --- | --- | --- |
| 사이즈 | 길이 고정 | dynamic한 길이. ArrayList는 사이즈를 나타내는 capacity 인스턴스 변수를 가진다. ArrayList에 요소들이 더해지면, ArrayList의 capacity가 자동으로 늘어난다. | 동적인 길이를 갖는다 |
| 속도 | 초기화 시 메모리에 할당되어 속도가 빠름 | 추가 시 메모리를 재할당해야해서 속도가 느림 |
| 변경 | 사이즈 변경 불가 | 삽입, 삭제 가능 (O(N)) | 삽입 삭제 가능 (O(1)), 새로운 요소에 할당된 메모리 위치 주소가 linkedlist 이전 요소에 저장된다. |
| 다차원 | 가능 | 불가능| 
| element로 가능한 타입 | primitive type (int, char, byte), object type 모두 가능 | object type 만 가능 |
| 제네릭 | 사용 불가능 | 사용가능 (타입안정성 보장) |
| 길이구할때 | length 변수 | size() 메서드 사용 |
| 변수 추가할 때 | assignment 연산자 사용 | add() 메서드 이용 |
| 접근 | random access를 지원. 요소들을 인덱스를 통해 접근할 수 있다. 특정 요소에 접근하는 시간은 O(1) | array와 같음 | sequential Access를 지원. 어떤 요소에 접근할 때 순차적으로 검색해야한다. O(N)이 걸린다|


## 🟪 ArrayList vs. LinkedList
| - | Array List | Linked List |
| --- | --- | --- |
| 공간적 제약 | 결국 배열이므로 크기가 고정. 새로운 요소를 추가하려고 할 때, 배열의 용량이 이미 가득 차있다면 새로운 배열 생성해주어야함. | 한개의 Node는 다른 Node에 대한 참조만 가지고 있다. 공간적 제약을 Array list에 비해 받지 않음|
| 새로운 요소 삽입 (맨뒤나 맨앞) | 새로운 요소를 추가할 때, 여유 공간이 있는경우엔 O(1), 여유공간이 없으면 O(N) | 항상 O(1), 이유는 마지막 요소에서 참조값을 가지게만 하면 되기 때문에 |
| access 방법 | Random Access (어떤 요소에 바로 접근하는 것). O(1) | Sequential Access (순차접근, 어떤 요소에 접근할 때 차례대로 접근하는 것, O(N) |
| 중간에 요소 삽입하기 | 해당 요소의 뒤에 있는 값들을 전부 옮기고 삽입 | 앞뒤요소의 참조값만 변경 |
| 중간에 요소 삭제 | 뒤에있는 요소들을 전부 앞으로 한칸씩 이동 | 앞뒤 요소의 참조값만 변경 |

이를 간단하게 요약하자면 아래 이미지와 같다.

<img width="679" alt="image" src="https://user-images.githubusercontent.com/96969693/183595927-a6126898-9b92-4cc9-bfe4-47d4537bdc8d.png">


# 핵심 포인트 정리!!
지금까지 작성한 내용은 모두 '자바'에 기반한, 자료구조적 설명이다. swift에서는 Array와 Array list를 따로 지원하지 않지만, 자료구조를 공부하면서 이들의 차이점은 정확하게 알고 넘어가야하기 때문에 알아두도록 하자.

- 핵심 포인트는, Array는 random access , linked list는 sequential access 기 때문에 시간복잡도에서 차이가 난다는 점
<img width="402" alt="image" src="https://user-images.githubusercontent.com/96969693/183596677-1d4db438-f277-4af3-9341-ccadae851f32.png">



## 📖 References
[Array 와 List](https://jinsangjin.tistory.com/80)
[마지막 세가지 핵심포인트 설명 캡쳐 이미지 출처](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Array%20vs%20ArrayList%20vs%20LinkedList.md)
[ArrayList vs LinkedList](https://velog.io/@humblechoi/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-ArrayList-vs-LinkedList)
[Array vs ArrayList](https://velog.io/@humblechoi/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-Array-vs-ArrayList)
[Array vs LinkedList](https://velog.io/@humblechoi/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-Array-vs-LinkedList)
