# 추상 팩토리 패턴
Abstract Factory는 실제 객체가 정확히 무엇인지 알지 못해도 객체를 생성하고 조작할 수 있도록 해준다.

## 추상 팩토리 패턴의 목적
구체적인 클래서를 지정하지 않고 관련된 객체들을 모으기 위한 인터페이스를 제공하는 것이다.
또한 코드를 변경하지 않고도 조건에 따른 적절한 객체를 사용할 수 있게 해준다.

## 등장 배경
UI 만들때 버튼, 스크롤 바과 같은 뷰를 사용해서 만들때 모두 다른 모양과 동작을 하지만 모두 연관되어 있다고 생각되어서 각자 다른 객체로 만들면 이후 수정이 어려워 지기 때문에 이러한 객체들을 표현하는 하나의 추상 클래스를 정의하여 해결하기 위해서 생성됨.

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
