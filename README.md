# Wechat_small_program_Share
微信小程序分享

## Github 欢迎 Star、Fork

### 如果喜欢，那就点个赞吧！❤️ 

## 微信小程序分享

对于微信小程序的注册和普通软件的使用，不做说明(开发文档有简易教程，带你走进微信小程序开发大门)，这里只是记录下微信小程序中的代码使用(API的调用)，瞄准官方开发文档一步一步的学会使用，并掌握微信小程序。

#### 点击跳转：[小程序开发文档](https://developers.weixin.qq.com/miniprogram/dev/)

## 文件

在微信小程序中有app.js,app.json,app.wxss分别是脚本文件，配置文件，样式文件。在脚本文件中我们能监听并处理小程序的生命周期函数，声明全局变量。在学习小程序之前你要掌握初步的html+css+javascript的基础知识。小程序起步到现在，越来越多的开发人员为其开发框架以及插件。

```
//app.js
App({
  onLaunch: function () {
    // 展示本地存储能力 --- 从本地缓存中同步获取指定 key 对应的内容。
    var logs = wx.getStorageSync('logs') || []
    logs.unshift(Date.now())
    // wx.setStorageSync(KEY,DATA) --- 将 data 存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的内容，这是一个同步接口。
    wx.setStorageSync('logs', logs)

    // 登录
    wx.login({
      success: res => {
        // 发送 res.code 到后台换取 openId, sessionKey, unionId
      }
    })
    // 获取用户信息
    wx.getSetting({
      success: res => {
        if (res.authSetting['scope.userInfo']) {
          // 已经授权，可以直接调用 getUserInfo 获取头像昵称，不会弹框
          // wx.getUserInfo(OBJECT) --- 
          // 注意：此接口有调整，使用该接口将不再出现授权弹窗，请使用 <button open-type="getUserInfo"></button> 引导用户主动进行授权操作
          // 当用户未授权过，调用该接口将直接报错,当用户授权过，可以使用该接口获取用户信息
          wx.getUserInfo({
            success: res => {
              // 可以将 res 发送给后台解码出 unionId
              this.globalData.userInfo = res.userInfo

              // 由于 getUserInfo 是网络请求，可能会在 Page.onLoad 之后才返回
              // 所以此处加入 callback 以防止这种情况
              if (this.userInfoReadyCallback) {
                this.userInfoReadyCallback(res)
              }
            }
          })
        }
      }
    })
  },
  globalData: {
    userInfo: null
  }
})
```

```
//app.json --- 对整个小程序的全局配置。
{
  "pages":[
    "pages/index/index",
    "pages/logs/logs"
  ],
  //配置小程序的窗口
  //背景色
  //配置导航条样式
  "window":{
    "backgroundTextStyle":"light",
    "navigationBarBackgroundColor": "#fff",
    "navigationBarTitleText": "WeChat",
    "navigationBarTextStyle":"black"
  }
}
```

```
/**app.wxss --- 整个小程序的公共样式表**/
.container {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  padding: 200rpx 0;
  box-sizing: border-box;
} 
```

## 组件以及附带该有的属性

组件的使用，有

视图容器：
```
view 视图容器 该有的属性：hover-class,hover-stop-propagation,hover-start-time,hover-stay-time

scroll-view 可滚动视图区域：scroll-x,scroll-y,upper-threshold,lower-threshold,scroll-top,scroll-left,scroll-into-view,scroll-with-animation,enable-back-to-top,bindscrolltoupper,bindscrolltolower,bindscroll

swiper 滑块视图容器：indicator-dots,indicator-color,indicator-active-color,autoplay,current,current-item-id,interval,duration,circular,vertical,previous-margin,next-margin,display-multiple-items,skip-hidden-item-layout,bindchange,bindanimationfinish

movable-view 可移动的视图容器，在页面中可以拖拽滑动

cover-view 覆盖在原生组件之上的文本视图 
```

