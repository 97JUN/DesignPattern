## 어댑터 패턴

인터페이스를 클라이언트에서 요구하는 형태의 인터페이스를 적응 시켜주는 역할

한클래스의 인터페이스를 클라이언트에서 사용하고자 하는 다른 인터페이스로 변환한다. 어댑터를 이용하면 인터페이스 호환성 문제 때문에 같이 쓸 수 없는 클래스들을 연결해서 쓸 수 있다.


```swift
struct Token {
  let id: String
  let pw: String
}

protocol LoginService {
  func login()
}

class Authorization: LoginService {

  func submitUserInfo(userInfo: Token) {

  }

  func login() {
    print("기본 로그인을 실행합니다")
  }
}
//위 기존 로그인 기능에서 KaKao 로그인 기능을 연결 시켜주도록 한다. By Adapter

class KakaoLogin  {
  func tryLogin() {
    print("카카오 로그인을 시도합니다.")
  }
}

struct KakaoLoginAdaper: LoginService {
  let adaptee = KakaoLogin()

  func login() {
    adaptee.tryLogin()
  }
}
```

기존 로그인에 LoginService protocol을 채택한다음 인터페이스로 적응시키고 클라이언트에서 필요로 하는 용도로 변경하여 새로운 기능을 호환하도록 한다.

### 데코레이터 VS 어댑터
- 데코레이터 : 인터페이스를 바꾸지 않고 책임을 추가한다.
- 어댑터 : 인터페이스를 변경해서 클라이언트에서 필요로하는 인터페이스로 적응시키기 위한 용도로 호환성을 위해 사용.


