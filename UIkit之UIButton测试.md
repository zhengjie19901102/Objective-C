## UIkit之UIButton测试

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    //创建一个UIButton按钮
    UIButton *uiBtn = [UIButton buttonWithType:UIButtonTypeCustom];
    uiBtn.frame = CGRectMake(0, 0, 100, 60);
    //设置按钮文字:正常状态
    [uiBtn setTitle:@"按钮" forState:UIControlStateNormal];
    //设置文字颜色:正常状态
    [uiBtn setTitleColor:[UIColor colorWithRed:243/255.0 green:234/255.0 blue:123/255.0 alpha:0.8] forState:UIControlStateNormal];
    //设置按钮高亮状态
    [uiBtn setTitle:@"高亮文字" forState:UIControlStateHighlighted];
    //设置按钮的高亮文字颜色
    [uiBtn setTitleColor:[UIColor colorWithRed:0 green:255 blue:0 alpha:1] forState:UIControlStateHighlighted];
    //设置按钮背景
    uiBtn.backgroundColor = [UIColor colorWithRed:255 green:0 blue:0 alpha:1];
    
    //获取文字
    UILabel *label = [uiBtn titleLabel];
    NSLog(@"%@",label.text);
    
//    UIImage *image = [uiBtn backgroundImageForState:UIControlStateHighlighted];
//   CGImageRef cf = image.CGImage;
    
    //给按钮添加事件
    [uiBtn addTarget:self action:@selector(getBtn:) forControlEvents:UIControlEventTouchUpInside];
    //添加按钮至viewController中
    [self.view addSubview:uiBtn];
}

//事件测试
-(void)getBtn:(UIButton *)button{
    NSLog(@"执行了单击按钮");
    button.enabled = NO;
}
```