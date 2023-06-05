
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