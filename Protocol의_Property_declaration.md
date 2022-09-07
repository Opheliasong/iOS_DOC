# Protocol의 gettable Property만 있을 경우의 짧은 이야기 #

Swift의 Protocol은 swift를 사용하면서 꽤 많이 사용하거나 만나게 되는 선언자로 swift.org의 설명대로 blueprint로써의 의미가 크다.<br>
Protocol은 명시적인 함수의 내용을 담을 수 없고, 명시적인 computed property 역시 가질수 없다.
라고 생각하기 쉽지만 사실 extension으로 확장할 경우 기본값 설정 및 프로토콜의 동작의 내용을 어느정도 정의 할 수 있다.


우선 Protocol의 property 중 getter 와 setter에 관해서 살짝 살펴보자면

```  swift
protocol Tech {
    var language:String { get }
    var grade:String { get set }
}

struct LowLevelSwiftTech: Tech {
    init() {
        language = "Swift"
        grade = "Low"
    }
    
    let language: String
    var grade: String
}

struct MidLevelSwiftTech: Tech {
    init() {
        language = "Swift"
        grade = "Mid"
    }
    
    var language: String
    var grade: String
}
```
위와 같이 Tech 프로토콜을 준수하는 LowLevelSwiftTech와 MidLevelSwiftTech 구조체를 선언하였다.<br>
Tech Protocol의 language는 getter만 있는 property이니 var이 가능할까? <br>

정답은 아무런 문제없이 컴파일이 된다.

``` swift
var low:LowLevelSwiftTech = LowLevelSwiftTech()
var mid:MidLevelSwiftTech = MidLevelSwiftTech()

low.language = "Java"
mid.language = "CPP"
```

그럼 다음과 같이 low와 mid라는 객체로 각각 명시적인 구조체 객체로 생성한 후, language에 접근한 코드의 경우 컴파일 에러가 몇개가 발생할까? <br>

정답은 1개이다.
(low 객체의 경우 상수에 할당할고 하니 당연히 불가)

그럼 다음과 같이 객체의 생성자가 변경된다면? <br>
``` swift
var low:Tech = LowLevelSwiftTech()
var mid:Tech = MidLevelSwiftTech()

low.language = "Java"
mid.language = "CPP"
```

명확한 객체의 타입을 사용하지 않고 protocol로 받아 업케스팅 후 사용한다면? <br>
둘 다 컴파일 에러가 발생한다.<br>

당연하게 프로퍼티가 오버라이딩 되었으니까 가능한거 아닌가? 라는 생각이 들때 swift는 타입에 민감하고 이를 통해 safe하다면 protocol을 준수하는 type읆 만들때 조금 더 민감하게 주의를 줘야 하는 것이 아닐까? 라는 생각이 들었다.

그럼 반대로 gettable property가아닌 gettable & settable property의 경우 상수로 사용이 가능할까?

``` swift
protocol Tech {
    var language:String { get set }
    var grade:String { get set }
}

struct LowLevelSwiftTech: Tech {
    init() {
        language = "Swift"
        grade = "Low"
    }
    
    let language: String
    var grade: String
}
```
위와 같이 Tech 프로토콜의 language 프로퍼티를 gettable & settable로 수정하게 되면
```
error: type 'LowLevelSwift' does not conform to protocol 'Tech'
```
이런 에러를 만나게 된다. <br>
gettable & settable의 경우 gettable만 가능한 프로퍼티 조금 더 조건이 생기는 셈이다.<br>
protocol의 프로퍼티에 getter만 선언한 뒤, setter는 가능하지 않는 형태의 property로만 한정적으로 하였다면<br>
'해당 프로토콜을 사용하는 사용자는 다르게 사용할 가능성도 있다.'는 생각을 배제한다면?<br>

클래스의 경우 final 키워드를 사용하여 오버라이딩을 막을 수 있지만 protocol은? <br>
이게 protocol을 '준수'하는것이 맞는건가? <br>
이런 생각을 잠시하게 되었다.
