## UIKit框架之UIView笔记
UIView是UIKit框架中一个非常重要的类，在文档中有如下描述:

`Views are the fundamental building blocks of your app's user interface, and the UIView class defines the behaviors that are common to all views.`

查看多个控件的继承树中可以得出:

大多数控件都继承自`UIView`父类，`UIview`类定义了所有视图中常见的行为属性,例如:背景颜色。源代码部分如下:

```objc
//...
@property(nonatomic)                 BOOL              clipsToBounds;              // When YES, content and subviews are clipped to the bounds of the view. Default is NO.
@property(nullable, nonatomic,copy)            UIColor          *backgroundColor UI_APPEARANCE_SELECTOR; // default is nil. Can be useful with the appearance proxy on custom UIView subclasses.
@property(nonatomic)                 CGFloat           alpha;                      // animatable. default is 1.0
@property(nonatomic,getter=isOpaque) BOOL              opaque;                     // default is YES. opaque views must fill their entire bounds or the results are undefined. the active CGContext in drawRect: will not have been cleared and may have non-zeroed pixels
@property(nonatomic)                 BOOL              clearsContextBeforeDrawing; // default is YES. ignored for opaque views. for non-opaque views causes the active CGContext in drawRect: to be pre-filled with transparent pixels
@property(nonatomic,getter=isHidden) BOOL              hidden;                     // default is NO. doesn't check superviews
@property(nonatomic)                 UIViewContentMode contentMode;                // default is UIViewContentModeScaleToFill
@property(nonatomic)                 CGRect            contentStretch NS_DEPRECATED_IOS(3_0,6_0) __TVOS_PROHIBITED; // animatable. default is unit rectangle {{0,0} {1,1}}. Now deprecated: please use -[UIImage resizableImageWithCapInsets:] to achieve the same effect.

@property(nullable, nonatomic,strong)          UIView           *maskView NS_AVAILABLE_IOS(8_0);

/*
 -tintColor always returns a color. The color returned is the first non-default value in the receiver's superview chain (starting with itself).
 If no non-default value is found, a system-defined color is returned.
 If this view's -tintAdjustmentMode returns Dimmed, then the color that is returned for -tintColor will automatically be dimmed.
 If your view subclass uses tintColor in its rendering, override -tintColorDidChange in order to refresh the rendering if the color changes.
 */
@property(null_resettable, nonatomic, strong) UIColor *tintColor NS_AVAILABLE_IOS(7_0);

/*
 -tintAdjustmentMode always returns either UIViewTintAdjustmentModeNormal or UIViewTintAdjustmentModeDimmed. The value returned is the first non-default value in the receiver's superview chain (starting with itself).
 If no non-default value is found, UIViewTintAdjustmentModeNormal is returned.
 When tintAdjustmentMode has a value of UIViewTintAdjustmentModeDimmed for a view, the color it returns from tintColor will be modified to give a dimmed appearance.
 When the tintAdjustmentMode of a view changes (either the view's value changing or by one of its superview's values changing), -tintColorDidChange will be called to allow the view to refresh its rendering.
 */
@property(nonatomic) UIViewTintAdjustmentMode tintAdjustmentMode NS_AVAILABLE_IOS(7_0);
//...
```
在UIView中定义大多数控件共有的属性，例如颜色、背景、透明度。

**`在查看源代码时可以发现UIButton、UISwitch等部分控件并未直接继承UIView，而是直接继承了UIControl。但是UIControl类继承了UIView类。可以得出在页面中可见的控件都是UIView的直接或间接子类。`**

查看文档:

`Views can be nested inside other views to create view hierarchies, which offer a convenient way to organize related content. Nesting a view creates a parent-child relationship between the child view being nested (known as the subview) and the parent (known as the superview). A parent view may contain any number of subviews but each subview has only one superview. `

`UIView`可以嵌套使用，一个`UIView`对象能有一个父类`UIView`，但是能有多个子`UIView`对象。

**`一个UIViewController对象只能有一个UIView直接子对象。UIViewController对象是不可见的，而UIView对象时可见的。`**

在storyboard中有些UIView是没法再嵌套其他的UIView，但是实际上按定义是可以。所以需要通过代码来实现。`通常storyboard中能完成的，通过代码也可以实现。而代码做的storyboard就不一定能做到了。`

**`UIView中常用的几个属性`**:

UIView属性 | 解释
------ | -------
subviews | 获取所有View子类对象，返回值时一个NSArray对象
superview | 获取其父类容器(按一个view只有一个父类原则，所有命名中也就没有s后缀复数的后缀了)
tag | 获取当前view对象tag值(给view对象取一个tag标签值，通过该值可以获取到对应控件)

**`UIView中常用的几个方法`**

UIView常用方法 | 解释
------|------
addSubview:(nonnull UIView *) | 将当前View对象添加到指定父容器,接收一个已存在的UIView父对象
(void)removeFromSuperview | 将当前View对象从容器中移除

**`注:`**`强调:没有一个ViewController只有一个view直接子类，当ViewController加载器根view时候在调用的viewDidLoad方法时无法在该方法中移除此view对象。因为系统在调用viewDidLoad时还未给view添加到UIWindow控件中，当调用了viewDidAppear方法后此时view被添加到了UIWindow中，因为view对象有了一个父对象，所以此时可以调用removeFromSuperview方法将从视图中移除。`

强调: `UIWindow`也继承了`UIView`类，这证明了只有`UIView`的实例才能互相嵌套且被可视。

