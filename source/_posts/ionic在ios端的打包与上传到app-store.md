title: ionic在ios端的打包与上传到app store
date: 2016-10-20 13:42:22
tags:
- ionic
- ios
- app store
---
搞了一段时间的ionic在ios端的打包上传，终于弄好了，期间有遇到很多坑，先记录下来，以供以后用到的人学习参考。

ionic打包成ipa并上传到app store，第一反应是怎么打包，和打包原生app有什么不同。其实没什么不同，完全可以看作是一个原生app的打包发布，网上打包原生app的教程也同样适用于ionic的打包发布。

可以参考一下内容打包发布

[ Xcode打包项目(.xcodeproj=>.ipa)](http://blog.csdn.net/haozhoupan/article/details/51181709)
[iOS开发之2016年App提交上架App Store最新流程(iPhone)](http://www.jianshu.com/p/ae482e6cb973)

下面说说这两篇文章没有提到我却遇到的坑。。TT

1.按照上面的步骤，得到的证书确是 ‘不受信任／由未知机构颁发的’ ,在打包的时候会报错，Missing iOS Distribution signing identity ...
网上说是删除过期证书，但是我删完了也没用，还是报错，看到了下面这片文章

[Missing iOS Distribution signing identity问题解决](http://blog.csdn.net/qq_26338299/article/details/50670630)

因该是AppleWWDRCA证书无效（但我这没过期。。所以具体原因不太清楚），下载一个新的，双击安装就好了。

[下载地址](https://developer.apple.com/certificationauthority/AppleWWDRCA.cer)

2. 打包时候在General下的Bundle Identifier的名字要与申请的保持一致

3. 在上传的时候，要General下的Deployment Info 下的Devices，如果只要选择iPhone，则选择iPhone，想全选选择Universal。

5. 上传说明图时，上传一下规格

4.7寸,5.5寸，ipad五种图片，对应尺寸大小：
3.5寸：横坚屏 640*960 或960*640
4寸：横坚屏 640*1036 或1036*640
4.7寸：横坚屏 750*1334 或1334*750
5.5寸：横坚屏 1242*2208 或2208*1242
ipad：横坚屏 1024*768 或768*1024

（5.5寸测试成功）

6. icon图标上传大小为1024*1024的正方形

额，目前遇到想到就这么多，望对读者有帮助。