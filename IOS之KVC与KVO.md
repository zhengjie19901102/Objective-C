## IOS之KVC与KVO

名词全称:

缩写 | 全称 
----|-----
KVC | Key Value Coding
KVO | Key Value Observing

**`KVC相关示例代码:`**

```objc

/******** 测试代码部分 ********/

#import <Foundation/Foundation.h>
#import "ObjectClass.h"
/**
 注意: 因为KVC中字典转模型，和模型转字典是直接赋值操作。所以如果模型对象中又嵌套了一个模型对象属性，那么
 转换会失败，如果成功那么结果也不是我们需要的。所以此时我们需要借助第三方框架来转换。
 */
int main(int argc, const char * argv[]) {
    //KVC能设置私用属性的的值,会自动转换数据类型。forKey参数中系统会自动判断属性的名称，所以@"_age"或@"age"都可以
    ObjectClass *class = [[ObjectClass alloc] init];
    [class setValue:[NSNumber numberWithInteger:13] forKey:@"_age"];
    [class setValue:@"十三章" forKey:@"name"];
    //打印设置的对象
    NSLog(@"%@",class);
    //打印设置的值[通过valueForKey获取的是id对象，所以需要转换成对应的数据类型]
    int age = [[class valueForKey:@"age"] intValue];
    NSLog(@"%i",age);
    
    //KVC能将对象转成NSDictionary对象
    NSDictionary *ns = [class dictionaryWithValuesForKeys:@[@"age",@"name"]];
    NSLog(@"%@",ns);
    
    //KVC还能将NSDictionary对象转换成对象
    NSMutableDictionary *dict = [NSMutableDictionary dictionary];
    [dict setObject:@12 forKey:@"age"];
    [dict setObject:@"name" forKey:@"name"];
    [class setValuesForKeysWithDictionary:dict];
    NSLog(@"%@",class);
    
    return 0;
}


/******** 对象部分 ********/
#import "ObjectClass.h"
//implementation:
@implementation ObjectClass
{
    int _age;
    NSString *name;
}

//相当于java的toString方法。当打印类对象时，系统会自动调用description方法
-(NSString *)description{
    return [NSString stringWithFormat:@"age = %i,name = %@",self->_age,self->name];
}
@end

//interface:
#import <Foundation/Foundation.h>
@interface ObjectClass : NSObject
@end


```

**`KVO相关示例代码:`**

```objc
#import "ViewController.h"
#import "obj.h"

/******** implementation部分 ********/

@interface ViewController ()
@end
@implementation ViewController
- (void)viewDidLoad {
    [super viewDidLoad];
    obj *ob = [[obj alloc] init];
    ob.age=12;
    /* 给对象添加监听器
     * addObserver: 谁做为监听器
     * forKeyPath: 要监听的属性名
     * options: 监听选项[当监听对象的属性发生改变时，返回的是改变后属性的值还是改变前属性的值]
     * context: 上下文对象[暂时不知道干嘛用的]
     */
    [ob addObserver:self forKeyPath:@"age" options:NSKeyValueObservingOptionNew|NSKeyValueObservingOptionOld context:nil];
    //改变对象的属性值
    ob.age=14;
    //给对象移除监听器
    [ob removeObserver:self forKeyPath:@"age"];
}

/**
 observeValueForKeyPath: 给监听者添加监听事件
 @param keyPath 监听的属性名
 @param object 监听属性的所属对象
 @param change 监听的属性改变前或后的值[一个字典对象]
 @param context 上下文对象[暂不知道干嘛用的]
 */
- (void)observeValueForKeyPath:(NSString *)keyPath ofObject:(id)object change:(NSDictionary<NSKeyValueChangeKey,id> *)change context:(void *)context{
    NSLog(@"keyPath:%@ --- ofObject:%i --- change:%@",keyPath,[object performSelector:@selector(age)],change);
}
@end



/******** interface部分 ********/
#import <UIKit/UIKit.h>
@interface ViewController : UIViewController
@end



/******** object部分[interface和implements] ********/
#import <Foundation/Foundation.h>
@interface obj : NSObject
@property(nonatomic,assign)int age;
@property(nonatomic,copy)NSString *name;
@end

#import "obj.h"
@implementation obj
@end


```

