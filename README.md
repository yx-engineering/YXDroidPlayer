## 云犀直播 YXDroidPlayer 播放控件说明文档
-  @author  FindFreeFire <1719048237@qq.com> 
-  @link 
-  @version 1.0 

云犀直播开发的Android的视频播放器 SDK，简化了开发流程，特色是支持 RTMP 和 HLS 直播流媒体播放,相关API网站 ：http://b.yunxi.tv/developer/

### 功能特性:
- [x] RTMP 直播流播放
- [x] HLS 播放
- [x] 高可定制
- [x] 音频后台播放
- [x] RTMP 直播首屏秒开支持
- [x] RTMP 直播累积延迟消除技术

### 1.基本配置

#### (1).添加权限
在 AndroidMainfest 添加网络访问权限
```xml
        <uses-permission android:name="android.permission.INTERNET" />
```
#### (2).注册应用
```java
        YXSDK.register(this, APPID, ACCESSKEY, SECRETKEY);
```

###  1.活动列表控件

#### (1).布局文件
```xml
    <com.yunxi.player.lib.YXActivityList
        android:id="@+id/yx_activitys"
        android:layout_width="match_parent"
        android:layout_height="match_parent">
    </com.yunxi.player.lib.YXActivityList>
```
#### (2).加载数据
    YXActivityList控件会根据注册信息自动加载数据
###  2.播放器控件
#### (1).初始化播放器
   
```java
      yunxiPlayer.init(this, livestreamJson, loadingDrawable);     //初始化视频播放器
```

#### (2).各个生命周期配置 
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
#### (3).直播准备,载入播放数据
```java
        YXThirdUser thirdUser = new YXThirdUser("0001-sdk", "卖报的小行家",
                        "http://www.th7.cn/d/file/p/2016/09/12/891c32cf36166bc42604ba226a7d5dba.jpg");
        //创建第三方用户对象,参数分别为 1.用户id+"sdk"  2.用户名  3. 用户头像url地址
        yunxiPlayer.steup(thirdUser, activityModel, livestreamJson);
        //相关API网站 ：http://b.yunxi.tv/developer/  获取livestreamJson
```
#### (4).播放器控制:
##### 开始直播
```java
      yunxiPlayer.startPlayer();
```  
##### 停止直播
   
```java
      yunxiPlayer.stopPlayer();
```  

##### 判断当前是否在直播中
   
```java
       yunxiPlayer.isPlaying();
```  
###  3.关于数据获取
#### (1).可以利用包内的YXApi获取活动的播放信息
```java
      YXApi.get().getLivestream(activityModel.id, System.currentTimeMillis(), new YXApiResponseHandler() {
            @Override
            public void onSuccess(YXApiResponse resp) throws JSONException {
                String livestreamJson = resp.getString(YXApi.VALUE_DATA);
                YXThirdUser thirdUser = new YXThirdUser("0001-sdk", "卖报的小行家",
                        "http://www.th7.cn/d/file/p/2016/09/12/891c32cf36166bc42604ba226a7d5dba.jpg");
                yunxiPlayer.steup(thirdUser, activityModel, livestreamJson);
                yunxiPlayer.startPlayer();
            }

            @Override
            public void onError(YXApiResponse resp) {
            }

            @Override
            public void onFailure(int statusCode, Header[] headers, Throwable throwable, JSONObject errorResponse) {
                yxErrorToast.showError(errorResponse.optString("msg"));
            }

            @Override
            public void onComplete() {
                loadingDialog.cancel();
            }
        });
```  
#### (2).可以利用包内的YXApi获取活动列表信息
```java
     YXApi.get().getActivitys(p, 20, System.currentTimeMillis() / 1000, new YXApiResponseHandler() {
            @Override
            public void onSuccess(YXApiResponse resp) throws JSONException{
                 JSONObject data = new JSONObject(resp.getString(YXApi.VALUE_DATA));
                 final JSONArray jsonArray = data.getJSONArray(ACTIVITIES);
            }

            @Override
            public void onError(YXApiResponse resp) {
            }

            @Override
            public void onFailure(int statusCode, Header[] headers, Throwable throwable, JSONObject errorResponse) {
            }

            @Override
            public void onComplete() {
            }
        });
```  
