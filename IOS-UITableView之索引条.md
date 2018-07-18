## IOS-UITableView之索引条

设置UITableView的索引条

```objc
/*
 索引条内容
 */
-(NSArray<NSString *> *) sectionIndexTitlesForTableView:(UITableView *)tableView{
    //返回右侧索引条的索引
    return @[@"A",@"B",@"C",@"D",@"...."];
}

/*
 是否显示头部状态栏:YES隐藏，NO不隐藏
 */
- (BOOL)prefersStatusBarHidden{
    return YES;
}
```

要显示并设置索引条，需要重写UITableView的`sectionIndexTitlesForTableView`方法。

想隐藏上方状态栏(电池图标的那一栏)需要重写`prefersStatusBarHidden`方法。

要设置UITableView的索引条背景和文字颜色，则可以在UIViewController初始化调用`viewDidLoad`后设置。

```objc
//设置索引条的文字颜色
self.tableView.sectionIndexColor = [UIColor orangeColor];
//设置索引条的背景颜色
self.tableView.sectionIndexBackgroundColor = [UIColor redColor];
```
