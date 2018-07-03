## IOS开发之简单购物车

**`自定义一个UIView控件`**

```objc

/**
 * 类实现部分
 */

#import "ZJShopView.h"
#import "ZJShop.h"
@interface ZJShopView ()
    @property(nonatomic,weak)UIImageView *imageView;
    @property(nonatomic,weak)UILabel *label;
    @property(nonatomic,strong)ZJShop *shop;
@end
@implementation ZJShopView
-(instancetype)initWithselfFrame:(CGRect)frame{
    if(self = [super init]){
        self.frame = frame;
    }
    return self;
}

+(instancetype)shopViewWithFrame:(CGRect)cgFrame{
    return [[self alloc] initWithselfFrame:cgFrame];
}

/** 设置图片 */
-(void)setImage{
    UIImage *img = [UIImage imageNamed:self.shop.img];
    UIImageView *imgView = [[UIImageView alloc] initWithImage:img];
    imgView.frame = CGRectMake(0, 0, self.frame.size.width, self.frame.size.width);
    //添加图片
    [self addSubview:imgView];
}

/** 设置文字 */
-(void)setLabel{
    UILabel *label = [[UILabel alloc] init];
    label.text = self.shop.name;
    label.frame = CGRectMake(0, self.frame.size.width, self.frame.size.width, (self.frame.size.height - self.frame.size.width));
    [label setTextAlignment:NSTextAlignmentCenter];
    label.font = [UIFont systemFontOfSize:12.f];
    [self addSubview:label];
}

/** 设置产品 */
-(void)setShop:(ZJShop *)shop{
    _shop = shop;
}

/** 布局子控件 */
-(void)layoutSubviews{
    /**
     * 设置图片
     */
    NSLog(@"layoutSubviews");
    [self setImage];
    /**
     * 设置文字
     */
    [self setLabel];
}
@end


/**
 * 类接口部分
 */
#import <UIKit/UIKit.h>
@class ZJShop;
@interface ZJShopView : UIView
	-(instancetype)initWithselfFrame:(CGRect)frame;
	-(void)setShop:(ZJShop *)shop;
	+(instancetype)shopViewWithFrame:(CGRect)cgFrame;
@end

```

**`UIViewController部分`**

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
    ZJShopView *shopView = [ZJShopView shopViewWithFrame:rect];
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

**`对象部分`**

```objc

/**
 * 接口部分
 */
#import <Foundation/Foundation.h>

@interface ZJShop : NSObject
/** 商品名 */
@property(nonatomic,strong) NSString *name;
/** 商品图片 */
@property(nonatomic,strong) NSString *img;
-(instancetype) initWithDict:(NSDictionary *)dictionary;
+(instancetype)shopWithDict:(NSDictionary *)dictionary;
@end

/**
 * 实现部分
 */
 #import "ZJShop.h"
@implementation ZJShop
    @synthesize name=_name,img=_img;
-(instancetype) initWithDict:(NSDictionary *)dictionary{
    if(self = [super init]){
        _name = dictionary[@"name"];
        _img = dictionary[@"img"];
    }
    return self;
}
+(instancetype)shopWithDict:(NSDictionary *)dictionary{
    return [[self alloc] initWithDict:dictionary];
}
@end
```

**`知识点总结`**

> `改变对象的大小等操作，会触发对象的layoutSubViews方法。`

> `在init初始化方法中，无法获取frame中的size等数据。因为此时并为对象设置长宽等数据。此时可以通过layoutSubViews方法中获取。触发layoutSubViews方法时已经将对象初始化完毕，所以也已经设置了对象的一些数据。`

**`layoutSubViews方法详细内容，参考`**[iOS - layoutSubviews总结（作用及调用机制）](https://www.jianshu.com/p/a2acc4c7dc4b)


