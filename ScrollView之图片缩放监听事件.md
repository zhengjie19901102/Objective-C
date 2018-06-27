## ScrollView之图片缩放监听事件

```objc
#import "ViewController.h"

@interface ViewController () <UIScrollViewDelegate>
@property (weak, nonatomic) IBOutlet UIScrollView *scrollView;
@property(weak,nonatomic) UIImageView *imageView;
@end

@implementation ViewController

/**
 * 模拟器如何模拟手指缩放手势: 按住option[也就是alt]键 + 鼠标单击键-->  在屏幕中央会出现俩个灰色圆点，此时单击并移动鼠标就是代表缩放手势
 因为模拟器手势默认开始出现位置为屏幕中间，所以要移动手势则需要符合键: option[alt] + shift + 鼠标移动 ---> 移动手势至指定位置
 */
- (void)viewDidLoad {
    [super viewDidLoad];
    UIImageView *imageView = [[UIImageView alloc] initWithImage:[UIImage imageNamed:@"timg.jpeg"]];
    //将图片设置到scrollView中
    [self.scrollView addSubview:imageView];
    self.imageView = imageView;
    //设置scrollView的ContentSize为图片的尺寸
    self.scrollView.contentSize = imageView.frame.size;
    
    //指定好我们要缩放的图片后，给scrollView指定图片的缩放比:[最大 | 最小]
    self.scrollView.minimumZoomScale = 0.5;
    self.scrollView.maximumZoomScale = 2.0;
}

//让scrollView知道我们要缩放的是它内部的那个图片[别的容器等]
- (UIView *)viewForZoomingInScrollView:(UIScrollView *)scrollView{
    //给scrollView返回我们指定添加的imageView
    return self.imageView;
}
@end
```