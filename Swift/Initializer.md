# Swift Initializer

Swift의 객체는 자신이 가진 모든 stored properties들에 값이 있어야 한다.

1. Optional property에 값이 등록되지 않는다면, nil 값이 들어가게 된다
2. default value가 선언되어 있다면, 특별한 값을 할당하지 않아도 된다.
3. Constant property는 initializer에서만 값을 설정 할 수 있다.
4. struct는 각 property에 대한 memberwise initializer를 제공한다. 단, init 메서드를 별도로 작성한다면 member wise initializer는 사용할 수 없다.

### Initializer Delegation

Initializer가 다른 initializer를 호출하여, 인스턴스 생산을 완료하는 것.
Struct와 Class가 각 Initializer Delegation의 적용이 다르다

### struct

```swift
struct contact {
  let name:String
  let number:String
  init() {
    //Initializer delegation -> call: init(name, number)
    self.init(name:"John Doe", number:"000-0000-0000")
  }
  init(name:String, number:String) {
    self.name = name
    self.number = number
  }
}

```



### Class

Class type의 Initializer는 3가지 룰을 가지고 있다.

1. Designated initializer는 반드시 상위 Superclass의 Designated initializer를 호출 하여야 한다.
2. Convenience initializer는 반드시 동일 클래스의 initializer를 호출해야 한다.
3. Convenience initializer는 반드시 최종적으로 designated initializer를 호출해야 한다.

해당 룰을 그림으로 표현하면 아래의 그림과 같다.

![image-20210510163348881](/Users/sungminpark/Documents/iOS-Doc/iOS_DOC/Swift/res/Initializer/image-20210510163348881.png)

Superclass의 가장 오른쪽 convenience initializer는 다른 convenience initializer를 호출함으로 2번 규칙을 만족하며, 호출된 initializer는 최종적으로 designated initializer를 호출함으로 3번을 만족하게 된다.
Subclass의 경우 2개의 designated initializer는 Superclass의 designated initializer를 호출함으로 1번 규칙을 만족한다.

>이 룰은 class의 인스턴스가 생성되는 방법에는 상관이 없으며, 해당 룰에 따라 자신이 가진 initializer를 사용하여 완전히 초기화된 인스턴스를 생성하게 된다.
>상위 룰은 Initializer를 작성하는 방법에만 적용된다.

[Apple's The swift programming language(Swift 5.4)]: https://books.apple.com/kr/book/the-swift-programming-language-swift-5-4/id881256329

## 두 단계의 Initializaion



