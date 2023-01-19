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
