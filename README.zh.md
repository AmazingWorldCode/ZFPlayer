<p align="center">
<img src="http://7xqbzq.com1.z0.glb.clouddn.com/log.png" alt="ZFPlayer" title="ZFPlayer" width="557"/>
</p>

<p align="center">
<a href="https://travis-ci.org/renzifeng/ZFPlayer"><img src="https://travis-ci.org/renzifeng/ZFPlayer.svg?branch=master"></a>
<a href="https://img.shields.io/cocoapods/v/ZFPlayer.svg"><img src="https://img.shields.io/cocoapods/v/ZFPlayer.svg"></a>
<a href="https://img.shields.io/cocoapods/v/ZFPlayer.svg"><img src="https://img.shields.io/github/license/renzifeng/ZFPlayer.svg?style=flat"></a>
<a href="http://cocoadocs.org/docsets/ZFPlayer"><img src="https://img.shields.io/cocoapods/p/ZFPlayer.svg?style=flat"></a>
<a href="http://weibo.com/zifeng1300"><img src="https://img.shields.io/badge/weibo-@%E4%BB%BB%E5%AD%90%E4%B8%B0-yellow.svg?style=flat"></a>
</p>

## 特性
* 支持横、竖屏切换，在全屏播放模式下还可以锁定屏幕方向
* 支持本地视频、网络视频播放
* 支持在TableviewCell播放视频
* 左侧1/2位置上下滑动调节屏幕亮度（模拟器调不了亮度，请在真机调试）
* 右侧1/2位置上下滑动调节音量（模拟器调不了音量，请在真机调试）
* 左右滑动调节播放进度
* 全屏状态下拖动slider控制进度，显示视频的预览图
* 断点下载功能
* 切换视频分辨率

## 要求

- iOS 8+
- Xcode 7.0+

## 统计

哪些APP使用ZFPlayer，并上架AppStore，请告诉我，帮助我统计。

## 组件

- 断点下载: [ZFDownload](https://github.com/renzifeng/ZFDownload)
- 布局: Masonry


## 安装

### CocoaPods    

```ruby
pod 'ZFPlayer'
```

Then, run the following command:

```bash
$ pod install
```

## 使用 （支持IB和代码）
##### 设置状态栏颜色
请在info.plist中增加"View controller-based status bar appearance"字段，并改为NO

##### IB用法
直接拖UIView到IB上，宽高比为约束为16：9(优先级改为750，比1000低就行)，代码部分只需要实现

```objc
self.playerView.videoURL = self.videoURL;
// 返回按钮事件
__weak typeof(self) weakSelf = self;
self.playerView.goBackBlock = ^{
	[weakSelf.navigationController popViewControllerAnimated:YES];
};

```

##### 代码实现（Masonry）用法

```objc
self.playerView = [[ZFPlayerView alloc] init];
[self.view addSubview:self.playerView];
[self.playerView mas_makeConstraints:^(MASConstraintMaker *make) {
 	make.top.equalTo(self.view).offset(20);
 	make.left.right.equalTo(self.view);
	// 注意此处，宽高比16：9优先级比1000低就行，在因为iPhone 4S宽高比不是16：9
	make.height.equalTo(self.playerView.mas_width).multipliedBy(9.0f/16.0f).with.priority(750);
}];
self.playerView.videoURL = self.videoURL;
// 返回按钮事件
__weak typeof(self) weakSelf = self;
self.playerView.goBackBlock = ^{
	[weakSelf.navigationController popViewControllerAnimated:YES];
};
```

##### 设置视频的填充模式（可选设置）
```objc
 //（可选设置）可以设置视频的填充模式，内部设置默认（ZFPlayerLayerGravityResizeAspect：等比例填充，直到一个维度到达区域边界）
 self.playerView.playerLayerGravity = ZFPlayerLayerGravityResizeAspect;
```

##### 是否有断点下载功能（可选设置）
```objc
 // 默认是关闭断点下载功能，如需要此功能设置这里
 self.playerView.hasDownload = YES;
```

##### 从xx秒开始播放视频（可选设置）
 ```objc
 // 如果想从xx秒开始播放视频
 self.playerView.seekTime = 15;
 ```
 
##### 是否自动播放，默认不自动播放（可选设置）
```objc
// 是否自动播放，默认不自动播放
[self.playerView autoPlayTheVideo];
```

##### 设置播放前的占位图（需要在设置视频URL之前设置）
```objc
// 这里传图片的名称
self.playerView.placeholderImageName = @"...";
```

### 图片效果演示

![图片效果演示](https://github.com/renzifeng/ZFPlayer/raw/master/screen.gif)

![声音调节演示](https://github.com/renzifeng/ZFPlayer/raw/master/volume.png)

![亮度调节演示](https://github.com/renzifeng/ZFPlayer/raw/master/brightness.png)

![进度调节预览图](https://github.com/renzifeng/ZFPlayer/raw/master/progress.png)

### 参考资料：

- [https://segmentfault.com/a/1190000004054258](https://segmentfault.com/a/1190000004054258)
- [http://sky-weihao.github.io/2015/10/06/Video-streaming-and-caching-in-iOS/](http://sky-weihao.github.io/2015/10/06/Video-streaming-and-caching-in-iOS/)
- [https://developer.apple.com/library/prerelease/ios/documentation/AudioVideo/Conceptual/AVFoundationPG/Articles/02_Playback.html#//apple_ref/doc/uid/TP40010188-CH3-SW8](https://developer.apple.com/library/prerelease/ios/documentation/AudioVideo/Conceptual/AVFoundationPG/Articles/02_Playback.html#//apple_ref/doc/uid/TP40010188-CH3-SW8)

---
### swift版Player：
请移步 [BMPlayer](https://github.com/BrikerMan/BMPlayer)，感谢 BMPlayer 作者的开源。

### swift版知乎日报：
本人最近编写的 [知乎日报Swift](https://github.com/renzifeng/ZFZhiHuDaily)。

---

# 联系我
- 微博: [@任子丰](https://weibo.com/zifeng1300)
- 邮箱: zifeng1300@gmail.com
- QQ群：213376937

# License

ZFPlayer is available under the MIT license. See the LICENSE file for more info.

