# CGColor vs UIColor

## CGColor

CGColor는 CoreGraphics의 색을 표현하기 위한 데이터로, 연산을 위한 함수들도 제공하고 있다.
색을 정확하고 빠르게 관리하기 위한 함수를 제공하고 있다.
특정 컬러들은 재사용을 하고 있다(텍스트를 위한 검은색).
일반적으로 CGColor는 CGLayer, CGImage와 같은 Core Graphics 객체들의 색을 적용하기 위한 연산에 사용된다.

## UIColor

UIColor는 색 정보와 Alpha 값과 같은 정보를 담고 있으며, 커스텀된 그리기 처리에 활용된다
UIColor의 경우 일반적으로 내부적으로 CoreGraphics 색 영역(CGColorSpace)에서 CGColor으로 표현되게 된다.
일반적으로 UIColor는 UIImage, UIView 등등과 같은 UIKit 인터페이스의 원소들에서 색을 적용하기 위한 연산에 사용된다.