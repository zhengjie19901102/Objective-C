## IOS开发之减变动画[简单]

```objc
#import "ViewController.h"

@interface ViewController ()
@property (weak, nonatomic) IBOutlet UIView *object;
@property (weak, nonatomic) IBOutlet UIView *grayView;
@end

@implementation ViewController
- (void)viewDidLoad {
    [super viewDidLoad];
}
//宽度动画
- (IBAction)widthAnimation{
    /**
     方式一
     */
    //动画开始beginAnimations
    /*[UIView beginAnimations:nil context:nil];
    CGRect frame = self.object.frame;
    [UIView setAnimationDelay:1.0f];
    frame.size.width -=100;
    self.object.frame = frame;
    //结束块动画
    [UIView commitAnimations];*/
    
    /**
     方式二
     */
    /*[UIView animateWithDuration:1.0f animations:^{
        CGRect frame = self.object.frame;
        frame.size.width -=100;
        self.object.frame = frame;
    }];*/
    
    /**
     方式三
     */
    /*
    [UIView animateWithDuration:1.0f animations:^{
        CGRect frame = self.object.frame;
        frame.size.width -=100;
        self.object.frame = frame;
    } completion:^(BOOL finished) {
        //UIView的块动画可以嵌套
        [UIView animateWithDuration:5.0 animations:^{
            CGRect frame = self.object.frame;
            frame.size.width +=100;
            self.object.frame = frame;
            self.object.backgroundColor = [UIColor blackColor];
        }];
    }];*/
    
    /**
     方式四
     */
    //因为块中会拷贝,所以需要先取出后使用
    CGFloat cf = self.object.frame.size.width;
    [UIView animateWithDuration:1.0f delay:1.0f options:UIViewAnimationOptionCurveEaseOut animations:^{
        CGRect frame = self.object.frame;
        frame.size.width -=cf;
        self.object.frame = frame;
    } completion:^(BOOL finished) {
        [UIView animateWithDuration:1.0f animations:^{
            CGRect frame = self.object.frame;
            frame.size.width +=cf;
            self.object.frame = frame;
            self.object.backgroundColor = [UIColor grayColor];
        }];
    }];
}
//移动动画
- (IBAction)moveAnimation{
    /**
     移动一
     */
    __block CGRect frameOut = self.object.frame;
    [UIView animateWithDuration:1.0f delay:1.0f options:UIViewAnimationOptionCurveEaseOut animations:^{
        CGRect frame = frameOut;
        frame.origin.y -= 100;
        self.object.frame = frame;
        frameOut = self.object.frame;
        self.object.backgroundColor = [UIColor greenColor];
    } completion:^(BOOL finished) {
        [UIView animateWithDuration:1.0f delay:0.0 options:UIViewAnimationOptionCurveEaseOut animations:^{
            CGRect frame = frameOut;
            frame.origin.y += 100;
            self.object.frame = frame;
            self.object.backgroundColor = [UIColor redColor];
        } completion:nil];
    }];
}
//缩放动画[比例]
- (IBAction)scaleAnmiation{
}
@end
```