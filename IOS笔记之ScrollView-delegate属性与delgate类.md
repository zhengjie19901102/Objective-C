## IOS笔记之ScrollView-delegate属性与delegate类
```objc
#import "ViewController.h"

@interface ViewController () <UIScrollViewDelegate>

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    //创建ScrollView
    UIScrollView *scrollView = [[UIScrollView alloc] init];
    scrollView.frame = CGRectMake(100, 100, 200, 300);
    scrollView.backgroundColor = [UIColor redColor];
    [self.view addSubview:scrollView];
    //创建ImageView
    UIImageView *imageView = [[UIImageView alloc] initWithImage:[UIImage imageNamed:@"x.jpg"]];
    scrollView.contentSize = imageView.frame.size;
    
    //将ImageView添加到ScrollView中
    [scrollView addSubview:imageView];
    
    //设置scrollView的代理对象
    scrollView.delegate = self;
    
    
}
//将被拖拽
- (void)scrollViewWillBeginDragging:(UIScrollView *)scrollView{
    NSLog(@"scrollView将要开始被拖拽");
}
//将要开始减速移动[此时已经放开鼠标，且此时移动由于惯性还未停止。
//注意:并不是说停止前一定会减速滑动，所以有可能此代理方法不一定被执行]
- (void)scrollViewWillBeginDecelerating:(UIScrollView *)scrollView{
    NSLog(@"将要开始减速移动");
}
//将要结束减速时被调用
- (void)scrollViewDidEndDecelerating:(UIScrollView *)scrollView{
    NSLog(@"将要结束减速时被调用");
}
//将要结束拖拽
- (void)scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate{
    NSLog(@"将要结束拖拽");
    if(decelerate == NO){
        NSLog(@"拖拽结束");
    }
}
//屏幕已经滚动
- (void)scrollViewDidScroll:(UIScrollView *)scrollView{
    NSLog(@"屏幕已经滚动");
}

@end
```