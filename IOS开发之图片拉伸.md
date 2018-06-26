## IOS开发之图片拉伸

在位图像素过低且大小与所显示的不一致时，一般直接拉伸图片会导致图片的失真。此时需要对图片进行像素点的相应处理。

UIKit的`UIImage`类中提供了三个相应处理的对象方法[**`返回处理过的UIImage`**]:

> 1. stretchableImageWithLeftCapWidth:(CGFloat) leftCapWidth topCapHeight:(CGFloat) topCapHeight

> 2. resizableImageWithCapInsets:UIEdgeInsetsMake((CGFloat)topHeight, (CGFloat)leftWidth, (CGFloat)buttomHeight, (CGFloat)rightWidth) resizingMode:(UIImageResizingModeTile|UIImageResizingModeStretch)

> 3. resizableImageWithCapInsets:UIEdgeInsetsMake((CGFloat)topHeight, (CGFloat)leftWidth, (CGFloat)buttomHeight, (CGFloat)rightWidth);

stretchableImageWithLeftCapWidth方法要求传入俩个参数: 参数1为要不做拉伸的左侧宽度，参数2为不做拉伸的上册高度。
查看头文件可以看到相应的解释:

**`leftCapWidth:`**

`default is 0. if non-zero, horiz. stretchable. right cap is calculated as width - leftCapWidth - 1`

**`topCapHeight:`**

`default is 0. if non-zero, vert. stretchable. bottom cap is calculated as height - topCapWidth - 1`

通过以上确定，系统会自动通过传入的两个参数来计算出可以被拉伸的尺寸。

`resizableImageWithCapInsets`方法有俩个重载，其中一个默认模式为拉伸，还有一个则可以自己选择拉伸模式。

`resizableImageWithCapInsets`的其中一个重载方法要求传入俩个参数: 参数1要求传入经过计算的可变宽度[传入一个`UIEdgeInsetsMake`结构图],参数2要求传入一个`UIImageResizingMode`枚举[自选的拉伸模式，有两种可以选择: UIImageResizingModeTile | UIImageResizingModeStretch]

计算图示如下:

<img src="/Users/zhengjie/Documents/文档笔记/objective-C/img/widthResizable.png" alt=""/>

`总结1: 宗上得出，Width - ((leftCapWidth  *0.5 - 1) + (leftCapWidth  *0.5))就可得出可拉伸的像素宽度。`

<img src="/Users/zhengjie/Documents/文档笔记/objective-C/img/heightResizable.png" alt=""/>

`总结1: 宗上得出，Height - ((leftCapHeight  *0.5 - 1) + (leftCapHeight  *0.5))就可得出的像素高度。`

在Xcode中除了代码，也可以直接使用:

<img src="/Users/zhengjie/Documents/文档笔记/objective-C/img/HorizontalAndVerical.png" width="30%"/>