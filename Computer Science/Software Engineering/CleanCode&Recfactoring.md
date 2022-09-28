# 클린코드와 리팩토링

## 클린코드란? (Clean Code)

### * 읽기 쉬운 코드가 클린 코드이다. *

```
“I like my code to be elegant and efficient.
The logic should be straightforward and make it hard for bugs to hide,
the dependencies minimal to ease maintenance, error handling complete according to an articulated strategy,
and performance close to optimal so as not to tempt people to make the code messy with unprincipled optimizations.
Clean code does one thing well.”

- Bjarne Stroustrup, inventor of ‘C++
```

  - C++의 창시자인 Bjarne Stroustrup은 C에는 객체 개념이 없기 때문에 객체지향 효과를 극대화하기 위해서 C++를 만든 것으로 유명합니다.
  - Bjarne Stroustrup은 위와 같이 클린코드에 대하여 정의했는데, 코드가 우아하다는 의미는 군더더기 없이 깔끔하다는 의미이고, 효과적이라는 것은 기능을 수행하는 코드를 최대한 작은 라인으로 구현한다는 의미로 보면 됩니다.
  - 또한 클린코드는 직접적이고 에러 처리가 잘 되어 있으며 하나의 역할을 수행한다고 합니다.

```
“Clean code is simple and direct. Clean code reads like well-written prose.
Clean code never obscures the designers’ intent but rather is full of crisp abstractions and straightforward lines of control.”

- Grady Booch, author of ‘Object-Oriented Analysis and Design with Applications’
```

  - Grady Booch는 James Rumbaugh, Ivar Jacobson과 함께 UML(Unified Modeling Language)을 창시한 사람입니다.
  - Grady Booch의 '클린코드가 단순하고 직접적이다’라는 말은 앞에서 설명한 내용과 동일한 의미입니다.
  - 또한 그렇게 함으로써 클린코드는 결코 원작자의 의도를 숨기지 않는다고 합니다.  
  
  
__이렇듯 Bjarne Stroustrup과 Grady Booch의 의견을 종합해 볼 때 클린코드의 가장 중요한 요소 중 하나는 가독성이라고 볼 수 있습니다.__  <br/>
__즉, 모든 팀원이 이해(understandability)하기 쉽도록 작성된 코드인 것이죠.__

## 클린코드 작성의 이유: 가독성 그리고 Technical Debt

### * 가독성은 왜 중요한걸까? *
  > 일반적으로 기존 코드를 변경하고자 할 때, 해석하는 시간과 수정하는 비율이 10:1이라고 합니다.
  > 예를 들면 코드를 변경하기 위해서 걸리는 전체 시간이 10시간이라고 하면, 사전에 코드를 분석하는 시간이 9시간 이상 걸린다는 말로 이해하면 쉬울 것 같습니다.

  > 그렇다면 해석이 어려운 코드는 그만큼 분석에 소요되는 시간이 더 오래 걸리겠죠?
  > 더욱이 대부분의 결함은 기존 코드를 수정하는 동안에 발생한다고 하니 이해하기 쉬운 코드야말로 오류의 위험성을 최소화하는 셈입니다.
  > 따라서 이해하기 쉽게 코드를 작성하는 것이 가장 중요하다고 볼 수 있습니다.

### * Technical Debt의 발생 *

  <img width="849" alt="스크린샷 2022-09-19 오후 4 43 09" src="https://user-images.githubusercontent.com/66079439/190971596-f6bf0ac1-b40b-4819-a21a-a82eaff28a72.png">
  
  > 이 그림을 보면 왜 클린코드를 작성해야 하는지에 대한 또 다른 설명이 될 것 같습니다. 변경 비용과 대응속도에 대한 이상치와 실제 프로젝트에서 발생하는 수치를 비교해 보았습니다.

  - 왼쪽의 그래프는 시간이 지나감에 따라 들어가는 변경비용으로, 이상적인 변경비용은 일관되게 낮지만 실제 변경비용은 증가함을 볼 수 있습니다.
  - 오른쪽의 그래프는 시간이 지나감에 따른 고객 요구사항의 대응속도로, 이상적인 대응속도는 일관되게 높지만 실제 대응속도는 점점 낮아짐을 볼 수 있습니다.

  > 이러한 차이가 생기는 이유는 프로젝트 초기에 클린코드로 개발하기 보다는 좀더 빠르고 쉬운 방법을 선택하기 때문입니다.
  > 대표적인 것이 'copy & paste'인데요. 이로 인하여 이상적인 변경 비용과의 차이가 나는 부분이 다음 그림의 Technical Debt입니다.
  > 즉 클린코드 작성을 위해 개발자들이 언젠가 해결해야 되는 부채인 셈입니다.

  <img width="605" alt="스크린샷 2022-09-19 오후 4 45 59" src="https://user-images.githubusercontent.com/66079439/190971720-02fe2b2a-6b9f-4651-873e-48a4d772918f.png">

