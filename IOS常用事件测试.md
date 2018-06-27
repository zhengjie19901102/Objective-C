## 常用事件测试

```objc
#import "ViewController.h"

@interface ViewController () <UITextFieldDelegate>
@property (weak, nonatomic) IBOutlet UITextField *textField;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    //设置textField的placeHolder
    self.textField.placeholder = @"placeholder";
//    UIControlEventEditingDidBegin                                   = 1 << 16,     // UITextField
//    UIControlEventEditingChanged                                    = 1 << 17,
//    UIControlEventEditingDidEnd                                     = 1 << 18,
//    UIControlEventEditingDidEndOnExit                               = 1 << 19,     // 'return key' ending
    //当编辑事件开始后
    [self.textField addTarget:self action:@selector(editingDidBegin:) forControlEvents:UIControlEventEditingDidBegin];
    //当编辑文本发生改变后
    [self.textField addTarget:self action:@selector(editingChanged) forControlEvents:UIControlEventEditingChanged];
    //当编辑事件结束后
//    [self.textField addTarget:self action:@selector(editingDidEnd) forControlEvents:UIControlEventEditingDidEnd];
    /**
     也可以通过代理方法来触发相应事件[因为UITextField即继承了UIControl也实现了delegate代理属性]
     设置TextField的代理属性对象，需要实现UITextFieldDelegate协议
     */
    self.textField.delegate = self;
}

-(void)editingDidBegin:(UITextField *)textField{
    NSLog(@"当编辑事件开始后");
}
-(void)editingChanged{
    NSLog(@"当编辑文本发生改变后");
}
//-(void)editingDidEnd{
//    NSLog(@"当编辑事件结束后");
//}

//当前ViewController触摸开始
- (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event{
    /**
     * 退出键盘
     * 方法一: 将当前的控件解除第一响应
     * 方法二: 将当前的控件结束编辑
     * 方法三: 因为控件太多，有时候不知道是哪个控件调出来的键盘，所以采用当前全部控件的父view结束编辑来退出键盘
     */
    //将当前的控件解除第一响应
    //[self.textField resignFirstResponder];
    //采用当前全部控件的父view结束编辑来退出键盘
    [self.view endEditing:YES];
    NSLog(@"执行了:%s",__func__);
}

/**
 * 实现了UITextFieldDelegate协议后，可以实现以下协议方法，来触发相应事件
 */
//当TextField结束编辑后
- (void)textFieldDidEndEditing:(UITextField *)textField{
    NSLog(@"通过delegate代理对象调用的结束编辑后方法");
}
//当TextField结束编辑
- (void)textFieldDidEndEditing:(UITextField *)textField reason:(UITextFieldDidEndEditingReason)reason{
    NSLog(@"ccc");
}
// 代理事件有多个重载。所以只能自己看头文件中或通过提示来查看有哪些方法了。
//以下为监听输入的内容[通过代理]
- (BOOL)textField:(UITextField *)textField shouldChangeCharactersInRange:(NSRange)range replacementString:(NSString *)string{
    //如果返回值为NO，则会阻止用户输入内容
    //如果返回值为YES,则允许用户输入内容
    //string参数为用户最后输入的一个字符
    NSLog(@"%@",string);
    //len输出的一直是0
    NSUInteger len = range.length;
    //貌似locationUn输出的是用的输入的字符在内容中的下标索引
    NSUInteger locationUn = range.location;
    NSLog(@"length:%li---location:%li",len,locationUn);
    return YES;
}
```