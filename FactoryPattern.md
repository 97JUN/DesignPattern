# Factory Pattern 이란?
공장의 생산라인을 바꾸는 것이 아니라 기본이 되는 생산라인을 만들어 놓고 요청이 들어오면 요청에 맞는 제품을 생산 해주는 패턴
Point! 공장은 어떤 요청이 들어올지 모른다.(AppleFactory라는 타입만 알고 IPhone인지 IPad인지 모른다)


## 예시코드
### Creator, Product 생성
```swift
// Creator
protocol AppleFactory {
  func createProduct() -> Product
}

// Product
protocol Product {
  func makeProduct()
}
```

### Concrete Creator, Product 생성
```swift
//Concrete Creator
class IPhoneFactory: AppleFactory {
  func createProduct() -> Product {
    return IPhone()
  }
}

class IPadFactory: AppleFactory {
  func createProduct() -> Product {
    return IPad()
  }
}

//Concrete Product
class IPhone: Product {
  func makeProduct() {
    print("IPhone 생산 완료")
  }
}

class IPad: Product {
  func makeProduct() {
    print("IPad 생산 완료")
  }
}
```

### 사용
```siwft

class Client {
  func order(factory: AppleFactory){
    let product = factory.createProduct()
    product.makeProduct()
  }
}

  let client = Client()
  client.order(factory: IPhoneFactory())
  client.order(factory: )
```
