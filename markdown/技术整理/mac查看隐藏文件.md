如何让 Finder 显示隐藏文件和文件夹
第一步：打开「终端」应用程序。
第二步：输入如下命令：
defaults write com.apple.finder AppleShowAllFiles -boolean true ; killall Finder
[![](http://upload-images.jianshu.io/upload_images/66256-99c7d5f7d14c98c4.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)](http://cdn.sspai.com/attachment/thumbnail/2014/08/06/413565ee2f63088a43202e3647914c8716910_mw_800_wm_1_wmp_3.jpg)
第三步：按下「Return」键确认。
现在你将会在 Finder 窗口中看到那些隐藏的文件和文件夹了。如果你想再次隐藏原本的隐藏文件和文件夹的话，将上述命令替换成
defaults write com.apple.finder AppleShowAllFiles -boolean false ; killall Finder
即可。
[![](http://upload-images.jianshu.io/upload_images/66256-6982ea102f6ab959.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)](http://cdn.sspai.com/attachment/thumbnail/2014/08/06/60dd6003ffdc9afe21d09330dc9ec31016912_mw_800_wm_1_wmp_3.jpg)
注：该命令适用于 OS X Mavericks 和 OS X Yosemite 系统。对于还在使用 OS X Mountain Lion 或是更早版本的系统的 Mac 用户来说，命令需要稍微变化一下。
