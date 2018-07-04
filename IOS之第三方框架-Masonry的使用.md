## IOS之第三方框架:Masonry的使用

`测试代码`

```objc
#import "ViewController.h"
//使用第三方框架:Masonry
/*
 //define this constant if you want to use Masonry without the 'mas_' prefix
 //如果你想使用Masonry排除掉'mas_'前缀，那么需要定义该宏
 #define MAS_SHORTHAND
 
 //define this constant if you want to enable auto-boxing for default syntax
  //如果你想为默认的语法开启自动边框，那么添加该宏
 #define MAS_SHORTHAND_GLOBALS
 

 --- 两个宏必须定义在头文件之上: 否则会无法识别简化的方法[报错]
 */

#import "Masonry.h"
@interface ViewController ()
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    //创建UIView空间:红色View
    UIView *redView = [[UIView alloc] init];
    redView.backgroundColor = [UIColor redColor];
    //创建UIView空间:蓝色View
    UIView *blueView = [[UIView alloc] init];
    blueView.backgroundColor = [UIColor blueColor];
    //讲UIView添加进父控件中
    [self.view addSubview:redView];
    [self.view addSubview:blueView];
    //通过Masonry添加View约束:将view放置于中心点位置，长宽各位100
//    [view mas_makeConstraints:^(MASConstraintMaker *make) {
//        make.width.mas_equalTo(100);
//        make.height.mas_equalTo(100);
//        make.center.mas_equalTo(self.view);
//    }];

    /*
     width:
     and:
     - (MASConstraint *)with {
     return self;
     }
     - (MASConstraint *)and {
     return self;
     }
     -- 都是返回自己本身，属于语言修饰属性
     */
    //设置蓝色View的约束
    [blueView mas_makeConstraints:^(MASConstraintMaker *make) {
        //蓝色View高度等于50
        make.height.mas_equalTo(50);
        //蓝色View的左边比父控件的左边要向右偏移20
        make.left.mas_equalTo(self.view.mas_left).mas_offset(20);
        //蓝色View的宽度等于红色View的宽度
        make.width.mas_equalTo(redView.mas_width);
        //记住:蓝色View比红色View的右边坐标要向左偏移20，也就是小了20[-20]
        make.right.mas_equalTo(redView.mas_left).offset(-20);
        //记住:蓝色View比父控件的底部坐标要向上偏移20, 也就是小了20[-20]
        make.bottom.mas_equalTo(self.view.mas_bottom).offset(-20);
    }];
    //设置红色View的约束
    [redView mas_makeConstraints:^(MASConstraintMaker *make) {
        //红色View的宽度等于蓝色的View:
        //因为已经有蓝色View限制了红色View的宽度两者一样，所以红色View的宽度约束可以不用重复设置
        make.width.mas_equalTo(blueView.mas_width);
        //红色View的右边比父控件的右边要向左偏移20[-20]
        make.right.mas_equalTo(self.view.mas_right).offset(-20);
        //红色View的顶部与蓝色View的顶部对齐[偏移量为0]:offset可以省略
        make.top.mas_equalTo(blueView.mas_top).offset(0);
        //红色View的底部与蓝色View的底部对齐[偏移量为0]:offset可以省略
        make.bottom.mas_equalTo(blueView.mas_bottom).offset(0);
    }];
}
@end
```

因为`Masonry`为第三方框架，所以需要导入第三方框架至当前项目中。

按`规范`第三方框架一般导入同名的目录即可。即:
要导入`Masonry`框架则在下载来的框架中找到同名的目录，拖拽至项目中即可。