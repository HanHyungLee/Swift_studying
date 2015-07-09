#Swift 2.0 Study

## Collection Type

### Array
- 순서대로 같은 자료형의 데이터가 저장되는 집합.
- NSArray와 호환(bridge)된다.

var로 선언하여 mutable 변경 가능
let으로 선언하면 변경불가능 

- 기본 선언
```
var shoppingList: [String] = [“Eggs”, “Milk”]
```
- Literal 문법
```
var shoppingList = [“Eggs”, “Milk”]
```
- isEmpty 메소드로 빈값 체크
- append(_:) 메소드로 값 추가

- += 연산자로 추가 가능
- index으로 값 추출 (0부터 시작하는 zero-indexed)
```
shopingList[0] = “Six eggs”
```
- 범위 지정으로 여러개의 값을 바꿀 수 있다.
```
shopingLIst[4…6] = [“Bananas”, “Apples”]
```
- 삭제
removeLast(), removeAtIndex(_:) 메소드로 삭제, 삭제시 삭제된 item이 리턴된다.
```
let apples = shoppingList.removeLast()
```

- 반복문
for-in loop문으로 값을 가져올 수 있다.
```
for item in shoppingList {
	print(item)
}
```
enumerate()를 사용해 index와 value를 추출할 수 있다.
```
for (index, value) in shoppingList.enumerate() {
    print("Item \(index + 1): \(value)")
}
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
