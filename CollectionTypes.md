#Swift 2.0 Strudy

- Collection Type

# Array
- 순서대로 데이터가 저장되는 집합.
- NSArray와 호환(bridge)된다.

# Set
- 유일한 값의 집합 (데이터가 중복해서 저장되지 않는다.)
- 같은 자료형의 데이터로 저장해야 한다.
- 정렬되지 않는다.

- 집합처럼 연산자 api지원

# Dictionary
- 같은 종류의 자료형  key와 value를 저장하는 집합.
- 순서대로 저장된다.
- key는 유니크한 값이어야 한다.
- NSDictionary와 호환(bridge)된다.
 
 
콜론 : 으로 key와 value를 구분한다.
[key1: value1, key2: value2, key3: value3]

\`var airports: [String: String] = ["YYZ": "Toronto Pearson", "DUB", "Dublin"]\`

