## IOS-UITableView性能优化实现[缓存池机制]

```objc
//获取当前的tableView
UITableView *tableVIew = self.tableView;

//从当前tableView的缓存池中获取UITableViewCell对象(标记为A)
UITableViewCell *cell = [tableVIew dequeueReusableCellWithIdentifier:@"A"];

//判断是否有cell在缓存池中
if(cell == nil){
	//如果没有则创建一个UITableViewCell对象并且标记为A.此时UITableView会自动在该Cell被移出屏幕时缓存到tableView的缓存池中。
    cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleSubtitle reuseIdentifier:@"A"];
    cell.backgroundColor = [UIColor blueColor];
    cell.backgroundView = [[UIView alloc] init];
    Wine *wine = self.wineArr[indexPath.row];
    cell.imageView.image = [UIImage imageNamed:wine.image];
    cell.textLabel.text = wine.name;
    cell.detailTextLabel.text = wine.money;
    cell.detailTextLabel.textColor = [UIColor orangeColor];
    cell.accessoryType = UITableViewCellAccessoryDisclosureIndicator;
}

```

**`从TableView缓存池中需要通过标记来获取cell，所以在创建cell的时候需要给cell带上标记，当移出屏幕时系统会检查是否带有标记，如果没有带有标记则消耗，如果带有则放入缓存池中已备使用。`**

**`重复创建、消耗会带来系统上的资源开销。所以开发时尽量减少资源开销。`**
