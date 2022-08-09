# Btree

B-trees are similar to binary search trees in many ways, but they have two big differences: 
   - the number of children per node is not limited to two
   - the number of keys in the node is also variable (not just 1).

B-trees are self-balanced, rooted, sorted trees. They allow operations such as insert, search, deletion, and access in logarithmic time.

Each internal node has n keys. These keys are like dividing points between child nodes. So, for n keys, the internal node has n+1 child nodes.

This feature makes B-trees suitable for different applications in fields such as databases and external storage.
Having more than two children per node and multiple keys allows the B-tree to perform multiple comparisons for each internal node,
so it has less tree height and therefore reduces the time complexity to access and search nodes.

As has been said, each internal node in a B-tree has a different number of keys inside. 
These keys are used to divide the subtrees below them in order.
Look at the following example:

![btree](https://user-images.githubusercontent.com/66079439/183341737-42fa5a96-8871-4a5f-b8b0-78bbfc38b6e7.jpeg)

B-tree example
Internal node A has three children (subtrees). In order to separate them, it needs two keys [5, 20]. As you can imagine, it is easy to search for a specific node when you have a well-organized structure like this.
Let enumerate some mathematical properties for B-trees.
For a B-tree of order X:
* 		The root node may have 1 value and 0-2 children
* 		The other nodes have the following:
    * 		x/2 to x-1 ordered keys
    * 		x/2-1 to x children (subtrees)
* 		The worst height case is O(log(n))
* 		All the leaves have the same depth, which is the height of the tree

------------------------------------------------------------------------------------------------------------------------------------------------

# B-트리
이진트리의 확장된 버전으로 하나의 노드가 가질 수 있는 자식 노드의 최대 숫자가 2보다 큰 m원 탐색 트리 자료구조이다.

노드의 자식 노드 레벨 규칙을 두어 전체적으로 트리의 균형을 유지하기 때문에 기본적인 m원 탐색 트리보다 향상된 탐색 성능을 가지고 있다고 볼 수 있다. B트리의 특징을 열거하면 아래와 같다.

   - 노드가 삽입되거나 삭제될 때, 내부 노드는 자식 노드의 수를 만족시키기 위해 분리되거나 혹은 다른 노드와 합쳐진다.
   - 루트와 잎 노드를 제외한 트리의 노드는 최소 ⌈m/2⌉개의 서브트리를 가져야 한다. 여기서 m은 차수를 의미하는데 예를 들어 m이 3이면, 내부노드는 최소 ⌈3/2⌉ = 2개의 서브트리를 가져야 한다는 뜻이다.    - 차수가 3이기 때문에 각각의 노드는 2개의 키를 가진다.
   - 루트 노드는 최소 2개의 자식(서브 트리)을 가져야 한다.
   - 트리의 모든 잎 노드는 같은 레벨에 있어야 한다. 이는 내부 노드에 있는 자식 노드의 수를 최대화함으로써 트리의 높이는 감소하며, 균형 맞춤은 덜 발생하고, 효율 증가를 가져다 준다.
   - 모든 삽입은 잎 노드에서 시작해야 한다. 삽입을 할 때는 삽입할 위치를 찾기 위해 노드를 왼쪽에서 오른쪽으로 탐색하며 들어갈 자리를 찾는다. 분리가 필요하면, 노드를 2개로 분리하고 키값과 포인터를 분리한 노드에 분배한다.
 
분배 시 중간 값을 가지는 노드는 부모 노드에 삽입한다.
삭제를 할 때는 먼저 삭제할 키값을 가지고 있는 노드를 찾아야 한다. 그 노드가 잎 노드일 경우, 키값을 삭제하고 필요 시 노드들을 재배열한다.
그 노드가 내부노드일 경우, 키값을 삭제하고 잎 노드에서 삭제된 자리에 올 키 값을 옮긴다. 삭제된 자리로 옮길 잎 노드가 정해진 개수의 키 값을 갖지 않으면 트리를 재배열 한다.


# B*트리
B-트리를 변형시킨 트리로서 공집합이거나 높이가 1 이상인 m원 탐색 트리이다.(m은 차수).

루트 노드가 아닌 노드는 노드의 2/3 이상이 채워져야 하는 특징이 있다. 루트노드가 가지는 자식노드의 갯수 범위는 2 ≤ x ≤ 2⌊(2m-2)/3⌋ +1 (x는 개수).

루트 노드와 잎노드가 아닌 노드는 최소 ⌈(2m-1)/3⌉ 개의 자식 노드를 가져야 한다. 차수가 m이기 때문에 잎노드가 아닌 노드는 포인터가 m개, 키 개수는 m-1개를 갖는다.
B*트리 또한 노드 삽입/삭제가 가능한데, 삽입 시 노드가 꽉 차더라도 바로 분리하지 않고, 키값과 포인터를 재분배하여 형제 노드로 이동시키는 구조를 갖고 있다. 만약 형제노드가 꽉 차있는 경우 노드를 분리한다.(2개 → 3개) 분리한 노드는 노드의 약 2/3가 차있어야 한다. 새로운 노드를 위해 새 메모리를 할당하는게 아니라 기존에 있는 노드로 이동시키기 때문에 '분리'보다 비용이 적게 든다.

삭제는 B-트리의 방법과 동일하지만, 삭제될 자리로 옮길 잎 노드가 정해진 개수의 키 값을 갖지 않을 때 형제 노드로부터 키 값을 재분배한다. 재분배 할 수 없는 경우 노드를 합친다(3개 → 2개).


# B+트리
B-트리의 특징을 가지고 있지만, 모든 키 값들이 잎 노드에 정렬되어있는 트리 구조이다. 잎 노드를 순차적으로 연결하는 포인터 집합을 가지고 있다.

이런 특성 때문에 인덱스 된 순차 파일을 구성하는데 사용된다. 순차 처리 시 포인터를 이용할 수 있기 때문에 키 값을 모두 일일이 비교하지않고 다음 데이터에 접근해서 처리할 수 있기 때문이다.

따라서 모든 키 값은 잎 노드가 가지고 있으며, 키 값의 실제 데이터 주소도 잎 노드만 가지고 있다.

B-트리와 동일하게 루트와 잎 노드를 제외한 트리의 노드는 최소 ⌈m/2⌉개의 서브트리를 가져야 한다.
루트 노드 또한 최소 2개의 서브트리를 가져야 한다.
노드에 빈 자리가 있으면 삽입을 하고, 노드에 빈 자리가 없으면 노드를 분리하고 중간 값을 가진 노드를 부모 노드에 삽입한다.
삭제 시에는 잎 노드에서만 키 값을 삭제한다.
만약 삭제로 인해 잎 노드가 없어지게 되면 형제 노드를 확인해 형제 노드를 재분배해 작은 키 값을 삭제한 노드 위치에 둔다.
인접 형제 노드가 재분배 할 수 없으면 삭제할 키 값의 잎 노드와 형제노드를 병합한다.
B+ 트리의 검색,삽입,삭제
일반적인 노드 구조

n-1개의K와n개의 포인터 P(팬아웃)로 구성.  (Pi는 Ki를 가지는 레코드(i = 1 ~ n-1))

P1 | K1 | P2 | ··· | Pn-1 | Kn-1 | Pn

노드 안의 K값은 정렬된 순서로 유지. 한 노드에 저장되는 최대 포인터의 개수는 n.

## 검색
검색 연산은 순차 세트에 도달하여 K에 해당하는 레코드 포인터를 획득하는 것으로 종료.

예 : K값 JPL15에 대한 검색 연산 시행

n = 3, 탐색 시점의 노드는 Y
Y(루트노드)를 조사해서 JPL15과 같거나 JPL15보다 큰 K 중 가장 작은 K를 찾음.
K가 해당 노드에 아무것도 없기때문에 오른쪽 포인터를 따라가게 됨
중간 노드 진입, JPL15보다 큰 K 중 가장 작은 K 탐색
해당 K = POC12, POC12의 왼쪽 포인터를 따라감
단말노드 진입, 해당 노드의 처음부터 살펴서 JPL15가 있는지 확인
JPL15가 존재하므로 JPL15의 왼쪽 포인터에 접근해 블록에 담긴 레코드 탐색
5번 시점에 해당 노드가 단말노드가 아니면 1부터 반복.

## 삽입
레코드 삽입은 새로운 K에 대한 인덱스 엔트리를 반영하는 과정.

삽입 시 해당 노드에서 유지해야 할 K와 포인터 수가 증가하는지에 따라 노드 분할 여부가 나뉨.

예시 :  n = 3, K값은 ‘GGL12’만 존재. GGL22삽입 요청.

1.GGL22이 속해야 할 단말 노드 탐색. 새 K값을 저장해야 할 노드에 빈 공간이 남아있는지 탐색.

2.루트노드에 공간이 남아있으므로 삽입. 분할은 발생하지 않음.

3.노드 내의 K들의 순서 유지.


4.GGL50을 추가 삽입 요청

5.루트 노드에 저장 공간이 없으므로 분할 진행.(이유 : n= 3, 가능한 K 수 = 2)

6.분할 전 순서를 유지한 K 기준으로 부모 노드에 GGL22를 올림. (n은  3이기 때문에 1번째 index(2번째 K))

부모노드 선택 :

⌈n/2⌉=t 라고 정의. / t는 0부터 시작
n 이 홀수 : 상위에 t-1 번째 index
n 이 짝수 : 상위에 t 번째 index
자식 포인터 연결  :

부모노드의 왼쪽 자식노드는 부모노드보다 작게 연결 되어야 함.
오른쪽 자식노드는 부모노드와 같거나 크게 연결 되어야 함.
GGL22보다 작은 GGL12가 왼쪽 자식노드(단말노드). GGL22와 GGL50은 오른쪽 자식노드(단말노드)

7.GGL70, JPL15를 차례대로 삽입

8.JPL15 추가 시 부모노드에 추가할 공간이 없기 때문에 부모노드 레벨에서 분할 수행.(중간노드 생성, 루트노드는 GGL50)



## 삭제
레코드 삭제는 삭제할 K와 포인터를 포함하는 단말노드를 검색하고 해당 K와 포인터를 삭제하는 과정.

예 : GGL70 삭제



1.GGL70 검색 후 해당 K, 연관된 포인터 삭제

2.삭제한 엔트리의 오른쪽에 있는 엔트리들은 빈 공간이 발생하지 않게 왼쪽으로 이동.

GGL22, GGL24 차례대로 삭제


4.GGL12삭제

5.GGL12이 속한 노드가 공백상태가 됨 & K 개수도 ⌈(차수-1)/2⌉개 보다 적어짐.

6.다음 이웃 단말 노드인 GGL50, GGL51의 키를 재분배, JPL15의 부모노드를 재분배. (2번 과정 포함)



7.GPL24, POC12, JPL15를 차례대로 삭제

8.JPL15의 다음 이웃 단말 노드가 ⌈(n-1)/2⌉ 개보다 K값이 적음. GGL51과 이웃 단말 노드와의 병합.




# 출처
https://learning.oreilly.com/library/view/swift-data-structure/9781785884504/ch05s05.html
