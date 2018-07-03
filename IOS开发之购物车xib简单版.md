## IOS开发之购物车xib简单版

**`ZJShopView.m`**


```objc
#import "ZJShopView.h"
#import "ZJShop.h"
@interface ZJShopView ()
@property (weak, nonatomic) IBOutlet UIImageView *imageView;
@property (weak, nonatomic) IBOutlet UILabel *labelTitle;
//@property(strong,nonatomic)ZJShop *shop;
@end
@implementation ZJShopView
-(void)setShop:(ZJShop *)shop{
    self.imageView.image = [UIImage imageNamed:shop.img];
    self.labelTitle.text = shop.name;
}
+(instancetype)shopView{
    return [[[NSBundle mainBundle] loadNibNamed:NSStringFromClass(self) owner:nil options:nil] firstObject];
}

//对xib进行改变大小等外观设置
- (void)awakeFromNib{
    [super awakeFromNib];
    self.imageView.frame = CGRectMake(0, 0,self.frame.size.width, (self.frame.size.width - 10));
    self.labelTitle.frame = CGRectMake(0, (self.frame.size.width - 10), self.frame.size.width, 20);
    
    self.backgroundColor = [UIColor colorWithRed:0 green:0 blue:0 alpha:0];
}
@end
```

**`ZJShopView.h`**

```objc
#import <UIKit/UIKit.h>
@class ZJShop;
@interface ZJShopView : UIView
+(instancetype)shopView;
-(void)setShop:(ZJShop *)shop;
@end

```

**`ViewController`**

```objc
#import "ViewController.h"
#import "ZJShop.h"
#import "ZJShopView.h"
@interface ViewController ()
@property(nonatomic,strong)UIView *shopCar;
@property(nonatomic,strong)UIButton *addBtn;
@property(nonatomic,strong)UIButton *removeBtn;
@property(nonatomic,strong)NSArray *arr;
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    //判断是否存在文件
    NSFileManager *fileManager = [NSFileManager defaultManager];
    NSString *shops = [[NSBundle mainBundle] pathForResource:@"shops.plist" ofType:nil];
    BOOL boolean = [fileManager fileExistsAtPath:shops];
    if(boolean){
        NSArray<NSDictionary *> *arr = [NSArray arrayWithContentsOfFile:shops];
        self.arr = arr;
    }else{
        NSArray<NSDictionary *> *arr = @[
             @{@"name":@"单肩包",@"img":@"danjianbao"},
             @{@"name":@"链条包",@"img":@"liantiaobao"},
             @{@"name":@"钱包",@"img":@"qianbao"},
             @{@"name":@"手提包",@"img":@"shoutibao"},
             @{@"name":@"双肩包",@"img":@"shuangjianbao"},
             @{@"name":@"斜挎包",@"img":@"xiekuabao"}
         ];
        NSBundle *bundle = [NSBundle mainBundle];
        NSString *str = bundle.bundlePath;
        NSRange rangeLocal = [str rangeOfString:@"/" options:NSBackwardsSearch];
        NSRange range= NSMakeRange(([str length] - [str length]), rangeLocal.location);
        NSString *pathStr = [str substringWithRange:range];
        
        NSMutableString *mutablePath = [NSMutableString string];
        [mutablePath appendFormat:@"%@/",pathStr];
        [mutablePath appendString:@"shops.plist"];
        [arr writeToFile:mutablePath atomically:YES];
        self.arr = arr;
    }
    //将数组遍历，然后转成ZJShop模型存入arr数组中
    NSMutableArray *arr = [NSMutableArray array];
    for (NSDictionary *dictionary in self.arr) {
        ZJShop * shop = [[ZJShop alloc] initWithDict:dictionary];
        [arr addObject:shop];
    }
    self.arr = arr;
  
    //创建UIView
    UIView *uiView = [[UIView alloc] initWithFrame: CGRectMake(16, 269, 343, 241)];
    //设置uiView背景
    uiView.backgroundColor = [UIColor colorWithRed:245/255.0 green:100/255.0 blue:0/255.0 alpha:1];
    //将UIView设置到当前ViewController中
    [self.view addSubview:uiView];
    self.shopCar = uiView;
    
    //添加按钮
    UIButton *addBtn = [UIButton buttonWithType:UIButtonTypeCustom];
    addBtn.frame = CGRectMake(16, (uiView.frame.origin.y-50-10), 50, 50);
    [addBtn setTitle:@"添加" forState:UIControlStateNormal];
    [addBtn setBackgroundColor:[UIColor redColor]];
    [addBtn setTitle:@"高亮添加" forState:UIControlStateHighlighted];
    //虽然titleLabel是readonly，但是其内部的font是可修改的
    addBtn.titleLabel.font = [UIFont systemFontOfSize:12.f];
    //绑定单击事件
    [addBtn addTarget:self action:@selector(addGood:) forControlEvents:UIControlEventTouchUpInside];
    self.addBtn = addBtn;
    //删除按钮
    UIButton *removeBtn = [UIButton buttonWithType:UIButtonTypeCustom];
    removeBtn.frame = CGRectMake(uiView.frame.size.width + 16 - 50, (uiView.frame.origin.y-50-10), 50, 50);
    [removeBtn setTitle:@"移除" forState:UIControlStateNormal];
    [removeBtn setBackgroundColor:[UIColor greenColor]];
    [removeBtn setTitle:@"高亮移除" forState:UIControlStateHighlighted];
    //虽然titleLabel是readonly，但是其内部的font是可修改的
    removeBtn.titleLabel.font = [UIFont systemFontOfSize:12.f];
    //绑定单击事件
    [removeBtn addTarget:self action:@selector(removeGood:) forControlEvents:UIControlEventTouchUpInside];
    self.removeBtn = removeBtn;
    //绑定到ViewController
    [self.view addSubview:removeBtn];
    [self.view addSubview:addBtn];
}

//添加事件
-(void)addGood:(UIButton *) this{
    
    //一排三个
    NSInteger num = 3;
    //宽度
    NSInteger width = 100;
    //高度
    NSInteger height = 110;
    //已添加的包包个数
    NSArray *arr = self.shopCar.subviews;
    NSUInteger index = [arr count];
    
    //设置坐标
    //x
    NSUInteger xPoint = index % num * (width + (self.shopCar.frame.size.width - width * num ) / (num - 1));
    //y
    NSUInteger yPoint = index / num * (height + (self.shopCar.frame.size.height - height * 2 ) / 1);
    //设置商品包包
    CGRect rect = CGRectMake(xPoint, yPoint, width, height);
    ZJShop *shop = self.arr[index];
    ZJShopView *shopView = [ZJShopView shopView];
    shopView.frame = rect;
    [shopView setShop:shop];
    [self.shopCar addSubview:shopView];
    
    //如果购物车放满，则不允许在添加商品
    this.enabled = self.shopCar.subviews.count != 6;
    //移除按钮可以使用
    self.removeBtn.enabled = YES;
}
//移除事件
-(void)removeGood:(UIButton *) this{
    NSArray *arrGoods = self.shopCar.subviews;
    UIView *viewGood = [arrGoods lastObject];
    [viewGood removeFromSuperview];
    //如果没有商品，则移除操作无法进行
    if(self.shopCar.subviews.count == 0){
        this.enabled = NO;
    }
    self.addBtn.enabled = YES;
}

@end
```

