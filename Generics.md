## Generics

 Generics code는 재사용 가능한 함수와 당신이 정의하는 요구사항에 따른 타입, 어떠한 타입이라도 동작할 수 있는 타입을 유연하게 작성할 수 있다. 당신은 중복을 피하고, 의도를 분명하게 표현하고, 추상적 방식으로 code를 작성할 수 있다.

 Generics는 Swift의 가장 강력한 특징 중 하나다, Swift의 표준 라이브러리는 generic code로 설계됐다. 사실은, generics는 Language Guide 처음부터 끝까지 사용됐으며, 심지어 그것을 인식 하지 못할 수 있다. 예를 들어 Swift의 Array와 Dictionary 타입 둘다 generic 콜렉션이다. 당신은 Array에 Int 값을 묶거나 String값을 묶거나 Swift에서 만들 수 있는 타입 중 확실한 어떠한 타입이라도 만들 수 있다. 유사하게 당신은 dictionary에 지정된 타입 중 어떠한 값이라도 저장할 수 있고, 타입에는 제한이 없다.

### Generics으로 문제 해결
 제너릭을 일반적인, 2개의 Int 값을 바꾸는 제너릭을 사용하지 않은 swapTwoInts 함수다:
```
func swapTwoInts(inout a: Int, inout _ b: Int) {

    let temporaryA = a

    a = b

    b = temporaryA

}

```
 이 함수는 a와 b의 값을 바꾸는 in-out 파라미터로 만들었다. in-Out 파라미터 설명 참조.

 swapTwoInts(_:_:)는 본래의 b 값을 a에 넣고, 본래의 a값을 b에 넣어 바꾸는 함수다. 당신은 이 함수를 2개 Int 값을 바꾸기위해 호출할 수 있다.

```
var someInt = 3

var anotherInt = 107

swapTwoInts(&someInt, &anotherInt)

print("someInt is now \(someInt), and anotherInt is now \(anotherInt)”)

// prints “someInt is now 107, and anotherInt is now 3"

```

 swapTwoInts(_:_:) 함수는 유익하다, 그러나 오직 Int값만 사용할 수 있다. 만약 당신이 2개의 String 값이나 2개의 Double값을 바꾸길 원한다면, 당신은 swapTwoStrings와 swapTwoDoubles(_:_:) 함수를 아래에 보여지는 것처럼 함수를 더 가져야한다:

```
func swapTwoStrings(inout a: String, inout _ b: String)
{

    let temporaryA = a

    a = b

    b = temporaryA

}

func swapTwoDoubles(inout a: Double, inout _ b: Double)
{

    let temporaryA = a

    a = b

    b = temporaryA

}

```

 당신은 swapTwoInts, swapTwoStrings 와 swapTwoDoubles(_:_:) 함수는 똑같은 본문을 가지고 있게 된다. 오직 승인하는 (Int, String, Double) 값의 타입만이 다르다.
 이것을 더 유용하고 상당히 유연하게 2개의 any type의 값을 바꿀 수 있도록 1개의 함수로 쓸 수 있다. Generic code는 다음과 같이 쓸 수 있다. (아래에 정의된 함수는 generic 버전)

```
참고
 3개의 함수는, 서로 같은 타입으로 정의된 a와 b의 타입이 중요하다. a와 b의 타입이 같지 않다면, 그들의 값을 바꾸는건 불가능하다. Swift는 type-safe 언어이고 변하기 쉬운 String과 Double 타입을 서로 바꾸는 것을 허용하지 않는다. 이렇게 시도하면 complie-time 에러가 보고된다.
```

### Generic 함수
 Generic 함수는 어떠한 타입이라고 동작할 수 있다. 여기 swapTowInts(_:_:) 함수로 부터 generic 버전의 swapTwoValues 이다:

```
func swapTwoValues<T>(inout a: T, inout _ b: T)
{

    let temporaryA = a

    a = b

    b = temporaryA

}

```

swapTwoValues(_:_:) 함수 내용은 swapTwoInts(_:_:) 함수와 동일한 내용이다. 그러나 swapTwoValues의 첫째줄은 swapTwoInts에서 다르다. 여기 첫번쨰 라인 비교:

