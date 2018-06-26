## IOS开发之plist文件操作

plist是ios中类似xml文件的配置文件。它以标签的节点方式保存:NSArray和NSDictionary相关对象的数据。

**`保存NSArray数据至plist文件中`**

```objc
//创建一个数组，数组中存放的是字典
NSArray *arrDict = @[
                    @{@"name":@"李莉莉",@"age":@26,@"address":@"中国"},
                    @{@"name":@"罗伯特·爱德华",@"age":@26,@"address":@"美利坚合众国"},
                    @{@"name":@"王忠",@"age":@12,@"address":@"新加坡"}];
    
//写入至plist文件中
[arrDict writeToFile:@"/Users/zhengjie/Desktop/add.plist" atomically:YES];
```

**`保存NSDictionary数据至plist文件中`**

```objc
//创建一个字典，数组中存放的是字典
NSDictionary *dictionary = @{@"name":@"李莉莉",@"age":@26,@"address":@"中国"};
    
//写入至plist文件中
[dictionary writeToFile:@"/Users/zhengjie/Desktop/adds2.plist" atomically:YES];
```

**`通过arrayContentOfFile和dictionaryContentOfFie对象工程方法从plist文件中读取数据并创建arry和dictionary对象`**

```objc

//读取文件数据并创建array对象
NSArray *arr = [NSArray arrayWithContentsOfFile:@"/Users/zhengjie/Desktop/add.plist"];

//读取数据创建dictionary对象
NSDictionary *dictionary = [NSDictionary dictionaryContentOfFile:@"/Users/zhengjie/Desktop/adds2.plist"];
```

**`重点: Foundation框架现已将writeToFile和**ContentOfFile两个方法废弃。`**