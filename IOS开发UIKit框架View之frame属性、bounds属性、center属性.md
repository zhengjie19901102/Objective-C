## IOS开发UIKit框架View之frame属性、bounds属性、center属性

属性名称      |     属性解释
------------|------------
frame			| 设置(获取)控件的坐标位置，及尺寸
center 		| 设置(获取)控件的坐标位置(控件中心点相对父控件左上角0,0坐标位置)
bounds			| 设置(获取)控件的尺寸大小(虽然也接受4个值，但是前两个坐标值固定是0，也就是相对自身控件的所在坐标)，**IOS9**之前是以自身控件左上角坐标为固定点然后向右下角放大(缩小)。**IOS9**之后变成为以自身中心点为固定点向周围放大(缩小)。

`frame属性`指定了控件在父容器的位置，及自身长宽尺寸。其位置以父容器的左上角为坐标原点(0,0)。横向为X轴坐标，纵向为Y轴坐标:

<img src="/Users/zhengjie/Documents/文档笔记/objective-C/img/img12.png" width="60%"/>

`frame属性`接收一个`CGRect`结构体。示例如下:

```objc

//View中定义的frame属性
@property(nonatomic) CGRect frame;

//CGRect实际为一个起了别名的结构体
struct CGRect {
    CGPoint origin;
    CGSize size;
};
typedef struct CG_BOXABLE CGRect CGRect;
```

OC中可以使用`CGRectMake(CGFloat x, CGFloat y, CGFloat width, CGFloat height)函数`来创建`CGRect`结构体。
框架中其函数源代码如下:

```objc
CGRectMake(CGFloat x, CGFloat y, CGFloat width, CGFloat height)
{
  CGRect rect;
  rect.origin.x = x; rect.origin.y = y;
  rect.size.width = width; rect.size.height = height;
  return rect;
}
```

**`总结: OC框架中凡是出现CG开头的结构体，都可以采用CG***Make的函数来创建该结构体。`**

在事件中不能直接修改`frame`属性中的结构体，因为直接获取等同于是一个常量，常量无法给常量赋值。所以需要告知编译器其属性中的结构体中指定的是一个变量，所以采用声明相同结构体，然后从`frame`中取出赋值给声明的结构体后进行修改再赋给`frame`回去(其实是要让编译器指定用户要的是一个变量，所以声明下告知编译器而已)。

`bounds属性`同样接收一个`CGRect`结构体，只是其中的`origin`的坐标值时固定的(0,0坐标)。因为**`IOS9`之前**与**`IOS9`之后**效果显示不一样，所以个人觉得能不用就不用。反正也很少用。😂

`center属性`结构一个`CGPoint`结构体(`CGPoint`就是`CGRect`结构体中修饰`origin`的结构体类型)。字面意思上"点"，实际上就是自身中心点相对父容器坐标原点的位置。

<img src="/Users/zhengjie/Documents/文档笔记/objective-C/img/img13.png" width="60%"/>

通过以上总结的规律，所以`CGPoint`结构体可以通过`CGPointMake(CGFloat x, CGFloat y)函数`来创建。

```objc
CGPoint center = CGPointMake(self.view.frame.size.width * 0.5, self.view.frame.size.height * 0.5);
```

**`注：结构体要修改内部数据，需要先声明(或者定义)结构体来告知编译器，该变量是结构的一个变量。`**

例如现在要修改某个控件的frame属性中结构体中的坐标:

```objc
//声明并初始化一个CGRect(通过获取控件的frame属性中的值),
//告知编译器我要修改frame中结构体某个变量的值
CGRect rect = self.label.frame;
//修改x轴坐标
rect.origin.x = 80.f;
//因为结构体是值传递，而不是地址传递。
//所以实际上当从frame中取出CGRect时是拷贝了一份结构体赋值给了rect变量。
//所以修改完毕后，要将新的结构体赋值回frame修改。
self.label.frame = rect;

```

**`注意: 结构体是值传递，而不是地址传递。可以把结构体赋值看做是拷贝了新的一份结构体交给了变量。`**