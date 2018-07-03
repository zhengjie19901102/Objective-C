## IOS开发之Xib笔记

**`实现部分`**

```objc
#import "ZJCarView.h"

@interface ZJCarView ()
@property (weak, nonatomic) IBOutlet UIImageView *imageName;
@property (weak, nonatomic) IBOutlet UILabel *labelTitle;
@property (weak, nonatomic) IBOutlet UILabel *labelDesc;
@property (weak, nonatomic) IBOutlet UIButton *btnAd;
@end

@implementation ZJCarView

//设置图片
-(void)setImage:(NSString *)image{
    UIImageView *imageView = self.imageName;
    [imageView setImage:[UIImage imageNamed:image]];
}

//设置标题
-(void)setTitle:(NSString *)title{
    UILabel *label = self.labelTitle;
    label.text = title;
    label.font = [UIFont boldSystemFontOfSize:17.f];
    label.lineBreakMode = NSLineBreakByTruncatingTail;
}

//设置描述信息
-(void)setDesc:(NSString *)desc{
    UILabel *descLabel = self.labelDesc;
    descLabel.text = desc;
    descLabel.font = [UIFont systemFontOfSize:14.f];
    descLabel.textColor = [UIColor colorWithRed:141/255.0 green:141/255.0 blue:141/255.0 alpha:1];
}

//设置按钮文字和背景颜色
- (void)setBtnName:(NSString *)btnName{
    UIButton *btn = self.btnAd;
    [btn setTitle:btnName forState:UIControlStateNormal];
    [btn.titleLabel setFont:[UIFont systemFontOfSize:12.f]];
    btn.backgroundColor = [UIColor colorWithRed:170/255.0 green:170/255.0 blue:170/255.0 alpha:1];
    btn.bounds = CGRectMake(0, 0, 48, 27);
}

//xib的view初始化使用initWithCoder
- (instancetype)initWithCoder:(NSCoder *)coder
{
    self = [super initWithCoder:coder];
    if (self) {
    }
    return self;
}

+(instancetype)charView{
    return [[[NSBundle mainBundle] loadNibNamed:@"Car" owner:nil options:nil] firstObject];
}

//Xib中加载view在初始化时期并未被唤醒，所以需要调用唤醒方法，对对象进行设置
- (void)awakeFromNib{
    [super awakeFromNib];
    UIToolbar *toolBar = [[UIToolbar alloc] init];
    toolBar.frame = self.imageName.bounds;
    [self.imageName addSubview:toolBar];
}
@end
```

**`声明部分`**

```objc
#import <UIKit/UIKit.h>

@interface ZJCarView : UIView
-(void)setImage:(NSString *)image;
-(void)setTitle:(NSString *)title;
-(void)setDesc:(NSString *)desc;
-(void)setBtnName:(NSString *)btnName;
+(instancetype)charView;
@end
```

**`ViewController`**

```objc
#import "ViewController.h"
#import "ZJCarView.h"
@interface ViewController ()

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    //方式1
    ZJCarView *view = [ZJCarView charView];
    [view setBtnName:@"365跟帖"];
    [view setImage:@"timg"];
    [view setDesc:@"很酷的跑车。跑车，很酷很酷的。很酷的跑车。跑车，很酷很酷的。很酷的跑车。跑车，很酷很酷的。很酷的跑车。跑车，很酷很酷的。很酷的跑车。跑车，很酷很酷的。很酷的跑车。跑车，很酷很酷的。很酷的跑车。跑车，很酷很酷的。"];
    [view setTitle:@"这是一辆跑车，非常的酷。是的，很酷！"];
    //设置位置
    view.frame = CGRectMake(0, 20, self.view.frame.size.width, 120);
    
//	  方式2
//    UINib *nib = [UINib nibWithNibName:@"Car" bundle:nil];
//    UIView *view = [[nib instantiateWithOwner:nib options:nil] firstObject];
    [self.view addSubview:view];
}
@end
```

`当xib与继承了UIView的类关联时即可进行拖线操作。`

xib中初始化view方法为**`initWithCoder`**而不是像代码创建`UIView`那样的**`initWithFrame`**和**`init`**方法。

xib中初始化时，各UIView还处于睡眠状态，如果要在Xib中已有的View中添加控件，则需要调用Xib对应的**`awakeFromNib`**方法。在**`awakeFromNib`**方法中进行添加控件。