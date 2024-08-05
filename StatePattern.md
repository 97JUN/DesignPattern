# 상태패턴
런타임에서 내부의 상태가 변경될 때 객체가 동작을 변경할 수 있도록 하여 마치 객체가 클래스를 변경하는 것처럼 보이게 하는 패턴


### 예시
유튜브 구독 상태를 Youtube 클래스의 property로 상태로 저장후 상태와 관련된 클래스를 교체 해주는 방식

```swift
protocol State {
  func goBackground()
  func playMusic()
  func videoDownload()
}

class Youtube {

  private var preminumState: State

  init(preminumState: State) {
    self.preminumState = preminumState
  }

  func subscribe() {
    self.preminumState = SubscribeState()
  }

  func unSubscribe() {
    self.preminumState = UnSubscribe()
  }

  func goBackground() {
    self.preminumState.goBackground()
  }

  func playMusic() {
    self.preminumState.playMusic()
  }

  func videoDownload() {
    self.preminumState.videoDownload()
  }
}
```




```swift
class SubscribeState: State {
  func goBackground() {
    print("백그라운드에서도 비디오 재생")
  }

  func playMusic() {
    print("백그라운드에서도 음악 재생")
  }

  func videoDownload() {
    print("다운로드가능")
  }
}

class UnSubscribe: State {
  func goBackground() {
    print("백그라운드에서 비디오 재생불가")
  }

  func playMusic() {
    print("백그라운드에서 음악 재생불가")
  }

  func videoDownload() {
    print("다운로드 불가")
  }
}
```




```swift
let youtube = Youtube(preminumState: UnSubscribe())
  youtube.goBackground()
  youtube.playMusic()
  youtube.videoDownload()

  youtube.subscribe()

  youtube.goBackground()
  youtube.playMusic()
  youtube.videoDownload()
```
