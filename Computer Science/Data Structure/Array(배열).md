# 🟣 Array (배열)
배열이란, 각각의 Value(값)에 Index(인덱스)를 부여하여 해당 데이터를 불러오는 자료구조이다. Swift에서는 이를 Collection이라고 부른다.

## 🟪 Swift에서의 두 가지 Array
Swift에서는 두 가지의 array가 존재한다. swift에서 제공하는 우리가 평소 사용하는 Array가 있고, Foundation에서 사용하는 NSArray라는 것이 있다. (Objective-C문법이다)

이 두가지의 차이점은 다음과 같다.

|--| Array | NSArray |
|---|---|---|
|**타입**|구조체타입|클래스타입|
|**저장위치**| 스택(stack) | 힙 (Heap) |
|**요소 자료형**|모두 동일한 자료형만 저장 가능 | 인스턴스라면 타입 상관없이 가능 (Int, Double과같은 구조체 타입은 불가하지만, NSNumber같은 인스턴스로 저장 가능. 인스턴스이기만 하다면 NSNumber, NSString 상관없이 모두 저장가능|
|**Copy on wirte** | O | X |

이렇게 두 가지 형태가 있다는 것만 알아두자. 우리가 보통 사용하는 것은 거의 다 Array 이다!

## 🟪 Array의 생성 (swift)
#### 빈 배열 생성
```swift
var arr: Array<Int> = Array<Int>()
var arr = Array<Int>()
var = [Int]()

```

#### 기본 값을 가진 배열 생성
```swift  
var arr1 = [Int](repeating: 4, count: 3) // result: [4, 4, 4]
var arr2 = [3, 3, 3]
var arr3 = arr1 + arr2 // [4, 4, 4, 3, 3, 3] 왼쪽부터 오른쪽 순으로 배열이 합쳐짐
var arrString = ['apple']
var arrError = arr1 + arrString  // 두개의 형태가 다르기 때문에 error를 반환!
```

#### 배열의 크기 반환
```.count```로 배열의 크기를 구할 수 있다.
```swift
var arr = [2, 3, 2, 3]
arr.count // 4 출력
```

## 🟪 배열(Array)의 특징
### 📌 메모리의 연속성
<img width="656" alt="image" src="https://user-images.githubusercontent.com/96969693/183232717-12838bf7-8fff-424e-b3bb-6716112edd91.png">
> 이미지출처 : https://beginnersbook.com/2018/10/data-structure-array/
배열은 실제 메모리 상에서도 메모리가 순차적으로 저장된다. 따라서 어느 위치에 있는지 인덱스로 접근 가능하고, 손쉽게 처리가 가능한 것이다.

### 📌 자료형
배열은 선언될 때 모든 칸에 있는 value들은 동일한 Type을 갖는다.

### 📌 중복허용
배열은 값의 중복을 허용하는 자료형이다. 중복 허용을 하지 않기 위해서는, set(집합)을 이용하면 된다.

### 📌 확장 불가
배열은 메모리 할당 시 더 이상 길이를 늘릴 수 없다.

### 📌 배열의 장점
1. 배열은 인덱스를 사용해서 무작위 접근이 가능하어 검색 성능이 빠르다. 인덱스를 활용했기 때문에 접근성이 매우 높다.
2. 순차접근이 연결리스트보다 빠르다. (배열은 주소가 나열되어있기 때문에)
3. 추가적인 메모리 할당이 필요가 없다. (할당된 메모리만 사용하므로)

### 📌 배열의 단점
1. 메모리를 처음에 할당하면 이후 크기를 바꿀 수 없다. 사용하지 않는 공간이라도, 해당 메모리 공간을 차지하고 있어서 메모리 누수가 발생할 수 있다.
2. 자료의 삽입, 삭제가 어렵다. 인덱스를 사용하기 때문에 연결 리스트, 트리, 스택 등 다른 자료구조들에 비해서 삭제, 삽입이 힘들다.
3. 메모리를 재사용할 수 없다. (연결리스트와 같이 포인터로 구성되어 있는 구조라면, 해당 메모리를 해제하여 메모리를 재활용 할 수 있다.) 

# 🟣 배열과 관련된 간단한 알고리즘
## 📌 배열 회전 알고리즘
배열을 회전한다는 것은 오른쪽이든 왼쪽이든 특정 방향으로 원소들을 이동하는 것을 말한다. 아래그림처럼 말이다.

<img width="300" alt="image" src="https://user-images.githubusercontent.com/96969693/183284491-3c8be2d9-ba49-4e47-8d41-8d0afc677de2.png">

이렇게 배열을 회전시킬때 어떻게 코드를 작성해야할지 알아보자.

### 🟪 배열 값 이동 방법
새 배열을 만들어서, 원 배열의 i 번째 인덱스의 값을 새 배열의 i+n 인덱스에 집어 넣는다. 이때 i+n 이 배열의 길이를 넘길 수 있기 때문에 배열의 길이만큼 나머지 연산을 해주어야 한다.

```swift
func rotate(_ arr: [Int], _ n: Int) -> [Int] {
    if arr.isEmpty {
        return arr
    }
    let N = arr.count
    n %= N
    
    if n.isEmpty {
        return arr
    }
    
    var new_arr = Array(repeating: 9999, count: N)
    for i in 0..<N {
        new_arr[(i+n) % N] = arr[i]

    return new_arr
}
```
이렇게 작성하게 되면, ```rotate([1,2,3,4,5], 2)``` 를 입력하게 될 경우, ```[3, 4, 5, 1, 2]```가 출력된다.

### 🟪 역전 알고리즘 
어떤 배열에 있어서 배열을 좌우로 완전히 뒤집는 것을 'r (reverse)' 연산이라고 해보자. 이 'r' 연산자는 배열의 우측 상단에 제곱승수처럼 써 놓았다.

<img width="156" alt="image" src="https://user-images.githubusercontent.com/96969693/183286778-b03d24b1-cba3-46bc-a20b-e80453c06967.png">

이 방식은, 배열의 일부를 잘라서 Left, Right 로 나눈 후, 두 배열을 합쳐주고, 다시 뒤집는 알고리즘이다.

<img width="279" alt="image" src="https://user-images.githubusercontent.com/96969693/183286797-823b83a4-a835-4b2e-88d5-6a589c5e1491.png">

L(Left)와 R(Right) 각각을 뒤집은 뒤, 이것들을 합친 결과 전체를 다시 뒤집으면, 우리가 원하는 RL 결과가 나온다는 것이다. 확인해보자.

<img width="225" alt="image" src="https://user-images.githubusercontent.com/96969693/183286867-bf1bac56-22bf-4467-9c03-3cc3694bf491.png">

이 과정을 코드로 쓰면 아래와 같다.

```swift
func reverse(_ arr: [Int]) -> [Int] {
    var new_arr = [Int]()
    var n = arr.count
    
    for i in 0..<n {
        new_arr.append(arr[n-1-i])
    
    return new_arr
    
func rotate(_ arr: [Int], _ n: Int) -> [Int] {
    if arr.isEmpty {
        return arr
    }
    
    let N = arr.count
    n %= N
    
    if n.isEmpty {
        return arr
    }
    
    var right = [Int]()
    var left = [Int]()
    
    for i in 0..< N-n {
        left.append(arr[i])
    for i in N-n..<N {
        right.append(arr[i])
    
    var left_rev = reverse(left)
    var right_rev = reverse(right)
    
    return reverse(left_rev + right_rev)
}
```

이렇게 알고리즘을 작성하게 되면, ```rotate([1,2,3,4,5], 2)``` 를 입력하게 될 경우, ```[3, 4, 5, 1, 2]```가 출력된다. 아까 앞에서 배운 알고리즘과 같은 결과를 가져다주고, 방법만 다름을 알 수 있다.

### 🟪 저글링 알고리즘
우리가 처음에 배웠던 "🟪 배열 값 이동 방법"이 가장 간단해보인다. 하지만 이 방법은, 원 배열의 크기만큼 하나의 새로운 배열을 만들어서 그 배열에 값을 옮기는 방식이다. 이때 필연적으로 새 배열의 크기 N 만큼의 공간이 추가로 필요해진다. 만약 배열의 크기가 크고, 주어진 메모리가 넉넉하지 않다면 (임베디드 시스템이라던가..) N만큼의 공간이 부담이 될 수 있다.

이때 '저글링 알고리즘'은 필요한 공간을 1로 줄일 수 있는 알고리즘이다.

<img width="675" alt="image" src="https://user-images.githubusercontent.com/96969693/183287255-e7e1a4f4-fc19-4ba7-be41-b726e6c276d5.png">

위 그림은 크기가 12인 배열에서 3만큼 왼쪽으로 회전하는 경우를 나타낸 그림이다. 

배열을 arr이라고 할때 arr[0]을 T라는 변수에 저장한다. 그리고 인덱스를 0에서 회전횟수 (n 여기서는 3)만큼 씩 채워가면서, 3번째에는 0번째로, 6번째에는 3번째로, 9번째에는 6번째로 값을 옮긴다. 9에 3을 더한 12는 배열의 마지막 인덱스 11을 초과하기 때문에 멈춘 후 9번째 인덱스에 아까 저장한 T값을 옮긴다 이렇게 하게 되면 한 사이클이 끝난 셈이다.
이렇게 1차 사이클이 돌고 완성된 배열은 ```[4 2 3 7 5 6 10 8 9 1 11 12]```

그리고 그 다음 사이클을 진행해보자. arr[1]부터 시작하는데, 1에서 4, 7, 10까지 위와 같은 방식으로 진행된다. 사이클은 총 n 만큼 진행하게되고, 사이클이 모두 돌아가면, 최종적으로 우리가 원했던 n만큼 회전한 결과값을 얻을 수 있게 된다.

두번째로 사이클을 돌고 출력되는 arr는 ```[4 5 3 7 8 6 10 11 9 1 2 12]```
세번째로 사이클을 돌고 출력되는 arr는 ```[4 5 6 7 8 9 10 11 12 1 2 3]```
최종적으로 우리가 원하는 값이 출력될 것이다!

⚠️ 근데 이 사이클은 n번 반복하기 때문에, 배열의 길이가 n의 배수 일때만 쓸 수 있다. 위 경우는 배열의 길이 12, n 은 3이다. 그래서 사용가능했다. 하지만 우리가 지금까지 풀었던 예제 [1,2,3,4,5]는 배열의 길이는 5, n 은 2이다. 이 경우를 구분해주어야한다.

배열의 길이가 회전 횟수의 배수가 아닌 경우는, 한 사이클 내에 전부 처리할 수 있다. 배수일 때는 한 사이클이 모든 원소를 바꾸지 못하고 계속 반복 회전하는데 비해 배수가 아니면 필연적으로 모든 원소를 회전시키기 때문이다. (코드를 보고 이해해보자!)

이를 코드로 작성하면 아래와 같다.

```swift
func rotate(_ arr: [Int], _ n: Int) {
    // 1. base case 검사
    if arr.isEmpty {
        return arr
    }
    
    let N = arr.count
    n %= N
    
    if n.isEmpty {
        return arr
    } else if N % n == 0 {   // 2. 길이가 회전 횟수의 배수일 때 
        for last in 0..<n {
            var start = N - n + last
            var T = arr[start]
            var s = start
            
            while s - n >= 0 {
                arr[s] = arr[s-n]
                s -= n
            arr[last] = T
        }
    } else {    // 3. 아닐 때
        var s = 0
        let T = arr[s]
        for _ in 0..<N-1 {
            arr[s] = arr[(s-n) % N]
            s = (s-n) % N
        }
        arr[s] = T
    return arr
}

```

1. base case 검사
  - 배열이 비어있거나 길이로 모듈로한 회전 횟수가 0이면 그대로 반환한다. 연산할 이유가 없기 때문이다.

2. 배열의 길이가 회전 횟수의 배수 일 때
  - n번 사이클이 생기기 때문에 그 만큼 반복문을 돌려준다. 이 때 위 그림의 예제에서는 last가 차례대로 0, 1, 2 가 되는데 이 원소들을 last라고 한 이유는, 사이클의 마지막 원소를 T로 저장하고, 앞의 원소들을 차례대로 앞으로 옮기면서 마지막으로 last원소에 아까 정한 T를 집어넣기 때문이다.
  - start는 사이클의 마지막이 된다. 위 그림에서는 사이클의 인덱스가 각각 9, 10, 11 이 된다.
  - while문을 돌며 앞의 원소를 오른쪽으로 옮긴다. 마지막으로 last를 T에 넣는다.

3. 배수가 아닐 때
  - 첫 원소의 인덱스를 0으로 잡은 뒤, 그 때부터 n씩 왼쪽 원소를 오른쪽으로 옮긴다.
  - for 문의 횟수가 왜 N-1이냐면, 배열의 모든 원소를 바꿔야하기 때문에 기본적으로 N에 필요한데, 그중 한 번은 아까 저장한 T를 가져다가 쓸 것이기 때문에 반복문 이외의 할당식이 필요하다. 그래서 1을 빼주고, 마지막에 T를 갖다 붙여주었다.


이 알고리즘을 그대로 가져다가 쓰면, 우리가 원하는 ```[3, 4, 5, 1, 2]``` 가 출력될 것이다!


## 📝 Reference
[회전 알고리즘 참고](https://shoark7.github.io/programming/algorithm/5-ways-to-rotate-array)

