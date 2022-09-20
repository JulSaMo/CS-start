// 2022.09.20

## DevOps란?

### 정의

Development + Operation 을 이은 말로, 소프트웨어 개발자와 정보기술 전문가/(소프트웨어 운영팀) 간의 소통, 협업 및 통합을 강조하는 개발 환경이나 문화를 의미함. 

### 목적

소프트웨어 제품과 서비스를 **빠른 시간에 개발 및 배포하는 것**

결국, 소프트웨어 제품이나 서비스를 알맞은 시기에 출시하기 위해 개발과 운영이 상호 의존적으로 대응해야 한다는 의미로 많이 사용하고 있다.

---

**근데 뭔지 알겠는데… 갑자기 이게 왜 나온거지??**

### 데브옵스 등장 배경

**데브옵스는 결국에는 애자일처럼 프로덕트를 좀 더 빠르게 발전시키기 위해 고안된 개발 문화이다.**

프로덕트를 만들면, 그 프로덕트를 안정적으로 운영하는 팀과 좀 더 기능적으로 개발하는 팀으로 나뉜다. 

그러면 당연히 새로운 기능을 추가하려면 안정적인 운영에 빈틈이 생길 수 밖에 없고… 그래서 운영팀과 개발팀 사이에 갈등이 생기게 되며 프로덕트의 발전은 더디게 된다. 

**그럼 어떡하면 될까??**

개발하는 순간부터 운영까지 고려해서, 새로운 기능을 추가할 때 케어해줘야하는 운영 부분들을 자동화시키면된다.  구성원들이 최대한 개발과 운영의 본질적인 부분에만 집중할수있게 통하환경과 자동화된 시스템을 도입해주면 된다. 이러한 문제로 부터 도커와 쿠버네티스 같은 툴이 나오게 된 것이다! 

 이렇게 개발팀과 운영팀이 나뉘어지지않고 하나의 팀이되어 개발 - 배포 - 운영 등의 작업을 원툴로 관리하는 문화를 데브옵스라고 한다.
 
 <img width="735" alt="image" src="https://user-images.githubusercontent.com/103009135/191184447-05b552f9-354e-48ec-afb6-424e6c7d26f0.png">

### 예시

실제로 AWS 홈페이지에 가보면 데브옵스에 대한 설명과 더불어 기업에서 데브옵스를 채택하기 위한 툴을 제공하고 있다.
<img width="725" alt="image" src="https://user-images.githubusercontent.com/103009135/191184553-8bf26939-e55a-4c2b-985c-b2fa10395f72.png">.  
https://aws.amazon.com/ko/devops/resources/.  


### More

데브옵스의 개념은 애자일 기법과 지속적 통합의 개념과도 관련이 있다.

- **[#](https://gyoogle.dev/blog/computer-science/software-engineering/DevOps.html#%E1%84%8B%E1%85%A2%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AF-%E1%84%80%E1%85%B5%E1%84%87%E1%85%A5%E1%86%B8)애자일 기법**
    
    실질적인 코딩을 기반으로 일정한 주기에 따라 지속적으로 프로토타입을 형성하고, 필요한 요구사항을 파악하며 이에 따라 즉시 수정사항을 적용하여 결과적으로 하나의 큰 소프트웨어를 개발하는 적응형 개발 방법
    
- **[#](https://gyoogle.dev/blog/computer-science/software-engineering/DevOps.html#%E1%84%8C%E1%85%B5%E1%84%89%E1%85%A9%E1%86%A8%E1%84%8C%E1%85%A5%E1%86%A8-%E1%84%90%E1%85%A9%E1%86%BC%E1%84%92%E1%85%A1%E1%86%B8)지속적 통합**
    
    통합 작업을 초기부터 계속 수행해서 지속적으로 소프트웨어의 품질 제어를 적용하는 것
    

---

## Reference

[https://m.blog.naver.com/ydot/221536323043](https://m.blog.naver.com/ydot/221536323043) (데브옵스 배경)

[https://machyobe.tistory.com/entry/많은-기업들이-Devops-엔지니어를-뽑는-이유는-무엇일까](https://machyobe.tistory.com/entry/%EB%A7%8E%EC%9D%80-%EA%B8%B0%EC%97%85%EB%93%A4%EC%9D%B4-Devops-%EC%97%94%EC%A7%80%EB%8B%88%EC%96%B4%EB%A5%BC-%EB%BD%91%EB%8A%94-%EC%9D%B4%EC%9C%A0%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C) 

[https://www.youtube.com/watch?v=_VEds_73Guc](https://www.youtube.com/watch?v=_VEds_73Guc)
