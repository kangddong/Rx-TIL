# Manual Memory Management

```swift
var myArray: [Int] = [] {

    didSet {

        print("size = \(MemoryLayout.size(ofValue: myArray))")
        print("capacity = \(myArray.capacity)")
        print()

    }

}

myArray.append(1)
// Result size = 8, capacity = 2
myArray.append(2)
// Result size = 8, capacity = 2
myArray.append(3)
// Result size = 8, capacity = 4
myArray.append(4)
// Result size = 8, capacity = 4
myArray.append(5)
// Result size = 8, capacity = 8
myArray.append(6)
// Result size = 8, capacity = 8
```