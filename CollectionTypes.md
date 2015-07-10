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

- count와 isEmpty 메소드로 갯수 체크
```
var shoppingList = ["Eggs", "Milk"]

// count
print(“shoppingList count: \(shoppingList.count)”)	// shoppingList count: 2

// 빈값 체크
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
- Set은 Hash Value를 지원한다.

- 선언과 초기화
```
// 기본 배열 선언
var letters = Set<Character>()

// Literal 문법 선언
var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"]

// 형식 추론 선언
var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]

// 빈값 초기화
favoriteGenres = []
```

- count, isEmpty로 갯수 체크
```
var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]

// coount
print("I have \(favoriteGenres.count) favorite music genres.")		// prints "I have 3 favorite music genres.

// 빈값 체크
if favoriteGenres.isEmpty {
    print("As far as music goes, I'm not picky.")
} else {
    print("I have particular music preferences.")
}
// prints "I have particular music preferences.
```

- 새로운 값 추가
```
var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]

favoriteGenres.insert("Jazz")	// ["Rock", "Classical", "Hip hop”, “Jazz”]
```

- 삭제
```
var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]

if let removedGenre = favoriteGenres.remove("Rock") {
    print("\(removedGenre)? I'm over it.")
} else {
    print("I never much cared for that.")
}
// prints "Rock? I'm over it.

// 모두 삭제
favortieGenres.removeAll()	// []
```

- 값 존재 유무 확인
```
var favoriteGenres: Set = ["Rock", "Classical", "Hip hop”, "Funk"]

if favoriteGenres.contains("Funk") {
    print("I get up on the good foot.")
} else {
    print("It's too funky in here.")
}
// prints "It's too funky in here.
```

- 반복문
```
var favoriteGenres: Set = ["Classical", "Jazz", "Hip hop”]

// for-in loop
for genre in favoriteGenres {
    print("\(genre)")
}
// Classical
// Jazz
// Hip hop”

// for-in loop & sort() 정렬
for genre in favoriteGenres.sort() {
    print("\(genre)")
}
// Classical
// Hip hop
// Jazz
```

- set 집합 연산
```
let oddDigits: Set = [1, 3, 5, 7, 9]
let evenDigits: Set = [0, 2, 4, 6, 8]
let singleDigitPrimeNumbers: Set = [2, 3, 5, 7]
 
// 합집합
oddDigits.union(evenDigits).sort()	// [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

// 교집합
oddDigits.intersect(evenDigits).sort()	// []

// 차집합
oddDigits.subtract(singleDigitPrimeNumbers).sort()	// [1, 9]

// 베타적 집합
oddDigits.exclusiveOr(singleDigitPrimeNumbers).sort()	// [1, 2, 9]
```

- 집합 포함관계
```
let houseAnimals: Set = ["🐶", "🐱"]
let farmAnimals: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
let cityAnimals: Set = ["🐦", "🐭"]
 
// houseAnimals 값이 armAnimals에 모두 포함하고 있는지 여부
houseAnimals.isSubsetOf(farmAnimals)	// true

// farmAnimals 값에 houseAnimals이 모두 포함되어 있는지 여부
farmAnimals.isSupersetOf(houseAnimals)	// true

// farmAnimals 값이 cityAnimals값에 포함하지 않는지 여부
farmAnimals.isDisjointWith(cityAnimals)	// true
```

### Dictionary
- 같은 종류의 자료형  key와 value를 저장하는 집합.
- 순서대로 저장된다.
- key는 유니크한 값이어야 한다.
- NSDictionary와 호환(bridge)된다.
-콜론 : 으로 key와 value를 구분한다.

- 선언과 초기화
```
// 기본선언
var namesOfIntegers = [Int: String]()
// namesOfIntegers is an empty [Int: String] dictionary

// 1개 값 초기화
namesOfIntegers[16] = "sixteen"

// Literal 문법
var airports: [String: String] = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]

// 형식 추론
var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]

// 빈값 초기화
airports = [:]

```

- count, isEmpty로 갯수 체크
```
var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]

// couint
print("The airports dictionary contains \(airports.count) items.")	// prints "The airports dictionary contains 2 items.

// 빈값 체크
if airports.isEmpty {
    print("The airports dictionary is empty.")
} else {
    print("The airports dictionary is not empty.")
}
// prints "The airports dictionary is not empty.
```

- 값 추가, 변경
```
var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]

// 추가
airports["LHR"] = "London"		// ["YYZ": "Toronto Pearson", "DUB": "Dublin”, "LHR”:  "London"	]

// 변경
airports["LHR"] = "London Heathrow”	// ["YYZ": "Toronto Pearson", "DUB": "Dublin”, "LHR”:  "London Heathrow"

// updateValue(_: forKey:) 값 변경, 변경되기 전 값이 리턴된다.
```
var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]

if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB") {
    print("The old value for DUB was \(oldValue).")
}
// prints "The old value for DUB was Dublin.
```

- 삭제
```
var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin”, "LHR”:  "London"]

// 삭제
airports["DUB"] = nil

// removeValueForKey() 메소드 사용, 삭제되는 값이 리턴된다.
if let removedValue = airports.removeValueForKey("LHR") {
    print("The removed airport's name is \(removedValue).")
} else {
    print("The airports dictionary does not contain a value for LHR.")
}
```

- 반복문
```
var airports = ["YYZ": "Toronto Pearson", "LHR”:  "London, Heathrow“]

// for-in loop  (key, value) 리턴
for (airportCode, airportName) in airports {
    print("\(airportCode): \(airportName)")
}
// YYZ: Toronto Pearson
// LHR: London Heathrow

// for-in loop key값만 리턴
for airportCode in airports.keys {
    print("Airport code: \(airportCode)")
}
// Airport code: YYZ
// Airport code: LHR

// for-in loop value값만 리턴
for airportName in airports.values {
    print("Airport name: \(airportName)")
}
// Airport name: Toronto Pearson
// Airport name: London Heathrow
```

- key와 value추출
```
var airports = ["YYZ": "Toronto Pearson", "LHR”:  "London, Heathrow“]

// key값만 추출, array형태로 리턴된다.
let airportCodes = [String](airports.keys)	// airportCodes is ["YYZ", "LHR"]

// value값만 추출, array형태로 리턴된다. 
let airportNames = [String](airports.values)	// airportNames is ["Toronto Pearson", "London Heathrow"]
```