```
func swapTwoInts(inout a: Int, inout _ b: Int)

func swapTwoInts<T>(inout a: T, inout _ b: T)
```

 함수의 generic 버전은 actual type 이름 (Int, String 또는 Double) 대신 placeholder 타입 이름 (여기서 T로 불리움) 으로 사용했다. placeholder 타입 이름은 무조건 T라고 말하진 않지만, a와 b둘다 같은 타입 T라고 말한다. 어떠한 무엇이든 T로 표현할 수 있다. swapTwoValues(_:_:) 함수가 호출될 때마다 결정되는 T의 자리에 actual 타입이 사용된다.

 generic 함수의 이름(swapTwoValues)의 차이는 placeholder 타입이름 T 를 angel brackets <T> 로 감싼다. brackets은 Swift에서 T는 swapTwoValues 함수내에 정의된 placeholder 이름으로 불려진다. 이유는 T는 placeholder이고, Swift는 T라고 불리우는 actual 타입을 찾지 않기 때문이다.

 swapTwoValues(_:_:) 함수는 swapTwoInts와 같은 방식으로 호출된다, 단, 서로 같은 타입의 값인 어떠한 타입의 2값을 넘길 수 있다. swapTwoValues가 호출될때 마다, T는 함수에 넘겨진 값의 타입으로 부터 추론되어 사용되는 타입이다.

 2가지 예제가 아래에 있다, T는 각각 Int와 String이다:

```
var someInt = 3

var anotherInt = 107

swapTwoValues(&someInt, &anotherInt)

// some Int is now 107, and anotherInt is now 3

var someString = "hello"

var anotherString = "world"

swapTwoStrings(&someString, &anotherString)

// someString is now "world", and anotherString is now "hello"
```

```
참고
 swapTwoValues(_:_:) 함수는 Swift 표준 라이브러의 한부분인 swap이라는 generic 함수에서 영감을 받아 정의했다, 당신의 앱에서 자동적으로 만들어져 사용한다. 당신의 코드에서 swapTwoValues(_:_:) 함수를 사용할 필요성이 있다면, Swift의 swap(_:_:) 함수를 사용하는게 더 낫다.
```

### 타입 인자 Type Parameters
 swapTwoValues 예제에서, placeholder 타입 T는 타입 파라미터의 예제이다. 타입 파라미터는 placeholder type 이름을 지정하고, 한쌍의 맞는 angle brackets (마치 <T>) 사이에 함수의 이름뒤에 즉시 쓴다.

 한 타입 파라미터를 지정한다, 당신은 함수의 파라미터의 타입 (swapTwoValues(_:_:) 함수의 a와 b 파라미터 처럼), 또는 함수의 리턴 타입, 또는 함수의 내용안에 타입 annotation 을 정의해서 사용할 수 있다. 각각의 경우, placeholder 타입은 함수가 호출 될 때 actual 타입으로 대체되어 표시된다. (swapTwoValues 예제에서, T는 첫번째 함수에서 호출될때 Int로 대체된다, 그리고 2번째 호출될때 String으로 호출된다.)

 당신은 하나 이상의 타입 파라미터를 사용할 수 있으며, 타입 파라미터 이름을 angle brackets에 콤마(,) 로 구분하여 작성한다.

### 타입 인자 이름 Naming Type Parameters
 간단한 경우 generic함수 또는 generic 타입은 한개의 placeholder 타입으로 언급되었다. (swapTwoValues generic 함수같은 또는 generic collection 한가지 타입을 저장하는 Array같은),타입 파라미터를 T 1개의 문자로 사용하는것은 전통적인 방식이다. 그러나 당신은 유요한 어떤 식별자로 타입 파라미터 이름으로 사용할 수 있다.

 만약 당신이 복합적인 generic함수나 genric 타입의 다중 파라미터를 더 정의하고자 하는 경우, 더 설명적인 타입 파라미터 이름을 제공하는게 유용하다. 예를 들어, Swift의 Dictionary 타입은 2가지 타입 파라미터를 가지고 있다-1개는 keys와 1개의 values. 만약 당신이 Dictionary를 직접 작성하고자 한다면, 당신은 2가지 타입 파라미터 key와 Value를 generic code를 사용하여 목적을 깨닫게 이름을 지어주어야 한다.

