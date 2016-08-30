## 云犀直播 YXDroidPlayer 播放控件说明文档
-  @author  FindFreeFire <1719048237@qq.com> 
-  @link 
-  @version 1.0 

云犀直播开发的Android的视频播放器 SDK，简化了开发流程，特色是支持 RTMP 和 HLS 直播流媒体播放,相关API网站 ：http://b.yunxi.tv/developer/

### 1.功能特性:
- [x] RTMP 直播流播放
- [x] HLS 播放
- [x] 高可定制
- [x] 音频后台播放
- [x] RTMP 直播首屏秒开支持
- [x] RTMP 直播累积延迟消除技术

### 2.快速配置:

#### 添加权限
在 AndroidMainfest 添加网络访问权限
```xml
<uses-permission android:name="android.permission.INTERNET" />
```

#### 配置工程
将 yunxi_player.aar 文件拷贝到项目目录下的libs文件下

#### 布局文件
```xml
 <com.yunxi.player.lib.YXPlayer
                android:id="@+id/yunxi_player"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_gravity="center"
                android:orientation="vertical"></com.yunxi.player.lib.YXPlayer>
```
#### 注册SDK
 
```java
       YXSDK.register(APPID);    //注册信息 填入APPID
```
    
#### 初始化播放器
   
```java
      yunxiPlayer.init(this, livestreamJson, loadingDrawable);     //初始化视频播放器
```
    相关API网站 ：http://b.yunxi.tv/developer/  获取livestream
#### 各个生命周期配置 
```java
    @Override
    protected void onResume() {
        super.onResume();
        yunxiPlayer.resumePlay();
    }

    @Override
    protected void onPause() {
        super.onPause();
        yunxiPlayer.pausePlayer();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        yunxiPlayer.destoryPlayer;
    } 
    
```
### 3.控制方法:
#### 开始直播
   
```java
      yunxiPlayer.startPlayer();
```  
#### 停止直播
   
```java
      yunxiPlayer.stopPlayer();
```  

#### 判断当前是否在直播中
   
```java
       yunxiPlayer.isPlaying();
```  
  
