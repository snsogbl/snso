---
layout: post
title: 动态调整UITableViewCell高度的实现方法
--- 

####前提
以前实现cell的动态高度觉得好麻烦，总是要先拿到数据，再根据数据算高度，再加上组件的上下边距，如果一个cell中有多个动态高度组件更加麻烦。

贴一个简单代码

	-(CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath{
    CGFloat cellH = 0.0;
    NSString *str = [array objectAtIndex:indexPath.row];
    cellH = 0.0 + 0.0;//这里要通过文字计算出文字高度 再加上文字的上下边距
    return cellH;
    }



###现在
现在有简单办法了，再也不能通过数据源算高度

* heightForRowAtIndexPath的回调中拿到cell，返回cell高度
* cellForRowAtIndexPath 代码中设置cell高度
* 最重要一点要设置estimatedRowHeight属性 给cell设一个预算高度(非常重要)

贴一个实现代码

	-(CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath{
    CGFloat cellH = 0.0;
    UITableViewCell *cell = [self tableView:tableView cellForRowAtIndexPath:indexPath];
    cellH = cell.frame.size.height;
    return cellH;
    }



代码


<pre>
	- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
    static NSString *CellIdentifier = @"Cell";
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:CellIdentifier];
    if (cell == nil) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:CellIdentifier];
        UILabel *titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(15, 15, IPHONE_WIDTH-15*2, 20)];
        titleLabel.tag = 1000;
        [cell addSubview:titleLabel];
        UILabel *bodyLable = [[UILabel alloc] initWithFrame:CGRectMake(15, 15+30, IPHONE_WIDTH-15*2, 20)];
        bodyLable.tag = 1001;
        [bodyLable setNumberOfLines:0];
        [cell addSubview:bodyLable];
    }
    NSString *str = [array objectAtIndex:indexPath.row];
    UILabel *titleLabel = (UILabel*)[cell viewWithTag:1000];
    [titleLabel setText:@"标题"];
    
    UILabel *bodyLable = (UILabel*)[cell viewWithTag:1001];
    [bodyLable setFrame:CGRectMake(15, 15+30, IPHONE_WIDTH-15*2, 20)];
    [bodyLable setText:str];
    [bodyLable sizeToFit];
    
    CGRect cellFrame = [cell frame];
    cellFrame.origin = CGPointMake(0, 0);
    cellFrame.size.height = bodyLable.frame.size.height + bodyLable.frame.origin.y +15;
    [cell setFrame:cellFrame];
    
    return cell;
}
</pre>


``` c

#include <stdio.h>
int main(void)
{
printf("hello markdown\n");
return 0;
}

```



