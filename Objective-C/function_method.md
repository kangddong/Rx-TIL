
# function & method

```objc

// 함수 모양새
- (return Type) 함수이름:(Type)parameter1, 별칭:(Type)parameter2,... , 별칭:(Type) parameterN
  {

        // 함수 body

   }

// 함수 선언의 예 

-(int) max:(int)num1 andNum2:(int)num2;

// 사용 예
sumNumbers: number1 number2: number2];
```


### +,- 심볼의 의미


`Objective-C` Method에서
기호 '-' 및 '+'는 메서드의 가시성과 범위를 나타내는 데 사용됩니다.

'-' 기호(static)는 클래스의 특정 인스턴스에 속하는 메서드인 인스턴스 메서드를 정의하는 데 사용됩니다. 이러한 메서드는 클래스의 인스턴스 변수 및 속성에 액세스할 수 있습니다. 예를 들어:

```objc
- (void)doSomething {
  // implementation code here
}
```


'+' 기호(class)는 클래스의 특정 인스턴스가 아닌 클래스 자체에 속하는 메서드인 클래스 메서드를 정의하는 데 사용됩니다. 이러한 메서드는 클래스 변수 및 속성에만 액세스할 수 있습니다. 예를 들어:

```objc
+ (void)doSomething {
  // implementation code here
}

```



따라서 Objective-C에서 메소드를 정의할 때
인스턴스 메소드에는 '-'를, 클래스 메소드에는 '+'를 사용하십시오.