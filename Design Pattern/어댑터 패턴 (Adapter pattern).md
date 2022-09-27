// 2022.09.27 Brown
<br>
<br>

# 🟣 어댑터 패턴 (Adapter Pattern)

```
- 서로 다른 인터페이스를 가진 객체를 함께 사용할 수 있도록 해주는 디자인 패턴
- Object Adapter 와 Class Adapter가 있다.
```

## 😈 Object Adapter

<p align="center"><img width="500" alt="image" src="https://user-images.githubusercontent.com/96969693/192471410-32e8906e-3505-4355-9d1b-842c1af321e5.png"></p>

- Client: 프로그램의 기존 로직을 포함하는 클래스이다.
- Target: 다른 클래스가 현재 로직에 포함되려면 따라야하는 프로토콜이다. (Client가 사용중인 인터페이스)
- Adaptee: 현재 존재하는 클래스가 아닌 외부에서 가지고온 유용한 클래스이다. 따라서 인터페이스가 다르기 때문에 바로 사용할 수가 없다.
- Adapter: 이러한 Client, Adaptee를 모두 사용할 수 있도록 도와준다. Adapter는 Client, Adaptee 객체를 모두 다룰 수 있고, Adaptee 객체를 Client 인터페이스로 래핑하거나 Client객체를 Adaptee 클래스가 사용할 수 있는 형식으로 변환한다.
- Adpater를 사용하면 기존 client 코드를 수정하지 않고도 새로운 클래스를 사용할 수 있다.


## 😈 Class Adapter

<p align="center"><img width="425" alt="image" src="https://user-images.githubusercontent.com/96969693/192472323-6a5cd184-99bb-41a9-9646-a9b056d5480f.png"></p>

- 다중 상속을 지원하는 언어에서, Adapter는 위와 같이 여러 개의 인터페이스를 상속하여 여러 클래스에서 동작 가능한 Adapter를 만들 수 있다.
- 이렇게 되면, Object Adapter와는 다르게 객체를 래핑해서 변환할 필요 없이 어댑터 내부에서 처리하게 된다.


# 🟣 어댑터 패턴은 언제 쓰나?

## 😈 문제 예시 상황




