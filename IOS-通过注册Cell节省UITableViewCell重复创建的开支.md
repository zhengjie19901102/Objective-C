## IOS-通过注册Cell节省UITableViewCell重复创建的开支

在`viewDidLoad`中通过tableView注册`cell`:

```objc
[self.tableView registerClass:[UITableViewCell class] forCellReuseIdentifier:status];
```

```objc
UITableViewCell *cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:status]; 
cell.detailTextLabel.text = @"描述描述，一个劲的描述";
cell.textLabel.text = @"是标题是标题，还是标题";
return cell;
```

**`重点: 在继承的UITableViewController中已经拥有了tableView属性，此时就可以使用该tableView来注册Cell。`**