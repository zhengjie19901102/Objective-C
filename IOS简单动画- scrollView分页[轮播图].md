## IOS简单动画: scrollView分页[轮播图]

```objc
#import "ViewController.h"
@interface ViewController ()
@property (weak, nonatomic) IBOutlet UIScrollView *scrollView;
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    int count = 3;
    CGFloat width = self.scrollView.frame.size.width;
    CGFloat height = self.scrollView.frame.size.height;
    //设置滚动尺寸，宽度大于scrollView宽度才能滚动
    self.scrollView.contentSize = CGSizeMake(width * count, height);
    for (int i = 0; i < count; i++) {
        UIImageView *imageView = [[UIImageView alloc] initWithImage:[UIImage imageNamed:[NSString stringWithFormat:@"%i.jpeg",i]]];
        imageView.frame = CGRectMake(i * width, 0, width, height);
        [self.scrollView addSubview:imageView];
    }
    //scrollView开启分页[IOS内置]
    self.scrollView.pagingEnabled = YES;
    
    //---> 分页功能不需要滚动条，可以用代码，也可以在storyBoard中勾去:showsHorizontalScrollIndicator和showsVerticalScrollIndicator
}
@end
```