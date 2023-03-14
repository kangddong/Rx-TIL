  
`BOOL`  스칼라 유형은 `YES` 또는 `NO` 인 부울 값을 보유하기 위해 `Objective-C` 에서 정의된다. 예상대로 `YES` 는 논리적으로 `true`와 `1`에 해당하는 반면 `NO`는 `false`와 `0`에 해당한다.  

`true`는 0이 아닌 수들을 뜻하지만
`YES`는 오직 1이다
``
`BOOL` 타입은 `obc.h`에 따라서 `signed char` 타입이다

```objc
bool b1 = 2;
if (b1) printf("CATCH b1 \n");
if (b1 != true) printf("NOT CATCH b1 \n");

BOOL b2 = 2;
if (b2) printf("CATCH b2 \n");
if (b2 != YES) printf("NOT CATCH b2 \n");
```

**CATCH b1  
CATCH b2  
NOT CATCH b2**


```objc

bool ansicBool = 64;
   
   if(ansicBool != true) printf("print되지 않음\n");
   printf("ansicBoool 이외의 모든 주어진 값은 1로 평가됩니다 %i\n", ansicBool);
   
   BOOL objcBOOL = 64;
   
   if(objcBOOL != YES) printf("cpu architecture에 따라 출력될 수 있다.\n");
   printf("BOOL 은 %i 로 할당한 값을 유지할 것이다.\n", objcBOOL);
   
   if(!objcBOOL) printf("print되지 않음\n");
   printf("! 연산자는 objcBOOL이 0으로 될 것이다 결과: %i\n", !objcBOOL);
   
   if(!!objcBOOL) printf("!! 연산자는 objcBOOL가  %i 로 평가 될 것이다.\n", !!objcBOOL);
```