```
참고
 항상 타입 파라미터는 대문자 UpperCamelCase로 첫글자 대문자를 시작으로 이름을 짓는다. (T와 Key같은) placeholder를 위한 값이 아닌 타입을 가리킨다.
```

### Generic Tapes
 generic 함수를 추가하는 경우, Swift는 당신이 정의한 generic types를 사용할 수 있다. 이 사용자 정의 클래스, 구조체와 열거형에 Array와 Dictionary와 유사한 어떠한 타입이든 작업이 가능하다.

 이 섹션은 당신이 Stack이 불리우는 generic collection 타입을 어떻게 작성해야하는지 보여준다. 스택은 배열과 유사하게 값을 순서대로 설정한다, 그러나 Swift의 Array보다 연상이 좀 더 제한적이다. 배멸은 새로운 아이템을 inserted하고 removed를 허용할때 어느 지역이든 허용한다. 스택은 하지만, 추가된 새로운 아이템의 오직 콜렉션의 끝에서만 허용된다. (스택에서 새로운 값을 pushing) 비슷하게, 스택은 아이템을 지울때 오직 콜렉션의 끝에서만 허용된다. (stack에서 popping)

```
참고
 스택의 컨셉은 네비게이션 계층에 뷰컨트롤러 모델인 UINavigationController 클래스에 사용되어 진다. “last in, first out” (후입선출 얘기) push , pop 나옴
```

아래 그림은 스탯에서 push / pop 동작을 보여준다.


현재 스택에 3개의 값이 있다.
4번째 값이 스택의 가장 위에 “pushed” 되었다.
스택에는 4개의 값이 있고, 가장 최근에 1개가 위에 생겼다.
맨 위에 아이템이 스택에서 삭제되었다. 또는 “poped”.
값이 popping 된 후, 스택에는 다시 3개의 값이 남아있다.

 여기 어떻게 non-generic 버전의 스택을 작성하는지, Int 값의 스택의 경우다:

```
struct IntStack {

    var items = [Int]()

    mutating func push(item: Int) {

        items.append(item)

    }

    mutating func pop() -> Int {

        return items.removeLast()

    }

}

```

 이 구조체는 items라는 스택의 값을 저장하는 Array 프로퍼티를 사용한다. Stack은 2개의 메소드를 제공한다, push와 pop, push 와 pop 값은 스텍에 값을 on and off 한다. 이 메소드들은 mutaing 으로 선언, 이유는 구조체의 items 배열이 수정(또는 변화)이 필요하기 때문이다.

 하지만 IntStack 타입은 오직 Int 값만 보여준다. 어떠한 타입의 값의 스택을 관리할 수 있는 generic Stack 클래스로 정의하는 훨씬 유용하다.

 여기 generic 버전의 샘플 코드이다:

```
struct Stack<T> {

    var items = [T]()

    mutating func push(item: T) {

        items.append(item)

    }

    mutating func pop() -> T {

        return items.removeLast()

    }

}

```

 참고 generic 버전의 Stack은 본질적으로 non-generic 버전과 같지만, Int파입의 actual 타입 대신  placeholder 타입 파라미터 T로 바꾼다. 이 타입 파라미터는 구조체 이름 뒤에 <T> 로 작성하여 넣는다.

 T는 이후에 제공되어진 “some type T”라는 placeholder 이름으로 정의한다. 이 미래 타입은 구조체의 정의된 범위안에서 어디서든 “T”를 적용할 수 있다. 이 케이스에서, T는 3가지 방식으로 사용된다:
items의 프로퍼티를 생성, T타입 값의 빈 배열로 초기화된다.
push 메소드는 반드시 T타입으로된 하나의 파라미터를 가진 item을 지정한다.
pop 메소드는 지정된 T타입의 값을 리턴한다.

 generic 타입이기 때문에, Stack은 Swift의 유효한 어떠한 타입이든 생성하여 사용할 수 있고, 유사한 방식으로 Array와 Dictionary가 있다.

 당신은 angle brackets안에 저장할 타입을 쓰는 새로운 Stack 인스턴스를 만든다. 예를 들어, 문자열의 새로운 스택을 만들때, 당신은 Stack<String>()로 쓴다:

```
var stackOfStrings = Stack<String>()

stackOfStrings.push("uno")

stackOfStrings.push("dos")

stackOfStrings.push("tres")

stackOfStrings.push("cuatro")

// the stack now contains 4 strings
```

여기 stackOfString를 보면 4개의 값이 pushing된 후를 볼 수 있다:


 Popping한 스택의 반환되는 값과 제일 위의 값 “cuatro"이 제거된다:

```
let fromTheTop = stackOfStrings.pop()

// fromTheTop is equal to "cuatro", and the stack now contains 3 strings
```

여기 popping된 스택의 제일 위의 값을 볼 수 있다:



### Extending a Generic Type
 generic타입을 확장할 때, 당신은 확장의 정의의 한 부분으로서 타입 파라미터 목록을 제공하지 않는다. 대신, 원래 타입으로부터 타입 파라미터 목록을 정의는 확장의 내용안에서 가능하고, 원래 타입 파라미터 이름은 원래 정의로부터 타입 파라미터를 참조하는데 사용된다.

 다음 예제는 generic Stack 타입의 확장으로 topItem 읽기전용인 계산 프로퍼티를 추가한다, 최상위 item을 스택으로부터 popping 없이 반환한다.
```
extension Stack {
    var topItem: T? {

        return items.isEmpty ? nil : items[items.count - 1]

    }

}

```

 topItem 프로퍼티는 T 타입의 옵셔널 값을 반환한다. 스택이 비어 있다면, topItem은 nil을 반환; 스택이 비어있지 않으면, items 배열에 마지막 값을 반환한다.

 이 확장은 타입 파라미터 목록을 정의하지 않음에 참고한다. 대신, Stack 타입의 존재하는 타입 파라미터 이름 T는 topItem 계산 프로퍼티의 옵셔널 타입으로 나타내는 확장에 사용된다.

 topItem 계산 프로퍼티는 어떤 Stack 인스턴스에서 접근하고, top item 제거없이 질의할 수 있다:
```
if let topItem = stackOfStrings.topItem {
    print("The top item on the stack is \(topItem).")

}

// prints "The top item on the stack is tres.”

```


### Type Constraints 형식 제약
 swapTwoValues(_:_:) 함수와 Stack 타입은 어떠한 타입에서 동작할 수 있다. 그러나, 때때로 generic 함수와 generic 타입을 사용할 때 특정 타입을 강제할떄 유연해진다. 타입 제약은 지정된 타입파라미터를 상속받는 특정 클래스로부터, 또는 개별적인 프로토콜 또는 프로토콜 결합과 일치해야한다.

 예를들어, Swift의 Dictionary타입은 dictionary의 사용되는 key의 타입이 제한된다. dictionary의 key의 타입은 hashable이다. 이것은 독자적으로 나타내는 방식으로 제공한다. Dictionary는 해쉬로 된 key가 필요하고, 특정 키의 값을 이미 포함하고 있는지 확인할 수 있다. 요구사항 없이, Dictionary는 특정 키에 대한 값을 바꾸거나 추가할 수 없고 또한 이미 dictionary에서 주어진 키 값을 찾아야만 한다.

 이 요구사항은 dictionary를 위한 키에서 타입 제약이 강제된다, 키 타입은 Hashable 프로토콜에 일치하도록 지정되며, 이 프로토콜은 Swift 표준 라이브러리에 정의되어 있다. 모든 Swift의 기본 타입은 (String, Int, Double과 Bool 같은) 기본적으로 해쉬로 되어있다.

 사용자정의 generic 타입을 만들때, 타입 제약을 정의할 수 있고 이들 제약은 generic 프로그래밍의 힘을 제공한다. Hashable 같은 추상 개념은 명확한 타입보다 개념적 특성의 측면에서 타입을 특성화 한다.

 #### 타입 제약 문법 Type Constraint Syntax
 타입 제약은 한 클래스 또는 프로토콜에 한정하여 타입 파라미터의 이름 뒤에 쓸 수 있다. 타입 파라미터 목록의 부분을 콜론(,)으로 나뉜다. 기본 문법은 아래와 같이 generic 함수의 타입 제약으로 보여진다 (비록 generic 타입과 같은 문법이지만).
