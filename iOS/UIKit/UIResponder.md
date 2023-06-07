
responding 과 핸들링 이벤트에 대한 추상적인 인터페이스

```swift
@MainActor class UIResponder: NSObject
```

응답기 개체(UIResponder 인스턴스)는 UIKit 앱의 이벤트 처리 backbone을 구성합니다.
`UIApplication` 개체, `UIViewController` 개체 및 모든 `UIView` 개체(`UIWindow` 포함)를 비롯한 많은 주요 개체가 응답자입니다. 
이벤트가 발생하면 UIKit은 이벤트를 앱의 응답자 개체로 전송하여 처리합니다.
터치 이벤트, 모션 이벤트, remote-contol 이벤트, press 이벤트 등 여러 종류의 이벤트가 있습니다.

특정 유형의 이벤트를 처리하려면 응답자가 해당 메서드를 꼭(must) 재정의해야 합니다. 
예를 들어, 터치 이벤트를 처리하기 위해, a responder  `touchesBegan(_:with:)`, `touchesMoved(_:with:)`, `touchesEnded(_:with:)`, and `touchesCancelled(_:with:)` 메소드들을 구현한다. 
터치의 경우 responder는 UIKit에서 제공하는 이벤트 정보를 사용하여 터치의 변경 내용을 추적하고 앱의 인터페이스를 적절하게 업데이트합니다.
 
In addition to handling events, UIKit responders also manage the forwarding of unhandled events to other parts of your app. If a given responder doesn’t handle an event, it forwards that event to the next event in the responder chain. UIKit manages the responder chain dynamically, using predefined rules to determine which object should be next to receive an event. For example, a view forwards events to its superview, and the root view of a hierarchy forwards events to its view controller.

UIKit 응답자는 이벤트 처리 외에도 처리되지 않은 이벤트를 앱의 다른 부분으로 전달하는 작업도 관리합니다. 지정된 응답자가 이벤트를 처리하지 않으면 해당 이벤트를 응답자 체인의 다음 이벤트로 전달합니다. UIKit는 미리 정의된 규칙을 사용하여 이벤트를 수신할 다음 개체를 결정하여 응답기 체인을 동적으로 관리합니다. 예를 들어 보기는 이벤트를 해당 수퍼뷰로 전달하고 계층의 루트 보기는 이벤트를 해당 보기 컨트롤러로 전달합니다.

