
# Appending String to NSString in Objective-C

`Swfit를` 사용할 때는 문자열끼리 `+연산자` 혹은 `문자열 보간법(string interpolation)`을 통해서 처리를 했지만, Objective-C에서는 아래와 같은 방법으로 처리해야한다.

```objc
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[]) {
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];
    NSString * test = [[NSString alloc] initWithString:@"test 임!"];
    // test = test 임!
    NSString * test2 = [test stringByAppendingString:@" test에 추가함 !"];
    // test2 = test 임! test에 추가함 !
    [test release];
    NSLog(test2);
    [pool release];
    return 0;
}

NSString * test3 = [test stringByAppendingString:[test2 stringByAppendingString:@" Adding a third string."]];

// test = test 임!
// test2 = test 임! test에 추가함 ! 또 추가함 !
// test3 = test 임!test 임! test에 추가함 ! 또 추가함 !
```