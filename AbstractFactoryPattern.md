# 추상 팩토리 패턴
Abstract Factory는 실제 객체가 정확히 무엇인지 알지 못해도 객체를 생성하고 조작할 수 있도록 해준다.
객체의 집합을 생성할때 유리한 패턴, 기존 팩토리를 한번 더 추상화 하여 서로 관련있는 제품군을 생성
Button, Label 만드는 Factory가 있을때 IPhone Button, label, IPad Button , Label 각각 만들도록


## 예시
```swift
// 추상화된 Factory
protocol UIFactoryable {
  func createButton() -> Buttonable
  func createLabel() -> Labelable
}

// 연관된 제품군을 실제로 생성하는 구체 Factory
final class IPadUIFactory: UIFactoryable {
  func createButton() -> Buttonable {
    return IPadButton()
  }
  
  func createLabel() -> Labelable {
    return IPadLabel()
  }
}

final class IPhoneUIFactory: UIFactoryable {
  func createButton() -> Buttonable {
    return IPhoneButton()
  }
  
  func createLabel() -> Labelable {
    return IPhoneLabel()
  }
}
```

```swift
//추상화된 Product

protocol Buttonable {
  func touchUp()
}

protocol Labelable {
  var title: String { get }
}

final class IPadButton: Buttonable {
  func touchUp() {
    print("IPadButton")
  }
}

final class IPhoneButton: Buttonable {
  func touchUp() {
    print("IPhoneButton")
  }
}

final class IPadLabel: Labelable {
  var title: String = "IPadLabel"
}

final class IPhoneLabel: Labelable {
  var title: String = "IPhoneLabel"
}
```
