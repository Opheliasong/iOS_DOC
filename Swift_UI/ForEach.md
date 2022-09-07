<b> Structure </b>
# ForEach 
해당 구조체는 구분이 가능한 데이터로 구성된 콜렉션들을 위임으로 계산 할 수 있도록 도와주는 구조체이다.

## 선언 형식
~~~ swift
struct ForEach<Data, ID, Content> where Data : RandomAccessCollection, ID : Hashable
~~~

## 둘러보기
ForEach는 임의로 접근이 가능한 콜렉션들을 View들로 제공하는데 사용된다. 
해당 콜렉션의 원소들은 Identifiable 인터페이스를 준수하거나, ForEach 생성자의 <i>id</i> 매개변수를 제공해야 한다.

ForEach를 사용하는 이유는 동적으로 특정 Range만큼 혹은 콜렉션들의 원소들 만큼 동일한 View를 생성하기 위하여 사용하는 경우일 것이다.
아래의 예시는 가장 흔하게 보는 Identifiable을 가지는 콜렉션들을 활영하여 Text View를 생성하는 구문이다.

~~~ swift
private struct NamedFont: Identifiable {
    let name: String
    let font: Font
    var id: String { name }
}

private let namedFonts: [NamedFont] = [
    NamedFont(name: "Large Title", font: .largeTitle),
    NamedFont(name: "Title", font: .title),
    NamedFont(name: "Headline", font: .headline),
    NamedFont(name: "Body", font: .body),
    NamedFont(name: "Caption", font: .caption)
]

var body: some View {
    ForEach(namedFonts) { namedFont in
        Text(namedFont.name)
            .font(namedFont.font)
    }
}
~~~
NamedFont 구조체의 경우 id를 name 프로퍼티를 활용하여 Identifiable을 구현하였다.

