순서는 공식 문서에 따릅니다.

[THE SWIFT PROGRAMMING LANGUAGE GUIDE](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html)

- The Basics
- [기본 연산자 (Basics Operators)](BasicsOperators.md)
- [문자열과 문자 (String and Characters)](StringAndCharacters.md)
- [콜렉션 타입 (Collection Types)](CollectionTypes.md)
- [제어문 (Control Flow)](ControlFlow.md)
- [함수 (Functions)](Functions.md)
- [클로저 (Closures)](Closures.md)
- [열거형 (Enumerations)](Enumerations.md)
- [클래스와 구조체 (Structures and Classes)](StructuresAndClasses.md)
- [프로퍼티 (Properties)](Properties.md)
- [매소드 (Methods)](Methods.md)
- [서브스크립트 (Subscripts)](Subscripts.md)
- [상속 (Inheritance)](Inheritance.md)
- [초기화 (Initialization)](Initialization.md)
- [초기화 해지 (Deinitialization)](Deinitialization.md)
- [옵셔널 체이닝 (Optional Chaining)](OptionalChaining.md)
- [에러 처리 (Error Handling)](ErrorHandling.md)
- [동시성 (Concurrency)](Concurrency.md)
- [타입캐스팅 (Type Casting)](TypeCasting.md)
- [중첩 타입 (Nested Types)](NestedTypes.md)
- [익스텐션 (Extensions)](Extensions.md)
- [프로토콜 (Protocols)](Protocols.md)
- [제네릭 (Generics)](Generics.md)
- [불투명한 타입 (Opaque Types)](OpaqueTypes.md)
- [자동 참조 카운트 (Automatic Reference Counting)](AutomaticReferenceCounting.md)
- [메모리 안정성 (Memory Safety)](MemorySafety.md)
- [접근 제어 (Access Control)](AccessControl.md)
- [고급 연산자 (Advanced Operators)](AdvancedOperators.md)



<details>
  <summary> 2022.01.19 올림, 내림, 반올림, 버림, 절대값 </summary>
  
  ```swift
  import Foundation

  var decimalPoints: [Double] = [30.6, 2.4, -1.2, -1.6]

  /*
   ceil 올림
   floor 내림
   trunc 버림
   round 반올림
   abs 절대값
   fabs Double 형의 절대값
  */

  func testDecimal() {
    
    print(#function + "start \n")
    decimalPoints.forEach { number in
        print("origin \(number)")
        print("ceil = \(ceil(number))")
        print("floor = \(floor(number))")
        print("trunc = \(trunc(number))")
        print("round = \(round(number))")
        print("abs = \(abs(number))")
        print("fabs = \(fabs(number))")
        print("\n")
    }
}

testDecimal()
  ```
</details>

<details>
  <summary> 2022.01.27 map, flatMap, compactMap, forEach, filter, reduce </summary>
  
  ```swift
  
  import Foundation

// MARK: map
// 각 요소에 대한 값을 변경하고자 할 때 사용하고, 그 결과들을 배열로 반환합니다.
let names = ["BTS", "손흥민", "봉준호", "Rx",]
names.map {
    $0 + "'s name"
}

let array = [1, 2, 3, 4, 5]
let mapTest1 = array.map { $0 + 1 }

print(" =================================================== ")
print("map, flatMap, compactMap\n")
print("mapTest1 \(mapTest1)")

// MARK: 1차원 배열의 경우
let array1 = [1, nil, 3, nil, 5, 6, 7]

// MARK: flatMap
// 1. flatten하게 만듬
// 2. nil을 제거
// 3. 옵셔널 바인딩
let flatMapTest1 = array1.flatMap { $0 }

// MARK: compactMap
// 1차원 배열에서
// 옵셔널 바인딩하고싶을 때
let compactMapTest1 = array1.compactMap { $0 }

print("flatMapTest1 \(flatMapTest1)")
print("compactMapTest1 \(compactMapTest1)")

// result
// flatMapTest1 [1, 3, 5, 6, 7]
// compactMapTest1 [1, 3, 5, 6, 7]

// MARK: 2차원 배열의 경우
let array2 = [[1, 2, 3], [nil, 5], [6, nil], [nil, nil]]

// MARK: flatMap
// 2차원 배열을 1차원 배열로 flatten 하게 만들어줌
let flatMapTest2 = array2.flatMap { $0 }

// MARK: compactMap
// 2차원 배열을 1차원 배열로 flatten 하게 만들어주지않음
let compactMapTest2 = array2.compactMap { $0 }

print("flatMapTest2 \(flatMapTest2)")
print("compactMapTest2 \(compactMapTest2)")

let flatMapAndCompactMapTest1 = array2.flatMap { $0 }.compactMap { $0 }
print("flatMapAndCompactMapTest1 \(flatMapAndCompactMapTest1)")
print(" =================================================== \n")
// result
// flatMapTest2 [Optional(1), Optional(2), Optional(3), nil, Optional(5), Optional(6), nil, nil, nil]
// compactMapTest2 [[Optional(1), Optional(2), Optional(3)], [nil, Optional(5)], [Optional(6), nil], [nil, nil]]

// flatMapAndCompactMapTest1 [1, 2, 3, 5, 6]

// MARK: for-in
// break, continue을 사용할 수 있고, return를 이용하면 에러가 납니다.
print(" =================================================== ")
print("forEach\n")
for number in array {
    print("number = \(number)")
}

// MARK: forEach
// break, continue 구문을 사용할 수 없고, return을 통해서 빠져나갈 수 있습니다. (continue처럼 동작함)
array.forEach { print("$0 = \($0)") }

print(" =================================================== \n")

print(" =================================================== ")
print("Filter\n")
let filterTest1 = names.filter { $0 == "Rx"}
let filterTest2 = array.filter { $0 % 2 == 0 }
print("filterTest1 = \(filterTest1)")
print("filterTest2 = \(filterTest2)")
print(" =================================================== \n")

// MARK: Reduce
// 문자열이든, 정수든 내부를 하나로 합쳐주는 기능을 한다.
// 첫 번째 매겨변수는 초깃값이고, 최초의 값($0)으로 사용된다.
print(" =================================================== ")
print("Reduce\n")

let reduceTest1 = (1...50).reduce(0) { (sum, nextValue) -> Int in
    return sum + nextValue
}
print("reduceTest1 = \(reduceTest1)")
print("(1...50).reduce(0) { $0 + $1 } = \((1...50).reduce(0) { $0 + $1 })")


// result
// 1275

let reduceTest2 = ["1", "2", "3", "4", "5"].reduce("") { (strSum, str) in
    return strSum + str
}
let reduceTest3 = ["1", "2", "3", "4", "5"].reduce("") { $0 + $1 }
print("reduceTest2 = \(reduceTest2)")
print("reduceTest3 = \(reduceTest3)")

print(" =================================================== \n")


  ```
</details>
