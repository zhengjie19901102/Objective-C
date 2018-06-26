##UIKit框架-UILabel

UILable文档中解释:

```txt
A view that displays one or more lines of read-only text, often used in conjunction with controls to describe their intended purpose.
```

翻译:

```
显示一个或多个只读文本行的视图，通常与控件一起使用，以描述其预期目的。
```

常用属性

属性名称 | 属性解释   |  属性接收的数据类型
--------|----------|----------------- 
Text    | Label的文本内容 | NSString *
textColor	| Label的文本的颜色| UIColor对象
font | Label文本字体 | UIFont对象
textAlignment | Label文本对其方式 | NSTextAlignment枚举类型
numberOfLines | 文本的行数(如果设置为0，则代表自动换行) | NSInteger类型
lineBreakMode | 文本的断行模式 | NSLineBreakMode枚举类型
clipsToBounds | 是否阶段超出界限的部分| BOOL类型
alpha|设置透明度|CGFloat类型
backgroundColor | 设置背景颜色 | UIColor对象
shadowColor | 设置阴影颜色 | UIColor对象
shadowOffset | 设置阴影的偏移量 | CGSize结构体类型
frame		| 设置Label的位置及长宽 | CGRect结构体类型
bounds | 设置Label的长宽(位置固定值为0,0。无法修改) | CGRect结构体类型
center | 设置label的中心点离父容器左上角原点的距离 | CGPoint结构体类型

涉及到的几个类使用方法:

类名: `UIFont`

方法名 | 方法类型 |解释
-----|------|-------
fontWithName | 类方法 | 返回使用CSS名称匹配语义的字体。接收两个参数:(NSString *)字体名,(CGFloat)字体大小
systemFontOfSize | 类方法 | 接收一个(CGFloat)字体大小。指定字体大小，并返回创建一个UIFont对象
boldSystemFontOfSize | 类方法| 接收一个(CGFloat)字体大小，设置粗体字体大小。并创建一个UIFont对象
italicSystemFontOfSize | 类方法 | 接收一个(CGFloat)字体大小，设置斜体字体大小。并创建一个UIFont对象

**`更多功能查看API或源码头文件`**

类名: `UIColor`

```objc
+ (UIColor *)blackColor;      // 0.0 white
+ (UIColor *)darkGrayColor;   // 0.333 white 
+ (UIColor *)lightGrayColor;  // 0.667 white 
+ (UIColor *)whiteColor;      // 1.0 white 
+ (UIColor *)grayColor;       // 0.5 white 
+ (UIColor *)redColor;        // 1.0, 0.0, 0.0 RGB 
+ (UIColor *)greenColor;      // 0.0, 1.0, 0.0 RGB 
+ (UIColor *)blueColor;       // 0.0, 0.0, 1.0 RGB 
+ (UIColor *)cyanColor;       // 0.0, 1.0, 1.0 RGB 
+ (UIColor *)yellowColor;     // 1.0, 1.0, 0.0 RGB 
+ (UIColor *)magentaColor;    // 1.0, 0.0, 1.0 RGB 
+ (UIColor *)orangeColor;     // 1.0, 0.5, 0.0 RGB 
+ (UIColor *)purpleColor;     // 0.5, 0.0, 0.5 RGB 
+ (UIColor *)brownColor;      // 0.6, 0.4, 0.2 RGB 
+ (UIColor *)clearColor;      // 0.0 white, 0.0 alpha 
```
**`查看源码头文件或文档`**