基础内容：
```
icon 图标：type size color ---- iconType：'success', 'success_no_circle', 'info', 'warn', 'waiting', 'cancel', 'download', 'search', 'clear'

text 文本： selectable space decode

rich-text 富文本：nodes

progress 进度条：percent,show-info,stroke-width,color	,activeColor,backgroundColor,active,active-mode
```

表单组件：

```
button ：按钮 size，type，plain，disabled，loading，form-type，open-type，hover-class，hover-stop-propagation，hover-start-time，hover-stay-time，lang，bindgetuserinfo，session-from，send-message-title，send-message-path，send-message-img，show-message-card，bindcontact，bindgetphonenumber，app-parameter，binderror，bindopensetting

checkbox ：checkbox-group由多个checkbox组成。 value，disabled，checked，color

form ：表单，将用户输入的<switch/> <input/> <checkbox/> <slider/> <radio/> <picker/> 提交。 report-submit，bindsubmit，bindreset

input ：输入框， value，type，password，placeholder，placeholder-style，placeholder-class，disabled，maxlength，cursor-spacing，auto-focus，focus，confirm-type，confirm-hold，cursor，selection-start，selection-end，adjust-position，bindinput，bindfocus，bindblur，bindconfirm

label ：用来改进表单组件的可用性 for

picker ：从底部弹起的滚动选择器，普通选择器，多列选择器，时间选择器，日期选择器，省市区选择器

picker-view ：嵌入页面的滚动选择器 value，indicator-style，indicator-class，mask-style，mask-class，bindchange

radio ：radio-group 内部由多个<radio/>组成。单项选择器 bindchange --- value，checked，disabled，color

slider ：滑动选择器  min，max，step，disabled，value，color，selected-color，activeColor，backgroundColor，block-size，block-color，show-value，bindchange，bindchanging

switch ：开关选择器 checked，type，bindchange，color

textarea ：多行输入框 value，placeholder，placeholder-style，placeholder-class，disabled，maxlength，auto-focus，focus，auto-height，	fixed，cursor-spacing，cursor，show-confirm-bar，selection-start，selection-end，adjust-position，bindfocus，bindblur，bindlinechange，bindinput，bindconfirm
```

导航组件：

```
navigator : 页面链接 target，url，open-type，delta，app-id，path，extra-data，version，hover-class，hover-stop-propagation，hover-start-time，hover-stay-time

functional-page-navigator : 用于跳转到插件功能页。 version，name，args，bindsuccess，bindfail
```

媒体组件：

```
audio: 建议使用能力更强的 wx.createInnerAudioContext 接口   id，src，loop，controls，poster，name，author，binderror，bindplay，bindpause，bindtimeupdate，bindended

image: 图片 src，mode，lazy-load，binderror，bindload

video: 视频 src，initial-time，duration，controls，danmu-list，danmu-btn，enable-danmu，autoplay，loop，muted，page-gesture，direction，show-progress，show-fullscreen-btn，show-play-btn，show-center-play-btn，enable-progress-gesture，objectFit，poster，bindplay，bindpause，bindended，bindtimeupdate，bindfullscreenchange，bindwaiting，binderror

camera: 系统相机 --- 需要用户授权 scope.camera mode，device-position，flash，scan-area，bindstop，binderror，bindscancode

live-player: 实时音视频播放---需要先通过类目审核---“设置”-“接口设置”中自助开通该组件权限

live-pusher: 实时音视频录制---需要用户授权 scope.camera、scope.record
```

地图组件：

```
map: 地图 longitude，latitude  scale，markers，covers --	即将移除，请使用 markers ，polyline，circles，controls，include-points，show-location，bindmarkertap，bindcallouttap，bindcontroltap，bindregionchange，bindtap，bindupdated
```

画布组件：

```
canvas: 画布 canvas-id，bindtouchstart，bindtouchmove，bindtouchend，bindtouchcancel，bindlongtap，binderror
```

开发能力组件：

```
open-data: 展示微信开放的数据 type open-gid lang

web-view: 用来承载网页的容器 src bindmessage

ad: 广告
```


