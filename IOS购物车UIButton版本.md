## IOS购物车UIButton版本备忘笔录

**`UIButton代码:`**

```objc
/**		interface部分	*/
#import <UIKit/UIKit.h>
@class ZJShop;
@interface ZJButton : UIButton
@property(nonatomic,strong)ZJShop *shop;
@end

/**		implements部分	*/
#import "ZJButton.h"
#import "ZJShop.h"
@implementation ZJButton
-(void)layoutSubviews{
    //别忘了调用父类的layoutSubviews方法
    [super layoutSubviews];
    CGFloat width = self.frame.size.width;
    CGFloat height = self.frame.size.height;
    //设置图片及文字的位置大小
    self.imageView.frame = CGRectMake(0, 0, width, width);
    self.titleLabel.frame = CGRectMake(0,width,width,width - height);
}

//获取数据进按钮中
- (void)setShop:(ZJShop *)shop{
    _shop = shop;
    //设置图片及文字
    NSString *img = shop.img;
    [self setImage:[UIImage imageNamed:img] forState:UIControlStateNormal];
    [self setTitle:shop.name forState:UIControlStateNormal];
    self.titleLabel.textAlignment = NSTextAlignmentCenter;
    self.titleLabel.font = [UIFont systemFontOfSize:14.f];
}
@end
```