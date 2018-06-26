## IOS之设置UIButton的内容[文字|图片]的内边距

```objc
import "ViewController.h"
@interface ViewController ()
//绑定一个storyBoard中的按钮
@property (weak, nonatomic) IBOutlet UIButton *btnText;
@end
@implementation ViewController

/**
 内边距设置按顺时针即:top | right | bottom | left ---> 与css中的内外边距的设置顺序一样
 */
- (void)viewDidLoad {
    [super viewDidLoad];
    //设置按钮内容[包括文字和图片]的内边距
    //self.btnText.contentEdgeInsets = UIEdgeInsetsMake(0, 0, 10, 0);
    //设置按钮内容[包括文字]的内边距
    self.btnText.titleEdgeInsets = UIEdgeInsetsMake(100, 50, 50, 50);
    //设置按钮内容图片的内边距
    self.btnText.imageEdgeInsets = UIEdgeInsetsMake(100, 100, 100, 100);
}
@end

```