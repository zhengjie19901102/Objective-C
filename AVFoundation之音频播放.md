## AVFoundation之音频播放

使用AVFoundation框架，需要导入 `AVFoundation/AVFoundation.h`头文件。

核心对象: `AVplayer`

附属对象: `AVPlayerItem`

代码:

```objc
AVPlayer *player = [[AVPlayer alloc] init];
NSURL *url = [[NSBundle mainBundle] URLForResource:@"zhao" withExtension:@"mp3"];
AVPlayerItem *apvL = [[AVPlayerItem alloc] initWithURL:url];
//替换当前播放列表中音频资源
[player replaceCurrentItemWithPlayerItem:apvL];
//播放音频
[player play];
//播放音频速率
[player rate:(float)];
//暂停播放
[player pause];
```
