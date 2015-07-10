#Swift 2.0 Study

## Collection Type

- array, set, dictionary 3가지 기본 타입을 지원한다.
- Swift에서는 저장할 수 있는 key와 value를 항상 명확하게 저장한다. 이것이 의미하는 것은 잘못된 타입으로 인한 실수를 방지하기 위함이다. 또한 콜렉션에서 되찾는 value의 타입에 대해서 확신을 가질 수 있다는 의미다.
- Swift의 array, set, dictionary는 generic collection을 제공한다.
- var로 선언하면 변경 가능 (mutable)
- let으로 선언하면 변경불가능 (immutable)
- 가장 좋은 방식은 변경이 필요 없을 때 let선언으로 immutable콜렉션으로 만드는 것이다. 이렇게 했을때 Swift 컴파일러가 성능을 효과적으로 해줄 것이다.

### Array
- 같은 자료형의 데이터가 순서대로 저장되는 집합.
- Objective-C 의 NSArray 클래스와 호환(bridge) 된다.

- 선언과 초기화
```
// 기본 배열 선언
var shoppingLit: Array<String> = []

// Literal 문법 선언
var shoppingList: [String] = [“Eggs”, “Milk”]

// 형식 추론 선언
var shoppingList = [“Eggs”, “Milk”]

// 빈값 초기화
shoppingList = []

// 특정 크기로 초기화
var threeDoubles = [Double](count: 3, repeatedValue: 0.0)		// [0.0, 0.0, 0.0]
```

- 새로운 값 추가, append(_:) 메소드
```
var shoppingList = ["Eggs", "Milk"]
shoppingList.append("Flour")	// "Eggs", "Milk”, "Flour"
```

- isEmpty 메소드로 빈값 체크
```
var shoppingList = ["Eggs", "Milk"]


if shoppingList.isEmpty {
    print("The shopping list is empty.")
} else {
    print("The shopping list is not empty.")
}
// prints "The shopping list is not empty.”

```

- + , += 연산자
```
var threeDoubles = [Double](count: 3, repeatedValue: 0.0)		// [0.0, 0.0, 0.0]
var anotherThreeDoubles = [Double](count: 3, repeatedValue: 2.5)	// [2.5, 2.5, 2.5]
var sixDoubles = threeDoubles + anotherThreeDoubles”	// [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]
```

- index으로 값 추출 (0부터 시작하는 zero-indexed)
```
var shoppingList = ["Eggs", "Milk”, "Flour"]
var firstItem = shoppingList[0]		// “Eggs”
```

- array 값 변경
```
var shoppingList = ["Eggs", "Milk”, "Flour"]

// index지정 값 변경
shopingList[0] = “Six eggs”

shopingLIst[0…2] = [“Bananas”, “Apples”]		//  [“Eggs”, “Bananas”, “Apples”, "Milk”, "Flour”]
```

- 삭제
removeLast(), removeAtIndex(_:) 메소드로 삭제, 삭제시 삭제된 item이 리턴된다.
```
var shoppingList = ["Eggs", "Milk”, "Flour"]
let flour = shoppingList.removeLast()	// "Flour" return and removed last index
```

- 반복문
for-in loop문으로 값을 가져올 수 있다.
```
var shoppingList = ["Eggs", "Milk”, "Flour"]

for item in shoppingList {
	print(item)
}

// “Eggs”
// “Milk”
// “Flour”
```

- enumerate()를 사용해 index와 value를 추출할 수 있다.
```
var shoppingList = ["Eggs", "Milk”, "Flour"]

for (index, value) in shoppingList.enumerate() {
    print("Item \(index + 1): \(value)")
}

// Item 1: “Eggs”
// Item 2: “Milk”
// Item 3: “Flour”
```

### Set
- 유일한 값의 집합 (데이터가 중복해서 저장되지 않는다. 중복데이터는 1개로 표시)
- 같은 자료형의 데이터로 저장해야 한다.
- 정렬되지 않는다.

- 집합처럼 연산자 api지원

### Dictionary
- 같은 종류의 자료형  key와 value를 저장하는 집합.
- 순서대로 저장된다.
- key는 유니크한 값이어야 한다.
- NSDictionary와 호환(bridge)된다.
 
 
콜론 : 으로 key와 value를 구분한다.
[key1: value1, key2: value2, key3: value3]

    var airports: [String: String] = ["YYZ": "Toronto Pearson", "DUB", "Dublin"]