```
func someFunction<T: SomeClass, U: SomeProtocol>(someT: T, someU: U) {
    // function body goes here

}

```

 위에 가정된 함수는 2개의 파라미터를 가진다. 첫번쨰 타입 파라미터 T는 SomeClass의 서브클래스로 T의 필요하는 타입 제약을 가진다. 2번째 타입 파라미터 U는 SomeProtocol 프로토콜을 준수하는 U를 필요하는 타입제약을 가진다.

#### 타입 제약 작동 Type Constraints in Action
 여기 non-generic 함수인 findStringIndex가 있다, String 값을 가지고 String값의 배열에서 찾는다. findStringIndex(_:_:) 함수는 Int 값을 반환한다, 배열에서 첫번째 매칭된 문자열을 찾은 경우 index를 반환하거나 찾지 못한경우 nil을 반환한다.
```
func findStringIndex(array: [String], _ valueToFind: String) -> Int? {
    for (index, value) in array.enumerate() {

        if value == valueToFind {

            return index

        }

    }



    return nil

}

```

findStringIndex(_:_:) 함수는 문자열의 배열에서 문자열 값을 찾을 수 있다:
```
let strings = ["cat", "dog", "llama", "parakeet", "terrapin"]
if let foundIndex = findStringIndex(strings, "llama") {

    print("The Index llama is \(foundIndex)")

}

// prints "The Index llama is 2”

```
 값의 index를 찾는 원리는 오직 문자열만 가능하므로 유연하지 않다. 당신은 같은 기능의 문자열 값 대신 T 타입으로 바꿔서 generic 함수 findeIndex를 작성할 수 있다.

 여기 findStringIndex의 generic 버전의 findIndex를 작성했다. 반환 타입은 여전히 Int? 다, 이유는 옵셔널 index숫자 반환과 배열에 값이 없을 경우가 있기 때문이다. 경고한다, 이 함수는 컴파일 되지 않는다, 예제 다음에 이유를 밝히겠다:
```
func findIndex<T>(array: [T], _ valueToFind: T) -> Int? {
    for (index, value) in array.enumerate() {

        if value == valueToFind {

            return index

        }

    }

    

    return nil

}

```

 위와 같이 작성된 함수는 컴파일 되지 않는다. 문제는 “if value == valueToFind”, 동등 체크다. 이는 Swift의 모든 타입이 동등 연산자(==)로 비교될 수 없기 때문이다. 만약 복잡한 데이터 모델을 표현한 클래스나 구조체를 만든다면, Swift에서 같다라고 추측할 수 없다. 이때문에, 모든 가능한 타입 T에 대해 보장해주지 못한다. 따라서 컴파일 에러가 발생한다.

 모두가 그렇지 않다. Swift 표준 라이브러리는 Equatable 프로토콜을 정의한다, 동등연산자(==) 부정연산자 (!=) 로 2가지 타입의 값을 비교할 수 있도록 구현되어 있다. 모든 Swift의 표준 타입은 자동적으로 Equatable 프로토콜을 지원한다.

Equatable인 타입은 findIndex 함수에서 안전하게 사용될 수 있다, 이유는 동등연산자 지원을 보장하기 때문이다. 이 사실을 표현하면, 함수를 정의할 때 타입 인자의 정의의 한 부분으로써 Equatable의 타입 제약으로 작성한다.
```
func findIndex<T: Equatable>(array: [T], _ valueToFind: T) -> Int? {
    for (index, value) in array.enumerate() {

        if value == valueToFind {

            return index

        }

    }

    

    return nil

}

```
 findIndex의 하나의 타입 파라미터는 T: Equatable이다, 이것은 “어떠한 타입 T 가 Equatable 프로토콜에 일치한다”를 의미한다.

 findIndex(_:_:) 함수는 컴파일이 성공적이고 Equatable로 Double과 String같은 어떠한 타입이라도 사용가능하다.
```
let doubleIndex = findIndex([3.14159, 0.1, 0.25], 9.3)
// doubleIndex is an optional Int with no value, because 9.3 is not in the array



let stringIndex = findIndex(["Mike", "Malcolm", "Andrea"], "Andrea")

// stringIndex is an optional Int containing a value of 2

```






 


