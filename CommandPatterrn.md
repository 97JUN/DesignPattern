# 커맨드 패턴

행위 패턴 중 하나로 실행될 기능을 캡슐화 함으로써 주어진 여러기능을 실행할 수 있는 재사용성이 높은 클래스를 설계하는 패턴
요구하는 객체와 요구를 받아들이고 처리하는 객체를 분리
-> 작업을 캡슐화 해서 Receiver에게 보내서 처리하고 싶을때

```swift

//명령 정의
protocol Command {
  func excute()
}

//호출자 구현
class RemoteControl {

  var redButton: Command?

  func setCommand(redButton: Command) {
    self.redButton = redButton
  }

  func turnOnTv() {
    redButton.execute()
  }
}

//작업 캡슐화
struct TurnOnTV: Command {
  var tv: TV?

  init(tv: TV) {
    self.tv = tv
  }

  func execut() {
    tv.turnOn() //Receiver에게 요청
  }
}

//Receiver가 동작하도록

struct TV{
  func turnOn() {
    print("turn on TV")
  }

}
```

### 전략패턴 VS 커맨드패턴

- 전략: 하고자 하는 것은 정해져 있고, 어떻게 할지(fly())
- 커맨드: 어떻게 할지에 대한 방법은 외부에서 정의 후 주입. 정의한걸 실행하는 것이 중요 캡슐화된 행위를 전달 받음.
