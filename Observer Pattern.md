## Observer Pattern 이란?
 Observer Pattern은 한 객체의 상태가 바뀌면 그 객체에 의존하는 다른 객체들에게 연락이 가고 자동으로 내용이 갱신되는 방식으로 일대다 의존성을 정의한다.
신문 구독으로 생각을 하면  신문사: Subject 구독자: Observer
대부분 주제 인터페이스와 옵저버 인터페이스가 들어있는 클래스 디자인을 바탕으로 한다.

## Observer Pattern 은 언제 사용할까?
다른 객체의 상태가 변경될 때마다 어떤 행동을 하고 싶다면 옵저버 패턴을 사용하면 된다.

## Observer Pattern의 결과

### 장점
OCP 를 지킬 수 있다.
Subject의 코드를 수정하지 않고 새로운 Observer 클래스를 추가할 수 있다.
런타임에서 객체간 관계를 설정할 수 있다.

### 단점
Observer에게 알림이 가는 순서는 보장 못한다.
Observer, Subject간 관게가 잘 정의되지 않으면 원하지 않는 동작이 발생할 수도 있다.



## 예시 코드
```swift
protocol Subject {
  var observers: [Observer] { get set }
  func registerObserver(observer: Observer)
  func removeObserver(observer: Observer)
}

protocol Observer {
  var id: String { get set }
  func update(temp: Float,
              huidity: Float,
              pressure: Float)
}

protocol Display {
  func display()
}

class WeatherData: Subject {
  var observers: [Observer] = []
  private var temp: Float = 0
  private var huidity: Float = 0
  private var pressure: Float = 0

  func registerObserver(observer: Observer) {
    self.observers.append(observer)
  }

  func removeObserver(observer: Observer) {
    if let index = self.observers.firstIndex(where: { $0.id == observer.id }) {
      self.observers.remove(at: index)
    }
  }

  func notifyObservers() {
    for observer in observers {
      observer.update(temp: self.temp, huidity: self.huidity, pressure: self.pressure)
    }
  }
}

class WeatherDisplay: Observer, Display {
  var id: String

  private var temp: Float = 0
  private var huidity: Float = 0
  private var pressure: Float = 0

  init(id: String) {
    self.id = id
  }

  func update(temp: Float, huidity: Float, pressure: Float) {
    self.temp = temp
    self.huidity = huidity
    self.pressure = pressure
    display()
  }

  func display() {
    print("\(id)의 온도는\(temp) 습도는\(huidity) 기압은\(pressure) 입니다")
  }
}

let hyunjunWeatherDisplay = WeatherDisplay(id: "hyunjun")
let weatherStation = WeatherData()
weatherStation.registerObserver(observer: hyunjunWeatherDisplay)
weatherStation.notifyObservers()
```


