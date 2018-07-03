## IOS开发之Nib[Xib]加载的两种方式

`方式1`

```objc
NSArray *arr = [[NSBundle mainBundle] loadNibNamed:@"Car" owner:nil options:nil];
UIView *view = [arr firstObject];
view.frame = CGRectMake(0, 20, self.view.frame.size.width, 120);
[self.view addSubview:view];
```

`方式2`

```objc
UINib *nib = [UINib nibWithNibName:@"Car" bundle:nil];
UIView *view = [[nib instantiateWithOwner:nib options:nil] firstObject];
[self.view addSubview:view];
```