Responders process [`UIEvent`](https://developer.apple.com/documentation/uikit/uievent) objects but can also accept custom input through an input view. The system’s keyboard is the most obvious example of an input view. When the user taps a [`UITextField`](https://developer.apple.com/documentation/uikit/uitextfield) and [`UITextView`](https://developer.apple.com/documentation/uikit/uitextview)object onscreen, the view becomes the first responder and displays its input view, which is the system keyboard. Similarly, you can create custom input views and display them when other responders become active. To associate a custom input view with a responder, assign that view to the [`inputView`](https://developer.apple.com/documentation/uikit/uiresponder/1621092-inputview) property of the responder.


응답자는 UI 이벤트 개체를 처리하지만 입력 보기를 통해 사용자 지정 입력을 수락할 수도 있습니다. 시스템의 키보드는 입력 보기의 가장 확실한 예입니다. 사용자가 화면에서 UITextField 및 UITextView 개체를 누르면 보기가 첫 번째 응답자가 되고 입력 보기인 시스템 키보드를 표시합니다. 마찬가지로, 사용자 정의 입력 보기를 작성하고 다른 응답자가 활성화될 때 표시할 수 있습니다. 사용자 지정 입력 보기를 응답기와 연결하려면 해당 보기를 응답기의 inputView 속성에 할당합니다.
git a
responders 및 esponder chain에 대한 내용은 `Using responders and the responder chain to handle events`를 참조하십시오.

# Overview

Apps receive and handle events using _responder objects_. A responder object is any instance of the [`UIResponder`](https://developer.apple.com/documentation/uikit/uiresponder) class, and common subclasses include [`UIView`](https://developer.apple.com/documentation/uikit/uiview), [`UIViewController`](https://developer.apple.com/documentation/uikit/uiviewcontroller), and [`UIApplication`](https://developer.apple.com/documentation/uikit/uiapplication). Responders receive the raw event data and must either handle the event or forward it to another responder object. When your app receives an event, UIKit automatically directs that event to the most appropriate responder object, known as the _first responder_. 

Unhandled events are passed from responder to responder in the active _responder chain_, which is the dynamic configuration of your app’s responder objects. The following image shows the responders in an app whose interface contains a label, a text field, a button, and two background views. The diagram also shows how events move from one responder to the next, following the responder chain.

![[Pasted image 20230606004605.png]]

If the text field doesn’t handle an event, UIKit sends the event to the text field’s parent `UIView` object, followed by the root view of the window. From the root view, the responder chain diverts to the owning view controller before directing the event to the window. If the window can’t handle the event, UIKit delivers the event to the `UIApplication` object, and possibly to the app delegate if that object is an instance of `UIResponder` and not already part of the responder chain.

# Determine an event's first responder

UIKit designates an object as the first responder to an event based on the type of that event. Event types include:

|Event type|First responder|
|---|---|
|Touch events|The view in which the touch occurred.|
|Press events|The object that has focus.|
|Shake-motion events|The object that you (or UIKit) designate.|
|Remote-control events|The object that you (or UIKit) designate.|
|Editing menu messages|The object that you (or UIKit) designate.|

Note

Motion events related to the accelerometers, gyroscopes, and magnetometer don’t follow the responder chain. Instead, Core Motion delivers those events directly to the designated object. For more information, see [Core Motion Framework](https://developer.apple.com/library/archive/documentation/Miscellaneous/Conceptual/iPhoneOSTechOverview/CoreServicesLayer/CoreServicesLayer.html#//apple_ref/doc/uid/TP40007898-CH10-SW27)

Controls communicate directly with their associated target object using action messages. When the user interacts with a control, the control sends an action message to its target object. Action messages aren’t events, but they may still take advantage of the responder chain. When the target object of a control is `nil`, UIKit starts from the target object and traverses the responder chain until it finds an object that implements the appropriate action method. For example, the UIKit editing menu uses this behavior to search for responder objects that implement methods with names like [`cut(_:)`](https://developer.apple.com/documentation/uikit/uiresponderstandardeditactions/2354193-cut), [`copy(_:)`](https://developer.apple.com/documentation/uikit/uiresponderstandardeditactions/2354191-copy), or [`paste(_:)`](https://developer.apple.com/documentation/uikit/uiresponderstandardeditactions/2354189-paste). 

Gesture recognizers receive touch and press events before their view does. If a view’s gesture recognizers fail to recognize a sequence of touches, UIKit sends the touches to the view. If the view doesn’t handle the touches, UIKit passes them up the responder chain. For more information about using gesture recognizer’s to handle events, see [Handling UIKit gestures](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/handling_uikit_gestures).

# Determine which responder contained a touch event

UIKit uses view-based hit-testing to determine where touch events occur. Specifically, UIKit compares the touch location to the bounds of view objects in the view hierarchy. The [`hitTest(_:with:)`](https://developer.apple.com/documentation/uikit/uiview/1622469-hittest) method of [`UIView`](https://developer.apple.com/documentation/uikit/uiview) traverses the view hierarchy, looking for the deepest subview that contains the specified touch, which becomes the first responder for the touch event.

Note

If a touch location is outside of a view’s bounds, the [`hitTest(_:with:)`](https://developer.apple.com/documentation/uikit/uiview/1622469-hittest)method ignores that view and all of its subviews. As a result, when a view’s [`clipsToBounds`](https://developer.apple.com/documentation/uikit/uiview/1622415-clipstobounds) property is `true`, subviews outside of that view’s bounds aren’t returned even if they happen to contain the touch. For more information about the hit-testing behavior, see the discussion of the [`hitTest(_:with:)`](https://developer.apple.com/documentation/uikit/uiview/1622469-hittest) method in [`UIView`](https://developer.apple.com/documentation/uikit/uiview).

When a touch occurs, UIKit creates a [`UITouch`](https://developer.apple.com/documentation/uikit/uitouch) object and associates it with a view. As the touch location or other parameters change, UIKit updates the same `UITouch` object with the new information. The only property that doesn’t change is the view. (Even when the touch location moves outside the original view, the value in the touch’s [`view`](https://developer.apple.com/documentation/uikit/uitouch/1618109-view) property doesn’t change). When the touch ends, UIKit releases the `UITouch` object.

# Alter the responder chain

You can alter the responder chain by overriding the [`next`](https://developer.apple.com/documentation/uikit/uiresponder/1621099-next) property of your responder objects. When you do this, the next responder is the object that you return.

Many UIKit classes already override this property and return specific objects, including:

- [`UIView`](https://developer.apple.com/documentation/uikit/uiview) objects. If the view is the root view of a view controller, the next responder is the view controller; otherwise, the next responder is the view’s superview.
    
- [`UIViewController`](https://developer.apple.com/documentation/uikit/uiviewcontroller) objects.
    
    - If the view controller’s view is the root view of a window, the next responder is the window object.
        
    - If the view controller was presented by another view controller, the next responder is the presenting view controller.
        
- [`UIWindow`](https://developer.apple.com/documentation/uikit/uiwindow) objects. The window’s next responder is the [`UIApplication`](https://developer.apple.com/documentation/uikit/uiapplication)object.
    
- [`UIApplication`](https://developer.apple.com/documentation/uikit/uiapplication) object. The next responder is the app delegate, but only if the app delegate is an instance of [`UIResponder`](https://developer.apple.com/documentation/uikit/uiresponder) and isn’t a view, view controller, or the app object itself.
