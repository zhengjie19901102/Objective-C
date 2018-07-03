## IOS开发之第一个小应用: 只会加法的计算器

首先创建一个`Single View App`项目。

在Main.storyboard中布局如下:

<img src="/Users/zhengjie/Documents/文档笔记/objective-C/img/img14.png" width=60%/>

布局中有以下控件:
两个`UITextField`控件，三个`UILabel`控件，一个`UIButton`控件。
给两个`UITextField`控件分别设置`Placeholder`为`第一个数字`和`第二个数字`。
将三个`UILabel`的`Text`的分别设置为`+`、`=`和`0`

在`ViewController`中输入如下代码:

```objc
@interface ViewController ()
    @property (weak, nonatomic) IBOutlet UITextField *firstNum;
    @property (weak, nonatomic) IBOutlet UITextField *secondNum;
    @property (weak, nonatomic) IBOutlet UILabel *countNum;
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
}

- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
}

//按钮的事件
- (IBAction)clickCalculate {
    UITextField *filed1 = self.firstNum;
    UITextField *filed2 = self.secondNum;
    
    NSString *str1 = filed1.text;
    NSString *str2 = filed2.text;
    
    if(str1.length == 0){
        [self showAlertInfo:@"提示" message:@"请填写第一个数字"];
        return;
    }
    
    if(str2.length == 0){
        [self showAlertInfo:@"提示" message:@"请填写第二个数字"];
        return;
    }
    
    NSInteger num1 = [str1 integerValue];
    NSInteger num2 = [str2 integerValue];
    NSInteger numSum = num1 + num2;
    
    NSString *count = [NSString stringWithFormat:@"%zd",numSum];
    self.countNum.text = count;
}

- (void) showAlertInfo:(NSString *)title message:(NSString *)msg{
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:msg delegate:nil cancelButtonTitle:@"关闭提示" otherButtonTitles:nil, nil];
    [alert show];
}

@end
```

将`UIButton`与方法`(IBAction)clickCalculate`拖线关联,将两个`UITextField`分别于`firstNum`和`secondNum`进行拖线关联,最后将设置text为0的`UILabel`与属性`countNum`进行关联。

**<del>`重点: UIAlertView`</del>`实际上该API已经被建议废弃，所以会有另外被代替的API方法。这里因为偷懒整上去了。`**
