ios13适配遇到的坑。。

1.tabbar文字设置失效 
原来：
NSDictionary *dicSlect = [NSDictionary dictionaryWithObject:XHBlueColor forKey:NSForegroundColorAttributeName];
NSDictionary *dicNormal = [NSDictionary dictionaryWithObject:[UIColor grayColor] forKey:NSForegroundColorAttributeName];

[vc.tabBarItem setTitleTextAttributes:dicSlect forState:UIControlStateSelected];
[vc.tabBarItem setTitleTextAttributes:dicNormal forState:UIControlStateNormal];

现在：
self.tabBar.tintColor = XHBlueColor;   //选中状态
self.tabBar.barTintColor = [UIColor grayColor];    //普通状态

2.控件使用默认颜色会根据系统浅色 深色模式自动切换 

3.环信的easeui里numberOfItemsInSection报错
解决前：

NSInteger numberOfBeforeSection = [_update[@"oldModel"] numberOfItemsInSection:updateItem.indexPathBeforeUpdate.section];
解决后：

 NSInteger numberOfBeforeSection = [(UICollectionView *)_update[@"oldModel"] numberOfItemsInSection:updateItem.indexPathBeforeUpdate.section];
 
参考链接：https://blog.csdn.net/bitcser/article/details/100113549

4.友盟推送 友盟统计老版本SDK会崩 需要更新

5.presentViewController进入下一界面显示改动 会留出上方一部分
vc.modalPresentationStyle = 0可解决

6.设置不兼容深色模式
info.plist文件里添加   User Interface Style   Light （上传ipa的时候被拒绝了）
目前在baseviewcontroller里用 if (@available(iOS 13.0, *)){ self.overrideUserInterfaceStyle = UIUserInterfaceStyleLight; }
