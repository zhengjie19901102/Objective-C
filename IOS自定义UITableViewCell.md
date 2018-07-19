## IOS自定义UITableViewCell

UITableViewController

```objc

#import "ZJUITableViewController.h"
#import "ZJTableViewCell.h"
@interface ZJUITableViewController () <UITableViewDataSource>

@end

@implementation ZJUITableViewController
NSString *ID = @"ID";
- (void)viewDidLoad {
    [super viewDidLoad];
    
    //注册Cell
    [self.tableView registerClass:[ZJTableViewCell class] forCellReuseIdentifier:ID];
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
    return 15;
}

-(UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath{
    UITableViewCell *cell = [[ZJTableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:ID];
    return cell;
}

@end
```

自定义Cell

```objc
#import "ZJTableViewCell.h"

@interface ZJTableViewCell()

//图片
@property(nonatomic,weak)UIImageView *iconImageView;
//标题
@property(nonatomic,weak)UILabel *titleLable;

@end

@implementation ZJTableViewCell

- (void)awakeFromNib {
    [super awakeFromNib];
}

- (void)setSelected:(BOOL)selected animated:(BOOL)animated {
    [super setSelected:selected animated:animated];
}

- (instancetype)initWithStyle:(UITableViewCellStyle)style reuseIdentifier:(NSString *)reuseIdentifier{
    if(self = [super initWithStyle:style reuseIdentifier:reuseIdentifier]){
        NSLog(@"%p",self);
        
        UIImageView *iconImageView = [[UIImageView alloc] init];
        [self.contentView addSubview:iconImageView];
        self.iconImageView = iconImageView;
        
        UILabel *titleLable = [[UILabel alloc] init];
        [self.contentView addSubview:titleLable];
        self.titleLable = titleLable;
        
    }
    return self;
}


@end
```