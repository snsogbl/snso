---
layout: post
title: 使用UICollectionView实现图片轮播
--- 

最近项目中要一个图片展示组件，最开始想到是用UIScrollView组件，用UIScrollView就有几个问题：

* 展示的是网络图片，用UIScrollView图片会同时加载，效果不理想。
* 如果展示的图片很多，UIScrollView也会有内存问题

最终选择UICollectionView。用起来很方便，最终支持本地图片、网络图片。

##如何实现
####自动滚动
用一个NSTimer，执行滚动下一页操作。
要注意的是需要在scrollview代理中控制好计时器，避免手动滚动时计时器触发。
	
	//计时器暂停
	- (void)scrollViewWillBeginDragging:(UIScrollView *)scrollView
	//计时器开始
	- (void)scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate
	
####轮播

1.将数据源的个数乘以100返回给代理
<pre>
- (NSInteger)collectionView:(UICollectionView *)collectionView numberOfItemsInSection:(NSInteger)section{
    int row = 0;
    row = [array count] * 100;
    return row;
}
</pre>

2.获取数据源对应的对象
<pre>
- (UICollectionViewCell *)collectionView:(UICollectionView *)collectionView cellForItemAtIndexPath:(NSIndexPath *)indexPath{
    int itemIndex = indexPath.item % [array count];
    [array objectAtIndex:itemIndex];
    ...
}
</pre>

具体代码 github:[https://github.com/snsogbl/CustomPhotosBrowse](https://github.com/snsogbl/CustomPhotosBrowse)
