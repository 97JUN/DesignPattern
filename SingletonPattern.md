# 싱글턴 패턴이란?

싱글턴을 사용하여 유일한 객체를 만든다
싱글턴은 특정 클래스의 인스턴스가 오직 하나임을 보장받는 객체이다.

## 언제 사용할까?

주로 앱 전체에 걸쳐서 유일한 객체를 만들기 위해서 사용한다.
어디에서나 전역적으로 접근할 수 있는 유일한 객체(UserDefaults, NotificationCenter, URLSession 등)

```swift
class MilkStore {
  static let shared = MilkStore()
  private var chocolateMilkeCount = 100
  private var strawberryMilkeCount = 100
  private var bananaMilkeCount = 100

  private init() {}

  func checkMilkStock() {
    print("남은재고: 초코:\(self.chocolateMilkeCount),딸기:\(self.strawberryMilkeCount),바나나: \(self.bananaMilkeCount)")
  }
}
```

## 장단점
 - 장점: 유일한 객체를 만들어서 다양한 객체들에게 공유되는 객체를 만들 수 있다는 장점이 있다. 또한 재사용이 가능하여 메모리 낭비를 방지.

 - 단점: 객체지향 관점에서 인스턴스들 간에 결합도가 높아져서 OCP 원칙을 위배하게 된다.
