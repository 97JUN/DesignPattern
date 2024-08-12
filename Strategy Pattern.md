App에서 달라지는 부분을 찾아내고, 달라지지 않는 부분으로부터 분리 시킨다.

오리 -> 날 수 있는 오리와 날지 못하는 오리로 나뉘기 때문에 날다를 분리 시킨다.


- 전략 패턴을 적용하기 전


```swift

class Duck {
  func fly() {
    print("날고 있어요")
  }

  func sound() {
    print("꽥 꽥")
  }
}

class BlueDuck: Duck {
  override func fly() {
    print("저는 계속 날 수 있어요")
  }
}

class RubberDuck: Duck { //날수 없는 RubberDuck 이지만 fly() 메소드를 재정의 하지 않았다.
  override func sound() {
    print("꽥꽥")
  }
}

let myDuck = RubberDuck()
myDuck.fly()
//날지 못하도록 설계하려고 했지만 fly()가 가능해 지는 오류가 발생
```
- 전략 패턴을 사용한 후

```swift

class Duck {
  var flyBehavior: Flyable?

  func setFlyBegavior(flyBehavior: Flyable) {
    self.flyBehavior = flyBehavior
  }

  func doFly() {
    flyBehavior?.fly()
  }
}

class CantFly:Flyable {
  func fly() {
    print("저는 날 수 가 없어요")
  }
}

class FlyWithWings:Flyable {
  func fly() {
    print("저는 날개로 날아요")
  }
}

let myDuck = RubberDuck()
myDuck.setFlyBegavior(flyBehavior: CantFly())
myDuck.doFly()
```
이렇게 fly() 를 분리하여 상속으로 인해 발생할 수 있는 문제를 해결할 수 있고 런타임에서 동작을 쉽게 변경할 수 있게 된다.


### 전략 VS 상태 패턴 

상태 패턴과 전략패턴은 둘 다 인터페이스와 클래스를 활용하여 하나의 인스턴스가 상태를 변경하거나 전략을 변경하여 유연한 코드를 제공합니다.
 
둘의 가장 큰 차이로는 내부적으로 상태가 변하는가 변하지 않는가입니다.
상태 패턴에서는 하나의 객체가 상태에 따라 내부적으로 상태를 변경합니다.
전략 패턴은 작업을 수행하기 위해 다양한 전략을 선택하지만 객체 내부 상태는 동일하게 유지합니다.
