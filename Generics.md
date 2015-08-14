### Generics

 Generics code는 재사용 가능한 함수와 당신이 정의하는 요구사항에 따른 타입, 어떠한 타입이라도 동작할 수 있는 타입을 유연하게 작성할 수 있다. 당신은 중복을 피하고, 의도를 분명하게 표현하고, 추상적 방식으로 code를 작성할 수 있다.

 Generics는 Swift의 가장 강력한 특종 하나다, Swift의 표준 라이브러리는 generic code로 설계됐다. 사실은, generics는 Language Guide 처음부터 끝까지 사용됐으며, 심지어 그것을 인식 하지 못할 수 있다. 예를 들어 Swift의 Array와 Dictionary 타입 둘다 generic 콜렉션이다. 당신은 Array에 Int 값을 묶거나 String값을 묶거나 Swift에서 만들 수 있는 타입 중 확실한 어떠한 타입이라도 만들 수 있다. 유사하게 당신은 dictionary에 지정된 타입 중 어떠한 값이라도 저장할 수 있고, 타입에는 제한이 없다.

Generics으로 문제 해결
 제너릭을 일반적인, 2개의 Int 값을 바꾸는 제너릭을 사용하지 않은 swapTwoInts 함수다:
