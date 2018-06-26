## IOS之UIScorllView[1]笔记

**`测试代码1`**

```objc
/**
 * 当设置contentSize属性之后，UIScrollView就可以使用滚动
 * 当contentSize的值设置的宽高设置的比UIScrollView的宽高小的时候也无法触发滚动
 */
self.uiScrollView.contentSize = CGSizeMake(self.uiScrollView.frame.size.width+100, self.uiScrollView.frame.size.height+100);
//当设置scrollEnabled为NO以后ScrollView就关闭了滚动功能，但是其仍旧能触发单机等其他事件
self.uiScrollView.scrollEnabled = NO;
//当设置scrollEnabled为NO以后ScrollView就关闭了滚动功能，并且其他的事件都无法被触发
self.uiScrollView.userInteractionEnabled = NO;
/**
 * userInteractionEnabled属性是UIView父类的属性，也就是说只要继承了
 * UIView类的类都能使用该属性。例如UIButton、UIImageVIew等等
 * 1.UIButon的[UIControlState]几种状态:
 *
    -------------  常用  -------------
        UIControlStateNormal      --> 正常状态
        UIControlStateHighlighted --> 高亮状态[按下未抬起]
        UIControlStateDisabled    --> 禁止使用状态
    ------------  不常用  ------------
        UIControlStateSelected
        UIControlStateFocused
        UIControlStateApplication
        UIControlStateReserved
	 要是UIButton状态为UIControlStateDisabled,则enabled需要设置为NO,设置UIView的userInteractionEnabled为NO则不行。
	 因为userInteractionEnabled是UIView的属性
 */
```


**`测试代码2:`**

scrollView显示可滚动图片:

```objc
//创建UIImageView对象，默认大小为图片大小
UIImage *image = [UIImage imageNamed:@"kej"];
UIImageView *imageView = [[UIImageView alloc] initWithImage:image];
//将图片添加至UIScrollView控件
[self.uiScrollView addSubview:imageView];
//设置可滚动范围为图片的大小
self.uiScrollView.contentSize = imageView.frame.size;
```

**`UIScrollView常用属性: `**

- `contentSize` 可滚动范围，接收一个CGSize结构体
- `alwaysBounceVertical` 总是显示纵向滚动条,默认是NO
- `alwaysBounceHorizontal` 总是显示横向滚动条,默认是NO
- `bounces` 是否开启弹簧效果[就是当滚动条拉到低时是否显示动态特效，默认是YES]

**`测试代码3:`**
UIScrollView的showsVerticalScrollIndicator和showsHorizontalScrollIndicator属性配合UIActivityIndicatorView,可以设置顶部或底部刷新界面: 

```objc
UIActivityIndicatorView *uiActiveView = [[UIActivityIndicatorView alloc] initWithActivityIndicatorStyle:UIActivityIndicatorViewStyleGray];
//默认是NO，设置ScrollView是否总是显示纵向或横向滚动条[bounce弹簧的意思]
self.scrollView.alwaysBounceVertical = YES;
self.scrollView.alwaysBounceHorizontal = YES;
    
uiActiveView.center = CGPointMake(100, -40);
    
self.scrollView.bounces = YES;
[uiActiveView startAnimating];
[self.scrollView addSubview:uiActiveView];
```

**`重点: 当ScrollView设置了contentSize以后，ScrollView会默认调整纵向和横向滚动条的显示大小及内部可滚动范围，所以当调用subviews方法是会对子控件自动添加滚动条子控件。所以千万不要直接通过subviews方法获取到的NSArray对象的lastObject或firstObject方法来获取想要的子控件[可能获取到的不会是想要的]。`**

