

error code 2003334207 시에 `checkResourceIsReachable()` 통해서 자세한 error을 볼 수 있다

```swift
do {
	let isReachable = try fileURL.checkResourceIsReachable()	
} catch {
	print(error.localizedDescription)
}

```