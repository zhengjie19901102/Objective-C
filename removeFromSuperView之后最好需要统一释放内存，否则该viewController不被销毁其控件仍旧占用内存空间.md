## removeFromSuperView之后最好需要统一释放内存，否则该viewController不被销毁其控件仍旧占用内存空间

```objc
@interface ViewController ()
//@property (weak, nonatomic) IBOutlet UIButton *btn1;
//@property (weak, nonatomic) IBOutlet UIButton *btn2;
//@property (weak, nonatomic) IBOutlet UIButton *btn3;
@property (weak, nonatomic) IBOutlet UIView *panel;
@property(nonatomic,weak) UISegmentedControl *arSeg;

@end

@implementation ViewController

//视图加载完成,此时还未开始出现(显示)
- (void)viewDidLoad {
    [super viewDidLoad];
}

//视图加载完成，将要显示(还未显示)
- (void)viewWillAppear:(BOOL)animated{
    [super viewWillAppear:animated];
}

//视图已经加载完成，且已经显示
- (void)viewDidAppear:(BOOL)animated{
    [super viewDidAppear: animated];
    
    UISegmentedControl *seg = [[UISegmentedControl alloc] initWithItems:@[@"😝",@"☺️",@"😊"]];
//    [self.view addSubview:seg]; //这一行会无效，因为一个控件只能有一个父控件
    [self.panel addSubview:seg];
    self.arSeg = seg;
    
    [self.panel removeFromSuperview]; //如果父类被移除，其子类同样会被移除掉。原因是因为实践上storyboard的xib是一个xml文件，父标签被干掉了子标签也就没有了。
    
    self.panel = nil;
    self.arSeg = nil;
    
}

//接收内存警告
- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
}

/*
- (IBAction)clickBtn:(UIButton *)sender {
    NSInteger integer = sender.tag;
    switch (integer) {
        case 1:
            NSLog(@"按了第一个按钮");
            break;
        case 2:
            NSLog(@"按了第二个按钮");
            break;
        case 3:
            NSLog(@"按了第三个按钮");
            break;
        default:
            NSLog(@"按了不是按钮");
    }
    NSLog(@"公共的事情");
}
 */

@end
``