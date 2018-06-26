##Objective-C预处理器指令学习笔录

`#import`是objective-C中新追加的预处理指令，其功能与`#include`指令相同。区别在于，`#import`指令在出现相同头文件导入时不会重复导入相同的头文件，而`#include`指令则需要通过`#if`、`#define`等预处理指令配合过滤重复的头文件。
在Objective-C下,`#import`指令与C语言的`#include`指令使用方式相同，都有俩种使用格式，但俩种使用格式有不同使用场景。其格式有以下两种:

```objective-C
	1. #import <header.h>
	2. #import "header.h"
```

现对这两种使用格式解释如下:

`#impor <header.h>`格式，\#import指令后需要导入的文件用`<>`括起来的代表导入的是缺省路径的二进制编译或头文件(系统或编译器内置的)。编译会根据缺省的搜索路径去搜索并导入指定的文件。其搜索文件的顺序如下:

```
编译指定存放预处理文件所在位置 → 系统级存放预处理文件所在位置
```
`#impor "header.h"`格式，\#import指令后需要导入的文件用`""`括起来的代表自定义资源文件，例如自定义的头文件、类的声明文件。编译会根据项目的相对路径去搜索对应的文件并导入到项目中。该编译器搜索的路径顺序如下:

```
自定义文件存放位置 → 编译指定存放预处理文件所在位置 → 系统级存放预处理文件所在位置
```

从以上的总结得出: 如果是系统或编译器自带(内置)的预处理文件则采用`#import <header.h>`的格式导入，而自定义项目内的头文件、资源文件等则可采用`#import "header.h"`这种格式导入。

这里对编译内置的相关头文件路径做下记录:

系统相关框架内置文件存放位置:

```
/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator.sdk/usr
```

系统环境的内置文件存放位置:

```
/usr/include
```

如果没有在对应的路径下没有系统环境的内置文件，则需要执行`xcode-select --install`命令，将系统内置文件安装到对应路径下。


