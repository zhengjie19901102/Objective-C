## IOS 轮播图[加定时器]

```objc
#import "ViewController.h"
@interface ViewController () <UIScrollViewDelegate>
@property (weak, nonatomic) IBOutlet UIScrollView *scrollView;
@property (weak, nonatomic) IBOutlet UIPageControl *pageControl;
@property(weak,nonatomic)NSTimer *timer;
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    int count = 3;
    CGFloat width = self.scrollView.frame.size.width;
    CGFloat height = self.scrollView.frame.size.height;
    //设置滚动尺寸，宽度大于scrollView宽度才能滚动
    self.scrollView.contentSize = CGSizeMake(width * count, height);
    for (int i = 0; i < count; i++) {
        UIImageView *imageView = [[UIImageView alloc] initWithImage:[UIImage imageNamed:[NSString stringWithFormat:@"%i.jpeg",i]]];
        imageView.frame = CGRectMake(i * width, 0, width, height);
        [self.scrollView addSubview:imageView];
    }
    //scrollView开启分页[IOS内置]
    self.scrollView.pagingEnabled = YES;
    
    //当轮播图只有一张时，最好是给页码隐藏掉
    if(count <= 1){
        //方式一:设置透明度为透明
        //self.pageControl.alpha = 0;
        //方式二:设置UIView的hidden属性
        //self.pageControl.hidden = YES;
        //方式三:使用pageControl的特有属性hidesForSinglePage
        self.pageControl.hidesForSinglePage = YES;
    }
    //---> 分页功能不需要滚动条，可以用代码，也可以在storyBoard中勾去:showsHorizontalScrollIndicator和showsVerticalScrollIndicator
    //设置分页标识的个数:---> 与轮播图数个数一致
    self.pageControl.numberOfPages = count;
    
    //分页页码可以自定义样式：通过KVC来自定义
//    [self.pageControl setValue:[[UIImageView alloc] initWithImage:[UIImage imageNamed:@"imageName"]] forKey:@"_currentImage"];
//    [self.pageControl setValue:[[UIImageView alloc] initWithImage:[UIImage imageNamed:@"imageName"]] forKey:@"_pageImage"];
    
    //开始定时器
    [self startTimer];
}

//开始定时器
-(void)startTimer{
    //target: 指定对应是那个类来定时,selector: 指定对应的那个类的方法最为定时器调用方法,userInfo: 当调用方法时定时器会将userinfo中的值传递给调用方法,repeats: 是否重复执行定时器
    self.timer = [NSTimer scheduledTimerWithTimeInterval:2.0 target:self selector:@selector(nextPage)  userInfo:nil repeats:YES];
}

-(void)stopTimer{
    //使定时器失效
    [self.timer invalidate];
    //因为timer是weak弱引用，实际这里也可以不用nil
    self.timer = nil;
}

//定时调用的方法
-(void)nextPage{
    //当前页码
    NSInteger page = self.pageControl.currentPage + 1;
    //当大于页码总数时，回退到0
    NSInteger number = self.pageControl.numberOfPages;
    if(page >= number){
        page = 0;
    }
    //设置自动偏移量:动画方式
    [self.scrollView setContentOffset:CGPointMake(page * self.scrollView.frame.size.width, 0) animated:YES];
}
//当开始拖拽的时候要停止定时器
- (void)scrollViewWillBeginDragging:(UIScrollView *)scrollView{
    [self stopTimer];
}

//当结束拖拽的时候恢复定时器
- (void)scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate{
    [self startTimer];
}


//设置结束后正在结束动作
- (void)scrollViewDidEndDecelerating:(UIScrollView *)scrollView{
    //计算下标索引
    //int index = self.scrollView.contentOffset.x / self.scrollView.frame.size.width;
    //设置当前页码
    //self.pageControl.currentPage = index;
}
//设置结束拖拽后的动作
//- (void)scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate{
//    if(decelerate == NO){
//        //计算下标索引
//        //int index = self.scrollView.contentOffset.x / self.scrollView.frame.size.width;
//        //设置当前页码
//        //self.pageControl.currentPage = index;
//    }
//}
//另一种方案
-(void)scrollViewDidScroll:(UIScrollView *)scrollView{
    //另一个方案:当图片超过一半显示需要将下标索引进一[四舍五入]
    int index = (self.scrollView.contentOffset.x / self.scrollView.frame.size.width + 0.5);
    self.pageControl.currentPage = index;
}
@end
```