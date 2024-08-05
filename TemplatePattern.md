# 템플릿 패턴이란?
템플릿 메서드 패턴은 단계적인 과정을 가지고 있는 알고리즘을 추상적으로 정의하고, 그 중 일부를 서브 클래스에서 필요에 따라 직접 구현할 수 있게 한다.

## 언제사용?


```swift
protocol SignUp {
  func register()

  func checkName()
  func checkID()
  func checkPW()
}

extension SignUp {

  func register() {

    checkName()
    checkID()
    checkPW()

  }

  func checkName() {
    print("이름체크")
  }

  func checkID() {
    print("ID 체크")
  }

  func checkPW() {
    print("PW 체크")
  }
}


final class NaverSignUp: SignUp {

  func checkID() {
    print("네이버 이메일 형식인지 확인하세요")
  }
}


let naver = NaverSignUp()
naver.register()
```
