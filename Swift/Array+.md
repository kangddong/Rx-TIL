```swift
extension Array {
    /// 안전하게 index로 데이터 가져오기
    subscript(safe index: Int) -> Element? {
        return self.indices ~= index ? self[index] : nil
    }
}
```


```swift
extension Array where Element : Equatable {

    mutating func predicateInsert(_ element: Element, at index: Int) -> Bool {
        guard !contains(element) else { return false }
        insert(element, at: index)
        return true
    }

    mutating func predicateAppend(_ element: Element) -> Bool{
        guard !contains(element) else { return false }
        append(element)

        return true
    }

}
```