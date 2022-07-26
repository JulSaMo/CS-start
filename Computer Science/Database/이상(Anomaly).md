// 20220823 <br>
// Brown
</br>
</br>

# 🟠 이상 (Anomaly)
```
좋은 관계형 데이터 베이스를 설계하는 목적 중 하나가 정보의 '이상현상(Anomaly)'이 생기지 않도록 설계하는 것
(정규화를 해야하는 이유는, 잘못된 테이블 설계로 인해서 이상현상이 생기기 때문이다.)
```

이상현상은, 세가지로 구성된다.
1️⃣ 갱신이상 (Modification Anomaly)
  - 반복된 데이터 중에 일부를 갱신할 때 데이터의 불일치가 발생하는 현상
2️⃣ 삽입이상 (Insertion Anomaly)
  - 불필요한 정보를 저장하지 않고서는 어떤 정보를 저장하는 것이 불가능한 현상 (내가 삽입하기 싫은 데이터도 넣어야만 할 때)
3️⃣ 삭제이상 (Deletion Anomaly)
  - 필요한 정보를 함께 삭제하지 않고서는 어떤 정보를 삭제하는것이 불가능한 현상

**즉, 이상현상은, 데이터의 중복성에 의해서 발생되는 데이터 불일치 현상이다.**

#### 예시를 살펴보자.

## 🔸 갱신이상(Modification Anomaly)
어떤 값을 업데이트 했을 때 그 속성의 다른 속성값들과의 불일치가 발생하는 현상이다.

<p align="center"><img width="365" alt="image" src="https://user-images.githubusercontent.com/96969693/186142580-b02e62c2-1b4d-4a7a-a94a-1b259ef6bc59.png"></p>

위와 같이 튜플의 이름을 '김소연'으로 바꿀 경우, 동일한 학번 100이라고 적혀있는 세번째 값은 그대로 '김사랑'이라고 남게되어, 불일치가 발생한다. 
이것이 발생되지 않게 하려면, '김사랑'이라는 값을 모두 찾아서 수정해주어야한다.

이렇게 무슨값을 update할 때 일어나는 불일치 현상을 의미한다.

### 📝 현재 이 데이터는 무슨 문제가 있을까? 어떻게 해결할까?

지금, 해당 데이터는 2NF가 이루어지지 않은 것으로 보인다. 하나의 컬럼이 하나의 value를 갖는 1NF는 만족되었지만, 완전함수종속을 만족하지 않는 것으로 판단된다.
완전함수종속이기 위해서는, 오직 PK만이 종속적인 관계를 갖도록 만들어주어야한다. 

2NF정규화를 통해 고쳐보자.

<p align="center"><img width="666" alt="image" src="https://user-images.githubusercontent.com/96969693/186144004-d0213289-8f90-4a98-a9c3-6d00780dadd6.png"></p>

이렇게 고쳤다. 이렇게 고침으로써, 오직 PK 만이 종속관계를 갖게되었다.


## 🔸 삽입이상(Insertion Anomaly)

내가 원하는 값만 테이블에 삽입하고 싶은데, 테이블에 필요하지 않은 필드들 때문에 원치 않는 필드까지 함께 삽입해야하는 경우이다.

<p align="center"><img width="634" alt="image" src="https://user-images.githubusercontent.com/96969693/186144601-2b673605-4058-4b26-a0b7-983a45881d12.png"></p>

나는 1,2,3번 필드에 대한 값만 테이블에 넣고 싶은데 테이블의 필드가 4개로 구성되어있기 때문에 마지막 필드값을 무엇을 넣어야할지 결정을 못하는 것이 삽입이상이다.

### 📝 이 문제도 정규화로 해결해보자.

이것도 마찬가지로 2NF 완전 함수 종속을 만족하지 못하는 것으로 판단되었다.

<p align="center"><img width="708" alt="image" src="https://user-images.githubusercontent.com/96969693/186148385-57b1b75e-5b0b-4378-8b3a-50b3de037cb6.png"></p>

그래서 이렇게 고쳤다. 사실 Faculty와 course code가 무슨관계인지 잘 이해가 안가고, 함게 묶여지는 관계가 모호하지만, 일단 Course code를 PK로 갖는 테이블로 한번 더 분해가 가능하다. 
이렇게 고치면 삽입이상이 해결된다! (빨간글씨가 삽입된 모습)


## 🔸 삭제이상 (Deletion Anomaly)
내가 원하느 ㄴ값만 테이블에서 삭제하고 싶은데, 하나의 튜플이 삭제를 원하지 않는 속성값도 갖고 있기 때문에 같이 지워져서 발생하는 문제이다.

<p align="center"><img width="453" alt="image" src="https://user-images.githubusercontent.com/96969693/186145588-c7a057cd-b9cc-45c2-8fef-5fcbd21dfcb1.png"></p>

그림처럼 '운영체제' 82점 이라는 정보만 삭제하고 싶은데, 이렇게 삭제하게 되면 102번 학생이 이선균이라는 정보도 함께 삭제된다.

### 📝 정규화로 해결해보자.
(그림의 오류: 김사랑 김소연 -> 김사랑임)
우선, 1NF는 만족하는 것으로 보이고, 2NF를 만족하는지 살펴보자. 아까 위에서 본 예제와 같다. 마찬가지로 2NF가 만족되지 않았다. 

<p align="center"><img width="666" alt="image" src="https://user-images.githubusercontent.com/96969693/186146031-6282c85e-f75d-45ff-808c-173819a60f27.png"></p>

이렇게 하게 되면, 운영체제 점수를 삭제해도, 이선균이라는 정보는 삭제되지 않는다.


**## (결론) 이렇게, 이상현상은 정규화를 통해 해결할 수 있다.**


# 📖 Reference
- [그림과 본문 일부](https://1000hg.tistory.com/22)


