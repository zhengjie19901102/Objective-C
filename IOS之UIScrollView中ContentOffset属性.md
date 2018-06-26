## IOS之UIScrollView中ContentOffset和contentInset属性

```objc
#import "ViewController.h"
@interface ViewController ()
@property (weak, nonatomic) IBOutlet UIScrollView *scrollView;
@end
@implementation ViewController
- (void)viewDidLoad {
    [super viewDidLoad];
    //设置图片到scrollView中
    UIImageView *imageView = [[UIImageView alloc] initWithImage:[UIImage imageNamed:@"btn"]];
    [self.scrollView addSubview:imageView];
    //给scrollView开启滚定
    self.scrollView.contentSize = imageView.frame.size;
    //给scrollView设置背景色
    self.scrollView.backgroundColor = [UIColor redColor];
    //设置scrollView的内边距。
    /**
     * ScrollView中的ContentSize计算仍旧为设置的contentSize长宽。内边距不计入contentSize中
     */
    self.scrollView.contentInset = UIEdgeInsetsMake(10, 10, 10, 10);
}
//上
- (IBAction)top {
    [UIView animateWithDuration:0.7 animations:^{
        self.scrollView.contentOffset = CGPointMake(self.scrollView.contentOffset.x, 0);
    }];
}
//下
- (IBAction)bottom {
    [UIView animateWithDuration:0.7 animations:^{
        //计算下边坐标距离
        CGFloat pointY = (self.scrollView.contentSize.height - self.scrollView.frame.size.height);
        CGFloat pointX = self.scrollView.contentOffset.x;
        self.scrollView.contentOffset = CGPointMake(pointX, pointY);
    }];
}
//左
- (IBAction)left {
    [UIView animateWithDuration:0.7 animations:^{
        self.scrollView.contentOffset = CGPointMake(0, self.scrollView.contentOffset.y);
    }];
}
//右
- (IBAction)right {
    [UIView animateWithDuration:0.7 animations:^{
        CGFloat pointX = (self.scrollView.contentSize.width - self.scrollView.frame.size.width);
        self.scrollView.contentOffset = CGPointMake(pointX, self.scrollView.contentOffset.y);
    }];
}
//右上
- (IBAction)rightTop {
    [UIView animateWithDuration:0.7 animations:^{
        //右边坐标
        CGFloat pointX = (self.scrollView.contentSize.width - self.scrollView.frame.size.width);
        self.scrollView.contentOffset = CGPointMake(pointX, 0);
    }];
}
//左下
- (IBAction)leftBottom {
    [UIView animateWithDuration:0.7 animations:^{
        //计算下边坐标距离
        self.scrollView.contentOffset = CGPointMake(0,self.scrollView.contentSize.height - self.scrollView.frame.size.height );
    }];
}

@end
```

**`重点: 按ScrollView可见视图的左上角坐标(0,0)进行计算。是内容的X或Y和ScrollView的左上角坐标X和Y的差值。`**