

# How to disable swipe gesture

```swift
func pageViewController(_ pageViewController: UIPageViewController, viewControllerBefore viewController: UIViewController) -> UIViewController?


func pageViewController(_ pageViewController: UIPageViewController, viewControllerAfter viewController: UIViewController) -> UIViewController?

// 두개의 메소드에서 return nil을 해주면 된다.
```