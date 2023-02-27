## 2023.02.27

### 현재 시간 구하기

```swift
print(Date())

// 출력 값 -> **2023-02-27 08:11:58 +0000**
```

### DateFormatter 사용하기
* 특정 연도, 월, 일, 시간을 구하고 싶을 때

```swift
var formatter = DateFormatter()
formatter.dateFormat = "yyyy-MM-dd HH:mm:ss"
formatter.string(from: Date())
```



## 시간차 구하기

### Date 클래스의  *timeIntervalSince(_:)메소드 이용하기


```swift

func timeIntervalSince(_ date: `Date`) -> TimeInterval

let date1: Date = Date()

DispatchQueue.global().asyncAfter(deadline: .now() + 5.0, excute : {

	let date2: Date = Date()
	let timeInterval1 = date2.timeIntervalSince(date1)						
	print(timeInterval1)											
})

```

