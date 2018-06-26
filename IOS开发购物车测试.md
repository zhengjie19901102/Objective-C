## IOS开发购物车测试

```objc
//
//  ViewController.m
//  购物车测试
//
//  Created by on 2018/6/15.
//  Copyright © 2018年 heiketu. All rights reserved.
//

#import "ViewController.h"

@interface ViewController ()
    //购物车
    @property(nonatomic,strong)UIView *shopCar;
    //添加按钮
    @property(nonatomic,strong)UIButton *addBtn;
    //移除按钮
    @property(nonatomic,strong)UIButton *reBtn;
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    //将购物车添加至ViewController中
    UIView *shopCar = [self createUIView];
    self.shopCar = shopCar;
    [self.view addSubview:shopCar];
    
    //添加按钮
    UIButton *btnAdd = [self createBtn:YES];
    [btnAdd addTarget:self action:@selector(addGood:) forControlEvents:UIControlEventTouchUpInside];
    //删除按钮
    UIButton *btnRemove = [self createBtn:NO];
    [btnRemove addTarget:self action:@selector(removeGood:) forControlEvents:UIControlEventTouchUpInside];
    
    //绑定添加事件
    //绑定删除事件
    
    [self.view addSubview:btnAdd];
    [self.view addSubview:btnRemove];
}

-(UIView *)createUIView{
    //创建UIView
    UIView *view = [[UIView alloc] initWithFrame:CGRectMake(23, 203, 352, 252)];
    view.backgroundColor = [UIColor colorWithRed:243/255.0 green:220/255.0 blue:120/255.0 alpha:1];
    return view;
}

-(UIButton *)createBtn:(BOOL)addOrRemove{
    //添加按钮和删除按钮
    UIButton *btn = [UIButton buttonWithType:UIButtonTypeCustom];
    if(addOrRemove){
        btn.frame = CGRectMake(23, (203-50-10), 50, 50);
        btn.backgroundColor = [UIColor greenColor];
        [btn setTitle:@"添加" forState:UIControlStateNormal];
    }else{
        btn.frame = CGRectMake(((352+23)-50), (203-50-10), 50, 50);
        btn.backgroundColor = [UIColor redColor];
        [btn setTitle:@"删除" forState:UIControlStateNormal];
    }
    return btn;
}

//添加事件
-(void) addGood:(UIButton *)this{
    
    self.addBtn = this;
    
    //当前购物车的长
    NSUInteger shopCarWidth = self.shopCar.frame.size.width;
    //当前购物车的宽
    NSUInteger shopCarHeight = self.shopCar.frame.size.height;
    //一排放的个数
    NSInteger num = 3;
    //固定商品的长
    NSInteger width = 100;
    //固定商品的宽
    NSInteger height = 120;
    //当前购物车中的商品数组
    NSArray<UIView *> *shopCarSubViews = self.shopCar.subviews;
    //当前购物车中的物品数量[坐标]
    NSUInteger indes = shopCarSubViews.count;
    //X轴坐标
    NSInteger xPoint = (indes % num) * (width + (shopCarWidth - width * num) / (num - 1));
    //Y轴坐标
    NSInteger yPoint = (indes / num) * (height + (shopCarHeight - height * (num-1)) / 1);
    UIView *good = [[UIView alloc] initWithFrame:CGRectMake(xPoint, yPoint, width, height)];
    [good setBackgroundColor:[UIColor greenColor]];
    //添加至当前购物车
    [self.shopCar addSubview:good];
    //关闭添加按钮
    this.enabled = shopCarSubViews.count != 5;
    //移除按钮要开启
    self.reBtn.enabled = YES;
    
}
//删除商品
-(void) removeGood:(UIButton *)this{
    self.reBtn = this;
    UIView *view = [self.shopCar.subviews lastObject];
    [view removeFromSuperview];
    self.addBtn.enabled = YES;
    this.enabled = self.shopCar.subviews.count != 0;
}

@end
```
