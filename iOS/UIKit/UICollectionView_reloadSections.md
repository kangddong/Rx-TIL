CollectionView의 특정 된 섹션의 데이터를 다시 불러오는 메소드이다.

함수원형을 보자

```swift
func reloadSections(_ section: IndexSet)
```


지정된 섹션의 항목만 선택적으로 다시 로드하려면 이 메소드를 호출하십시오. 
이로 인해 컬렉션 뷰는 해당 항목과 관련된 모든 셀을 버리고 다시 표시합니다. 이 메서드는 또한 지정된 섹션의 placeholders를 버립니다.

## IndexSet

다른 컬렉션에 있는 elements의 인덱스를 나타내는 고유한 정수 값의 컬렉션입니다.

```swift
struct IndexSet
```

유효한 정수 값의 범위는 `0...Int.max-1` 입니다 . 이 범위를 벗어나면 오류입니다.


# 사용 예시


```swift

enum SectionType: Int {
	case banner = 0
	case list

	var section: Int {
		// rawValue로 바로 사용할 수 있었는데 명시적이지않다고 생각하여 프로퍼티 사용
		return self.rawValue
	}
}

collectionview.reloadSections(IndexSet(interger: SectionType.home.section)
```

Thread 1: "Invalid update: invalid number of sections.
The number of sections contained in the collection view after the update (2) must be equal to the number of sections contained in the collection view before the update (1), plus or minus the number of sections inserted or deleted (1 inserted, 1 deleted). 