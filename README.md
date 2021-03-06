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

## Features
* Support for horizontal and vertical screen switch, in full screen playback mode can also lock the screen direction
* Support local video, network video playback
* Support in TableviewCell playing video
* The left 1/2 position on the sliding screen brightness adjustment (simulator can't adjust brightness, please in the real machine debugging)
* The right 1/2 position on the sliding screen volume adjustment (simulator can't adjust the volume, please in the real machine debugging)
* Left and right sliding adjustment play schedule
* Full screen mode to drag the slider control progress, display video preview
* Breakpoint Download 
* Toggle video resolution

## Requirements

- iOS 8+
- Xcode 7+

## Statistics

What APP using ZFPlayer, and on AppStore, please tell me, help me to statistics.

## Component

- Breakpoint Download: [ZFDownload](https://github.com/renzifeng/ZFDownload)
- Layout: Masonry

## Language
[中文说明](https://github.com/renzifeng/ZFPlayer/blob/master/README.zh.md)

## Installation

### CocoaPods    

```ruby
pod 'ZFPlayer'
```

Then, run the following command:

```bash
$ pod install
```

## Usage （Support IB and code）
##### Set status bar color
Please add the "View controller-based status bar appearance" field in info.plist and change it to NO

##### IB usage
Direct drag IB to UIView, the aspect ratio for the 16:9 constraint (priority to 750, lower than the 1000 line), the code section only needs to achieve

```objc
self.playerView.videoURL = self.videoURL;
// Back button event
__weak typeof(self) weakSelf = self;
self.playerView.goBackBlock = ^{
	[weakSelf.navigationController popViewControllerAnimated:YES];
};

```

##### Code implementation (Masonry) usage

```objc
self.playerView = [[ZFPlayerView alloc] init];
[self.view addSubview:self.playerView];
[self.playerView mas_makeConstraints:^(MASConstraintMaker *make) {
 	make.top.equalTo(self.view).offset(20);
 	make.left.right.equalTo(self.view);
	// Note here, the aspect ratio 16:9 priority is lower than 1000 on the line, because the 4S iPhone aspect ratio is not 16:9
    make.height.equalTo(self.playerView.mas_width).multipliedBy(9.0f/16.0f).with.priority(750);
}];
self.playerView.videoURL = self.videoURL;
// Back button event
__weak typeof(self) weakSelf = self;
self.playerView.goBackBlock = ^{
	[weakSelf.navigationController popViewControllerAnimated:YES];
};
```

##### Set the fill mode for the video (optional)

```objc
 // (optional settings) you can set the fill mode of the video, the default settings (ZFPlayerLayerGravityResizeAspect: wait for a proportional fill, until a dimension reaches the area boundary).
 self.playerView.playerLayerGravity = ZFPlayerLayerGravityResizeAspect;
```
##### Is there a breakpoint download function (optional)
```objc
 // Default is to close the breakpoint download function, such as the need for this feature set here
 self.playerView.hasDownload = YES;
```

##### Play video from XX seconds (optional)

 ```objc
 // Play video from XX seconds
 self.playerView.seekTime = 15;
 ```

##### Automatically play the video，not automatically play by default(optional)
```objc
// Automatically play the video
[self.playerView autoPlayTheVideo];
```

##### Set the video placeholderImage (need to set the video URL before)
```objc
// Here is the name of the picture
self.playerView.placeholderImageName = @"...";
```

### Picture effect demonstration

![Picture effect](https://github.com/renzifeng/ZFPlayer/raw/master/screen.gif)

![Sound adjustment demonstration](https://github.com/renzifeng/ZFPlayer/raw/master/volume.png)

![Brightness adjustment demonstration](https://github.com/renzifeng/ZFPlayer/raw/master/brightness.png)

![Progress adjustment demonstration](https://github.com/renzifeng/ZFPlayer/raw/master/progress.png)


### reference material：

- [https://segmentfault.com/a/1190000004054258](https://segmentfault.com/a/1190000004054258)
- [http://sky-weihao.github.io/2015/10/06/Video-streaming-and-caching-in-iOS/](http://sky-weihao.github.io/2015/10/06/Video-streaming-and-caching-in-iOS/)
- [https://developer.apple.com/library/prerelease/ios/documentation/AudioVideo/Conceptual/AVFoundationPG/Articles/02_Playback.html#//apple_ref/doc/uid/TP40010188-CH3-SW8](https://developer.apple.com/library/prerelease/ios/documentation/AudioVideo/Conceptual/AVFoundationPG/Articles/02_Playback.html#//apple_ref/doc/uid/TP40010188-CH3-SW8)

---
### swift project Player:
See the [BMPlayer](https://github.com/BrikerMan/BMPlayer) please, thanks the BMPlayer author's open source.

### swift project ZFZhiHuDaily:
I recently written [ZFZhiHuDaily](https://github.com/renzifeng/ZFZhiHuDaily).

---

# Contact me
- Weibo: [@任子丰](https://weibo.com/zifeng1300)
- Email:  zifeng1300@gmail.com
- QQ Group: 213376937

# License

ZFPlayer is available under the MIT license. See the LICENSE file for more info.

