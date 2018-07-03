## Objective-C轻量级泛型

类声明部分:

```objc
@interface TestClass<__covariant T> : NSObject
	@property(nonatomic,weak) T art;
@end
```

类实现部分:

```objc
#import "TestClass.h"
@implementation TestClass
    @synthesize art = _art;
@end
```

测试部分:

```objc
#import <Foundation/Foundation.h>
#import "TestClass.h"
int main(int argc, const char * argv[]) {
    TestClass<NSString *> *c = [[TestClass alloc] init];
    c.art = @"ouy";
    NSLog(@"%@",c.art);
    return 0;
}
```

从测试结果可以看出,当我们声明类时，在声明类的`.h`文件中加上了`<__covariant T>`就可以使用泛型类型`T`来进行定义我们的属性返回值等信息。


泛型约束(类型限定):

```objc
#import <Foundation/Foundation.h>
@class TestClass;
#import "FilesNem.h"
@interface TypeTest : NSObject
	@property(nonatomic,weak)TestClass<FilesNem> *arr;
@end
```

通过在属性类型后加上`<...>`限定类型的范围，`<>`中是需要制定的协议。那么属性必须实现该协议，否则会报警告(**`最好当它是报错`**)。

`警告信息类似:Incompatible pointer types assigning to 'TestClass<FilesNem> *' from 'TestClass<NSString *> *'`

更详细参考: [Objective-C轻量级泛型](https://www.cnblogs.com/zenny-chen/p/5094075.html)