## IOS约束动画[修改约束]

```objc
#import "ViewController.h"

@interface ViewController ()
@property (weak, nonatomic) IBOutlet NSLayoutConstraint *widthConstrant;
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
}


-(void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{
    self.widthConstrant.constant = 50.f;
    //设置刷新动画
    [UIView animateWithDuration:2.f animations:^{
        //父控件刷新布局
        [self.view layoutIfNeeded];
    }];
}
@end
```

**`重点: 约束也是对象[万物皆对象],只要是对象，那么在storyboard中的约束就可以通过连线来修改其对应属性值。`**