## 클린코드 작성 원칙
<img width="876" alt="스크린샷 2022-09-19 오후 4 49 54" src="https://user-images.githubusercontent.com/66079439/190972369-df2201ee-e059-4848-88b3-276f6a6392ba.png">

  <br/>

  > 일반적인 사항으로는 다들 잘 알고 있는 것처럼 Coding 표준을 준수하고 단순하게 만들어서 가독성을 높이는 방법입니다.
  > Boy Scout Rule은 개발자로서 내가 담당하게 된 시스템을 내가 담당하기 이전의 코드보다 더 클린하게 만들자는 원칙인데요,
  > 그런 과정을 거치면서 대규모 레가시 코드들도 점점 더 클린해질 수 있겠죠?

  <br/>

<img width="873" alt="스크린샷 2022-09-19 오후 4 50 04" src="https://user-images.githubusercontent.com/66079439/190972398-d0c6deac-17fd-41bc-b374-df68263fc39a.png">

  <br/>

이 외에 클린 코드를 위한 고려사항들
  - 1. 의미 있는 변수명
  - 2. 명확하고 간결한 주석
    - 함수의 주요 세부사항은 주석으로 남기기 (함수 선언으로는 알 수 없는 내용들)
    - 보기 좋게 배치하고 꾸미기 (여러개의 그룹-문단으로 나누기) + 열 정렬
  - 3. 읽기 쉽게 흐름제어 만들기
    - 삼항 연산자는 꼭 필요할때만
    - do-while은 피하라
    - 부정문 보다는 긍정문을 사용하라
  - 4. 함수는 가급적 작게, 하나의 작업만 수행하도록


#### ** Swift 기준의 클린코드 예시는 아래 링크를 참고하면 좋을듯 **
 - https://ios-development.tistory.com/category/Clean%20Code%20%28%ED%81%B4%EB%A6%B0%20%EC%BD%94%EB%93%9C%29?page=2


## 리팩토링이란? (Refactoring)
  - 리팩토링은 외부 동작을 바꾸지 않으면서 내부 구조를 개선하는 방법으로, 소프트웨어 시스템을 변경하는 프로세스이다.
  - 소프트웨어를 보다 이해하기 쉽고, 수정하기 쉽도록 만드는 것,
  - 겉으로 보이는 소프트웨어의 기능을 변경하지 않는 것.

## 리팩토링의 목적
  - 리팩토링은 성능을 최적화시키는 것이 아니다.
  - 코드를 신속하게 개발할 수 있게 만들어주고, 코드 품질을 좋게 만들어준다.

## 리팩토링이 필요한 상황 및 코드
  - 상황: 소프트웨어에 새로운 기능을 추가해야할 때
  - 코드: 
    - 중복코드
    - 긴 메소드
    - 거대한 클래스
    - Switch문
    - 절차지향으로 구현한 코드

## 리팩토링의 과정
####  테스트
      - 현재 작동하는 코드들이 정상적으로 작동하는 것을 유지하되,
      - 내부적으로 코드를 개선해 이해하고 수정하기 쉽게 만드는 작업
####  함수 쪼개기
      - 추상화 수준을 높여 같은 일을 하는 것들을 추출하라
      - 추출한 것들을 따로 함수로 만들어 함수는 최대한 작게 만들어라
####  임시 변수 제거하기
      - 임시변수란 값이 한 번만 대입되고 변경되지 않는 변수이다.
      - 임시변수는 과감히 지우고 부수효과를 테스트하자.

## 클린코드와 리팩토링의 차이??
  - 비슷하지만 리팩토링이 클린코드에 비해 조금 더 큰 개념이라고 볼 수 있다.
  - 클린 코드는 단순하게 가독성을 높이기 위한 작업이라면,
  - 리팩토링은 클린 코드를 포함하여 유지보수를 위한 코드의 개선이라고 볼 수 있다.
  - 클린 코드와 같은 부분은 설계단계에서 잘 이루어져 있는 것이 중요하고, 리팩토링은 결과물이 나온 이후 수정이나 추가 작업이 진행될 때 개선해 나가야 한다.


## Reference
  - Clean Code - Robert C Martin
  - Clean Code Cheat Sheet - Urs Enzler
  - https://www.samsungsds.com/kr/insights/cleancode-0823.html
  - https://beforb.tistory.com/3#recentEntries
  - https://ablue-1.tistory.com/83

