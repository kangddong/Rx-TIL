## Performing Calculations

이 값을 역으로 바꿉니다.

```swift
mutating func negate()
```

주어진 값으로 나눈 이 값의 몫과 나머지를 반환합니다.
```swift
func quotientAndReminder(dividingBy rhs: Self) -> (quotient: Self, reminder: Self)
```

이 값이 주어진 값의 배수라면 true를 반환하고, 그렇지 않으면 false를 반환합니다.
```swift
func isMutiple(of other: Self) -> Bool
```


두 개의 edge case는 특히 주목할 가치가 있다:

-  `x.isMultiple(of: 0)`은 x가 0이면 참이고 그렇지 않으면 거짓이다.
- T.min.isMultiple(of: -1)는 몫 T.min / -1이 T 유형에서 나타낼 수 없더라도 부호 있는 정수 T에 대해 참이다.