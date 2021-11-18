# ScreenShotDemo
监听截屏回调

透過 ContentProvider 來監聽 uri 變化，間接達成監聽截屏事件(前提需要檔案訪問權限)


# 截屏方案对比（截屏事件没有同一的api）

## 方案一：利用FileObserver监听某个目录中资源变化情况

* 优点：操作简单
* 缺点：
  * 不同的手机，默认截屏图片储存的文件夹可能不同
  * 不同的手机，事件回调可能有些不同
  * FileObserver只能监听文件夹中子文件和子文件夹的变化情况，不能监听子文件夹内部的资源变化
</br>

## 方案二：利用ContentObserver用来监听指定uri的所有资源变化【适配R】

* 优点：适配方便
* 缺点：去重麻烦

结合方案一方案二优缺点，且项目里已有方案是FileObserver有些机型难适配， 适配考虑 最终选择了方案二

### ContentObserver实现方案

ContentObserver用来监听指定uri的所有资源变化

添加过滤条件

时间判断，图片的生成时间在开始监听之后, 并与当前时间相隔10秒内

尺寸判断，图片的尺寸没有超过屏幕的尺寸

路径判断，图片路径符合包含特定的关键词：这一点是关键，截屏图片的保存路径通常包含“screenshot”

自测机型

* Android 11.0
* 小米 11
* vivo iQOO 5
* Android 10.0
* 华为 mate20x
* oppo Reno2
* Android 9.0
* 华为 荣耀 9
* vivo 1725
* oppo Reno
* Android 8.1
* oppo R11s
* 小米6X

————————————————

原文出处链接：https://blog.csdn.net/xuwb123xuwb/article/details/118091867
