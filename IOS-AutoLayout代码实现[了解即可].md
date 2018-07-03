## IOS-AutoLayout代码实现[了解]

```objc
UIView *redView = [[UIView alloc] init];
redView.backgroundColor = [UIColor redColor];
//取消苹果添加的默认约束转换
redView.translatesAutoresizingMaskIntoConstraints = NO;
[self.view addSubview:redView];
    
//添加约束:宽度
NSLayoutConstraint *constraintWidth = [NSLayoutConstraint constraintWithItem:redView attribute:NSLayoutAttributeWidth relatedBy:NSLayoutRelationEqual toItem:self.view attribute:NSLayoutAttributeWidth multiplier:0.0 constant:300.0f];
    
//添加约束:高度
NSLayoutConstraint *constraintHeight = [NSLayoutConstraint constraintWithItem:redView attribute:NSLayoutAttributeHeight relatedBy:NSLayoutRelationEqual toItem:self.view attribute:NSLayoutAttributeHeight multiplier:0.0 constant:200.0f];
    
//添加约束:左边距
NSLayoutConstraint *marginLeft = [NSLayoutConstraint constraintWithItem:redView attribute:NSLayoutAttributeLeft relatedBy:NSLayoutRelationEqual toItem:self.view attribute:NSLayoutAttributeLeft multiplier:1 constant:10.0f];
    
//添加约束:下边距
NSLayoutConstraint *marginBottom = [NSLayoutConstraint constraintWithItem:redView attribute:NSLayoutAttributeBottom relatedBy:NSLayoutRelationEqual toItem:self.view attribute:NSLayoutAttributeBottom multiplier:1 constant:-10.0f];
    
[self.view addConstraint:constraintWidth];
[self.view addConstraint:constraintHeight];
[self.view addConstraint:marginLeft];
[self.view addConstraint:marginBottom];
```