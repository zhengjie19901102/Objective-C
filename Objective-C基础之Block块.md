##Objective-C基础之Block块

block类似定义C语言函数指针变量。

```objc
//C语言的函数指针
void (*functionPoint)(int,int);

//oc中的block块声明
void (^blockName)(int,int);
```

从以上代码得出，block声明与C语言的函数指针声明非常相似。只是C语言中的声明变量名前是`*`,而Objective-C中的变量名前为`^`。

`声明block块然后定义block。`

```objc
void (^blockName)(int,int);
blockName = ^(int a,int b){
    NSLog(@"block块:a->%i,b->%i",a,b);
};
blockName(10,12);
```

`也可以在声明的同时定义block块。`

```objc
void (^blockName2)(int,int) = ^(int a,int b){
    NSLog(@"a->%i,b->%i",a,b);
};
blockName2(10,12);
```

**`从以上代码得出，声明时在参数列表中可以不需要声明变量名。编译器在声明期只需要知道需要预留多少内存空间即可。`**

如果block没有参数，那么赋block值时^后面的()可以省略。示例如下:

```objc
//定义同时进行初始化。
void (^blockName3)(void) = ^{
    NSLog(@"block被执行。");
};
blockName3();

//先声明定义后蔬初始化。
void (^blockName4)(void);
blockName4 = ^{
    NSLog(@"block4被执行。");
};
blockName4();
```

**`Block块定义别名与函数指针方法相似`**

```objc
//函数指针的别名
typedef void (*functionName)(void);
//使用函数指针别名
functionName fun = anotherfunName;
使用函数指针定义的别名执行函数
func();

//定义blockName块别名
typedef void (^blockName)(void);
//使用别名定义block块
blockName block = ^{
    NSLog(@"block");
};
//使用别名定义的block块
block();
```
**`从以上代码看出两者极为类似。`**

**`BLOCK块注意点:`**

> block可以访问外边先定义的变量

> block中可以定义外界同名变量

> block默认无法修改外界定义的变量，因为block会拷贝一份外界定义的变量至堆内存中

> 因为是拷贝，所以在block调用之前修改外界定义的变量不会影响block内部的同名变量

> 如果外边给变量修饰上__block后，则反编译成C++后显示是指针传递，也就是说外部修改后会影响到block内部，反之亦然。

> block默认存放在栈中，进行一次copy操作后会转移到堆中

**`block主要用途在于包装一块可重用的代码块。用途很广[在UIKit等框架中用到很多]。`**

