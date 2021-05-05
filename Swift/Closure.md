# Closure

## Closure는 Reference type이다

아래의 예시 코드를 보면 incrementBySeven과 incrementByTen은 상수로 선언이 되어있다.
하지만 closure가 참조하는 runningTotal 변수가 캡쳐되어 여전히 증가하고 있음을 알 수 있다.
이는 closure와 함수는 reference type으로 동작하기 때문이다.

```swift
1. let alsoIncrementByTen = incrementByTen
2. alsoIncrementByTen()
3. // returns a value of 50
4. 
5. incrementByTen()
6. // returns a value of 60
```

함수나 closure를 상수나 변수로 선언을 하였을때, 함수나 closure에 대한 참조로만 동작하게 된다.
실제로. alsoIncrementByTen은 상수로 참조를 하고 있으며, closure의 내부의 모든 내용들이 상수화 되지는 않는다.
이 의미는 closure를 두개의 상수나 변수로 할당 하더라도, 동일한 closure를 참조하게 되는 것을 말한다.
위 예시의 alsoIncrementByTen을 호출 후 incrementByTen을 호출 하였을때, 마치 incrementByTen을 두번 호출 한 것과 같은 결과가 되는 것을 알 수 있다.



[ref: Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Closures.html)



