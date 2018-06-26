## IOS开发中4种连线方式
> 第一种方式:

实现事件方法后(返回值为IBAction),然后单击左侧不放然后拖线至storyboard的指定控件上松开单击键即可:

<img src="/Users/zhengjie/Documents/文档笔记/objective-C/img/img7.png"/>

> 第二种方式:

实现方法后(返回值为IBAction),然后选中storyboard中的指定控件，按住control键不放，然后单击不放拖线至指定方法实现处松开单击键和control键:

<img src="/Users/zhengjie/Documents/文档笔记/objective-C/img/img8.png"/>

> 第三种方式:

选中storyboard中的控件后，然后鼠标右键，在弹出来的菜单中单击要连线的事件左侧的空心圆不放然后拖线至实现方法处松开:

<img src="/Users/zhengjie/Documents/文档笔记/objective-C/img/img9.png"/>

> 第四种方式:

选中storyboard中的控件后按住control键不放，直接拖线至实现方法的ViewController的代码处，出现一小块横线后松开鼠标，此时会弹出一个菜单框。然后输入需要的参数后点击Done即可:

<img src="/Users/zhengjie/Documents/文档笔记/objective-C/img/img10.png"/>

<img src="/Users/zhengjie/Documents/文档笔记/objective-C/img/img11.png"/>

参数名 | 参数解释
------| -------
Connection | 行为描述(Action \| Outlet 等, action指的是方法。Outlet指的是属性 )
Name | 方法名
Type | 指定参数的类型
Event| 事件名称(单击事件等)
Arguments | 指定参数(控件的类型、控件和事件或者没有参数)

`一个控件可以有多个事件(方法)，一个事件(方法)也可以都多个控件。一个view的Outlet(类的属性)可以有多个控件，反过来一个控件也可以有多个属性。`

`目前理解: 只有继承了UIControl的类才可以指定事件，例如: UIButton,UITextField等。`

 