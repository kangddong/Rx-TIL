
# @property @dynamic @synthesize

objective - C에서 클래스는 `@interface`와 `@implementaion`의 2부분으로 나누어지는데
`@property`는 `@interface` 부분과 연결,
`@synthesize`와 `@dynamic`은 `@implementation` 부분과 연결 된다.
`@synthesize`는 preprocessor macro라서 Xcode에서 Build and Run을 실행했을 때 prewritten/preformatted 코드블락으로 교체된다.

**preprocessor macro란 ?**
preprocessor(전처리기)
macro(매크로)

# @property

기존에 프로퍼티에 대한 getter와 setter 메서드를 선언해 줄 수 있습니다. 
하지만 항상 같은 형태로 반복되는 지루한 작업이기 때문에
*Objective-C 2.0*에서부터는 `@property` 지시어를 사용해서 getter와 setter에 대한 코드를 자동으로 생성할 수 있도록 해줍니다.

`@property`의 선언 원형은 아래와 같다.

```objc
@property (attributes) type name;
```


코드를 통해서 얘기해보자
```objc
@interface MyClass: NSObject {
	float value;
}

// floatingValue에 대한 getter와 setter를 지정할 수 있다. (기존)
- (float)value;
- (void)setValue:(float)newValue;

// @property를 통해서 선언해주는 방법
@property float floatingValue;
@end

@interface ViewController: UIViewController {
	UIScrollView bgView;
}

@property (nonatomic, retain) UIScrollView *bgView;
@end
```

## about attributes

#### Writability
#### Setter Semantics
#### Atomicity


[The Objective-C Programming Language](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/ObjectiveC/Chapters/ocProperties.html)
