
```swift
protocol Beverage {
  var description: String { get set }
  func cost() -> Int
}

protocol BeverateDecorator {
  var beverage: Beverage { get set }
  init(beverage: Beverage)
}

class ColdBrew: Beverage {
  var decription: String = "콜드브루"
  func cost() {
    return 4500
  }
}

class Mocha: BeverageDecorator {
  var description: String = "모카"
  var beverage: Beverage

  init(beverage: Beverage) {
    self.beverage = beverage
    self.description = beverage.description + "" + self.description
  }

  func cost() -> Int {
    return beverage.cost() + 500
  }
}

let coldBrew = ColdBrew()
let mocha = Mocha(beverage: coldBrew)
```
- 장점
상속을 통한 하위 클래스를 만들지 안혹 객체의 기능을 확장
런타임에서 객체에 책임을 추가하고 제거 가능
객체를 여러 데코레이터로 합칠 수 있다
SIP 원칙 가능

- 단점
특정 래퍼를 제거 하기 어렵다
데코레이터 순서에 의존해야한다
코드 복잡도가 올라갈 수 있다.







