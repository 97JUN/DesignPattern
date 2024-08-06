# 반복자 패턴 이란?
 컬렉션의 내부 구현을 노출하지 않으면서 컬렉션의 모든 요소에 접근할 수 있는 방법을 제공하는것
 -> 실제로 사용되는 컬렉션이 배열인디, 리스트인지 와 같은 실제 구조와 상관 없이 각 원소들에 접근을 가능하게 만든다.

## 언제사용할까?
- 특정 타입을 for-in loop를 사용하는 등 타입안의 요소들을 순회하고 싶을때
- Collection 타입이 복잡한 데이터 구조를 가지고 있어 사용에 대한 편의성이나 보안을 위해 타입의 내부 구현을 숨기고 싶을 때
- 객체를 순회하는 알고리즘이 간단하지 않아 해당 코드를 별도로 분리해 책임을 명확히 하고 싶을때
- 내가 원하는 방식(앞에서 2개씩 건너뛰기 등)으로 객체의 요소를 순회하고 싶을떄

 ```swift
struct Food {
    let name: String
}

struct Foods {
    let foods: [Food]
}

struct FoodsIterator: IteratorProtocol {
    private var current = 0
    private let foods: [Food]

    init(foods: [Food]) {
        self.foods = foods
    }

    mutating func next() -> Food? {
        defer { current += 1 }
        return foods.count > current ? foods[current] : nil
    }
}

extension Foods: Sequence {
    func makeIterator() -> FoodsIterator {
        return FoodsIterator(foods: foods)
    }
}
  // Iterator 사용 - Client
  let favoriteFoods = Foods(foods: [Food(name: "마라탕")])

  for food in favoriteFoods {
    print("나는 \(food)을/를 좋아해!")
  }
```

이렇게 하면 for Loop를 돌리지 못하던 struct도 순회가 가능하다
