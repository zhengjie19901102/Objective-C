## IOS之自定义Button按钮布局
效果图如下:

<img src="/Users/zhengjie/Documents/文档笔记/objective-C/img/btn1.png" alt="按钮" width="10%"/>

按钮部分俩部分:

> 上方为图片[UIimageView],
> 下方文字[UIlabel]

因为`UIButton`在创建后系统默认会自动固定按钮内图片和文字的位置**[会有默认布局]**。

所以对应那些系统控件，因为有些地方无法更改，那么我们就定义一个U控件继承父控件并重写默认控件的固定方法的方式来修改默认布局。

对于按钮有俩种方式。

* **`第一种继承父Button代码如下:`**

`定义类名: ZJBtn`

```objc
/**
 * @interface部分
 */
#import <UIKit/UIKit.h>
	@interface ZJBtn : UIButton
@end

/**
 * @implements部分
 */
#import "ZJBtn.h"
@implementation ZJBtn
	//通过重写系统默认调用方法:imageRectForContentRect:和titleRectForContentRect:
	//覆盖图片默认位置
	-(CGRect)imageRectForContentRect:(CGRect)contentRect{
    	return CGRectMake(100, 0, 100, 100);
	}
	
	//覆盖文字默认位置
	-(CGRect)titleRectForContentRect:(CGRect)contentRect{
	    return CGRectMake(0, 0, 100, 100);
	}
@end

/**
 * ViewController部分
 */
#import "ViewController.h"
#import "ZJBtn.h"
@interface ViewController ()
@end
@implementation ViewController
- (void)viewDidLoad {
    [super viewDidLoad];
    ZJBtn *navgate = [ZJBtn buttonWithType:UIButtonTypeCustom];
    //设置按钮在屏幕位置
    navgate.frame = CGRectMake(100, 100, 100, 120);
    //设置文字
    [navgate setTitle:@"按钮" forState:UIControlStateNormal];
    //设置文字区域背景
    [navgate setTitleColor:[UIColor blackColor] forState:UIControlStateNormal];
    //设置按钮的字体大小和样式[此处为粗体15号大小]
    [navgate.titleLabel setFont:[UIFont boldSystemFontOfSize:15.f]];
    //设置按钮的图片
    [navgate setImage:[UIImage imageNamed:@"timg"] forState:UIControlStateNormal];
    //创建完成后添加进ViewController中的UIView中进行显示
    [self.view addSubview:navgate];
}
@end

```

* **`第二种继承父Button代码如下:`**

`定义类名: ZJBtn`

```objc
/**
 * @interface部分
 */
#import <UIKit/UIKit.h>
	@interface ZJBtn : UIButton
@end

/**
 * @implements部分
 */
#import "ZJBtn.h"
@implementation ZJBtn
//覆盖初始化方法，对控件进行相应设置
-(instancetype)initWithFrame:(CGRect)frame{
    if(self = [super initWithFrame: frame]){
        //设置图片的内容模式，设置为按比例填充区域
        self.imageView.contentMode = UIViewContentModeScaleAspectFill;
        //让文字在文字区域居中显示
        self.titleLabel.textAlignment = NSTextAlignmentCenter;
    }
    return self;
}
//重写布局子控件方法，将图片和文字重新定位
-(void)layoutSubviews{
    [super layoutSubviews];
    self.imageView.frame = CGRectMake(0, 0, 100, 100);
    self.titleLabel.frame =  CGRectMake(0, 100,100,20);
}
@end

/**
 * ViewController部分
 */
#import "ViewController.h"
#import "ZJBtn.h"
@interface ViewController ()
@end
@implementation ViewController
- (void)viewDidLoad {
    [super viewDidLoad];
    ZJBtn *navgate = [ZJBtn buttonWithType:UIButtonTypeCustom];
    //设置按钮在屏幕位置
    navgate.frame = CGRectMake(100, 100, 100, 120);
    //设置文字
    [navgate setTitle:@"按钮" forState:UIControlStateNormal];
    //设置文字区域背景
    [navgate setTitleColor:[UIColor blackColor] forState:UIControlStateNormal];
    //设置按钮的字体大小和样式[此处为粗体15号大小]
    [navgate.titleLabel setFont:[UIFont boldSystemFontOfSize:15.f]];
    //设置按钮的图片
    [navgate setImage:[UIImage imageNamed:@"timg"] forState:UIControlStateNormal];
    //创建完成后添加进ViewController中的UIView中进行显示
    [self.view addSubview:navgate];
}
@end
```

**`重点总结: 在代码创建UIView的时候系统会调用initWithFrame方法，在initWithFrame方法中会创建对应的控件，设置控件的部分属性。如果是xib或nib创建的控件则是调用initWithCoder初始化控件。代码创建控件在初始化后会调用layoutSubviews方法，在此方法中设置位置布局。果是xib或nib创建的控件则需要唤醒子控件才能设置布局，所以是在awakeFromNib方法中。`**
