## IOS-UITableView测试

```objc
#import "ViewController.h"

@interface ViewController () <UITableViewDataSource>

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
}


- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
}

//多少组
-(NSInteger)numberOfSectionsInTableView:(UITableView *)tableView{
    return 3;
}

//每组多少列
-(NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section{
    if(section == 0){
        return 4;
    }else if(section == 1){
        return 4;
    }else{
        return 1;
    }
}

//每个cell中的内容
-(UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath{
    UITableViewCell *cell = [[UITableViewCell alloc] init];
    
    if(indexPath.section == 0){
        if(indexPath.row == 0){
            //设置图片
            cell.imageView.image = [UIImage imageNamed:@"aer"];
            //设置文字
            cell.textLabel.text = @"阿尔宙斯";
            //设置右侧图标
            cell.accessoryType = UITableViewCellAccessoryDisclosureIndicator;
            //设置右侧图标为UIView --> 该优先级大于accessoryType，所以同时设置的情况下会覆盖accessoryType
            //cell.accessoryView = [[UISwitch alloc] init];
        }else if(indexPath.row == 1){
            //设置图片
            cell.imageView.image = [UIImage imageNamed:@"hongshenggu"];
            //设置文字
            cell.textLabel.text = @"红圣姑";
            //设置右侧图标
            cell.accessoryType = UITableViewCellAccessoryDisclosureIndicator;
            //设置右侧图标为UIView --> 该优先级大于accessoryType，所以同时设置的情况下会覆盖accessoryType
            //cell.accessoryView = [[UISwitch alloc] init];
        }else if(indexPath.row == 2){
            //设置图片
            cell.imageView.image = [UIImage imageNamed:@"lanshenggu"];
            //设置文字
            cell.textLabel.text = @"蓝圣姑";
            //设置右侧图标
            cell.accessoryType = UITableViewCellAccessoryDisclosureIndicator;
            //设置右侧图标为UIView --> 该优先级大于accessoryType，所以同时设置的情况下会覆盖accessoryType
            //cell.accessoryView = [[UISwitch alloc] init];
        }else{
            //设置图片
            cell.imageView.image = [UIImage imageNamed:@"huangshenggu"];
            //设置文字
            cell.textLabel.text = @"黄圣姑";
            //设置右侧图标
            cell.accessoryType = UITableViewCellAccessoryDisclosureIndicator;
            //设置右侧图标为UIView --> 该优先级大于accessoryType，所以同时设置的情况下会覆盖accessoryType
            //cell.accessoryView = [[UISwitch alloc] init];
        }
    }else if(indexPath.section == 1){
        if(indexPath.row == 0){
            //设置图片
            cell.imageView.image = [UIImage imageNamed:@"fengwang"];
            //设置文字
            cell.textLabel.text = @"凤王";
            //设置右侧图标
            cell.accessoryType = UITableViewCellAccessoryDisclosureIndicator;
            //设置右侧图标为UIView --> 该优先级大于accessoryType，所以同时设置的情况下会覆盖accessoryType
            //cell.accessoryView = [[UISwitch alloc] init];
        }
    }
    
    return cell;
}

//每组的头部标题
-(NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section{
    if(section == 0){
        return @"第四世代";
    }else if(section == 1){
        return @"第二世代";
    }else{
        return @"第三世代";
    }
}

//每组的尾部标题
-(NSString *)tableView:(UITableView *)tableView titleForFooterInSection:(NSInteger)section{
    if(section == 0){
        return @"第四世代";
    }else if(section == 1){
        return @"第二世代";
    }else{
        return @"第三世代";
    }
}
@end
```