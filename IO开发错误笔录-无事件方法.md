## IOS开发错误笔录-方法事件方法

```objc
2018-06-06 10:11:13.353049+0800 test[2289:54707] -[ViewController openFile:]: unrecognized selector sent to instance 0x7fce5a606920
2018-06-06 10:11:13.359526+0800 test[2289:54707] *** Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '-[ViewController openFile:]: unrecognized selector sent to instance 0x7fce5a606920'
*** First throw call stack:
(
	0   CoreFoundation                      0x000000010cebf1e6 __exceptionPreprocess + 294
	1   libobjc.A.dylib                     0x0000000109cd8031 objc_exception_throw + 48
	2   CoreFoundation                      0x000000010cf40784 -[NSObject(NSObject) doesNotRecognizeSelector:] + 132
	3   UIKit                               0x000000010a7a273b -[UIResponder doesNotRecognizeSelector:] + 295
	4   CoreFoundation                      0x000000010ce41898 ___forwarding___ + 1432
	5   CoreFoundation                      0x000000010ce41278 _CF_forwarding_prep_0 + 120
	6   UIKit                               0x000000010a575448 -[UIApplication sendAction:to:from:forEvent:] + 83
	7   UIKit                               0x000000010a6f0804 -[UIControl sendAction:to:forEvent:] + 67
	8   UIKit                               0x000000010a6f0b21 -[UIControl _sendActionsForEvents:withEvent:] + 450
	9   UIKit                               0x000000010a6efa69 -[UIControl touchesEnded:withEvent:] + 580
	10  UIKit                               0x000000010a5ea11f -[UIWindow _sendTouchesForEvent:] + 2729
	11  UIKit                               0x000000010a5eb821 -[UIWindow sendEvent:] + 4086
	12  UIKit                               0x000000010a58f370 -[UIApplication sendEvent:] + 352
	13  UIKit                               0x000000010aed057f __dispatchPreprocessedEventFromEventQueue + 2796
	14  UIKit                               0x000000010aed3194 __handleEventQueueInternal + 5949
	15  CoreFoundation                      0x000000010ce61bb1 __CFRUNLOOP_IS_CALLING_OUT_TO_A_SOURCE0_PERFORM_FUNCTION__ + 17
	16  CoreFoundation                      0x000000010ce464af __CFRunLoopDoSources0 + 271
	17  CoreFoundation                      0x000000010ce45a6f __CFRunLoopRun + 1263
	18  CoreFoundation                      0x000000010ce4530b CFRunLoopRunSpecific + 635
	19  GraphicsServices                    0x000000010f7aca73 GSEventRunModal + 62
	20  UIKit                               0x000000010a5740b7 UIApplicationMain + 159
	21  test                                0x00000001093d87ff main + 111
	22  libdyld.dylib                       0x000000010e09c955 start + 1
	23  ???                                 0x0000000000000001 0x0 + 1
)
libc++abi.dylib: terminating with uncaught exception of type NSException

```

以上错误异常栈得出: 问题出在 `-[ViewController openFile:]:unrecognized selector sent to instance 0x7fce5a606920'...`这处。
经检查，是因为对应控件的事件方法被删除，但是控件还连线着事件方法，导致控件无法找到对应的事件从而抛出异常。