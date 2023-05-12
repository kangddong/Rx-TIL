1. Add HealthKit Entitlement, Capabilities
2. Add Info.plist `NSHealthUpdateUsageDescription`, `NSHealthShareUsageDescription`
3. reqquest API

```swift
let store = HKHealthStore()

let allTypes = Set([HKObjectType.workoutType(),
                    HKObjectType.quantityType(forIdentifier: .activeEnergyBurned)!,
                    HKObjectType.quantityType(forIdentifier: .distanceCycling)!,
                    HKObjectType.quantityType(forIdentifier: .distanceWalkingRunning)!,
                    HKObjectType.quantityType(forIdentifier: .heartRate)!])

store.requestAuthorization(toShare: allTypes, read: allTypes) { granted, error in
	if let error = error {
		print(error.localizedDescription)
		return
	}
	print("granted = \(granted)")

}
```