# Proxy Pattern
프록시 클래스는 다른 무언가와 이어지는 인터페이스 역할을 하는 클래스

다른 객체에 대한 접근을 제어할 수 있도록 대리자를 제공할 수 있는 구조 패턴
Proxy가 원본 객체에 대한 접근을 제어하기 때문에 어떤요청이 원본객체에 전달되기 전이나 후에 작업을 수행할 수 있다.

Proxy는 어떤 객체가 존재하지만, 해당 객체를 바로 사용하기엔 부담스러운 경우 Proxy 객체를 통해 처리를 하고 객체가 반드시 필요한 시점에야 비로소 해당 객체를 생성해서 사용한다.

RealSubject에게 시간을 벌어주는 느낌. Real Subject가 너무 무거운 경우도 예시 중 하나.


### 사용예시

```swift
protocol DownLoadSubject {
  func downloadImage()
}

final class RealSubject: DownLoadSubject {

  func downloadImage() {
    print("다운로드")
  }

}

class Proxy: DownLoadSubject {
  private var realSubject: RealSubject?

  init(realSubject: RealSubject? = nil) {
    self.realSubject = realSubject
  }

  func downloadImage() {
    if realSubject == nil {
      realSubject = RealSubject()
    }
    realSubject?.downloadImage()
  }
}

// Usage example
let proxy = Proxy()
proxy.downloadImage()  // 출력: 다운로드
