# Wechat_small_program_Share
微信小程序分享

## Github 欢迎 Star、Fork

### 如果喜欢，那就点个赞吧！❤️ 

## 微信小程序分享

对于微信小程序的注册和普通软件的使用，不做说明(开发文档有简易教程，带你走进微信小程序开发大门)，这里只是记录下微信小程序中的代码使用(API的调用)，瞄准官方开发文档一步一步的学会使用，并掌握微信小程序。

#### 点击跳转：[小程序开发文档](https://developers.weixin.qq.com/miniprogram/dev/)

## 官方文档

- [小程序设计指南](https://developers.weixin.qq.com/miniprogram/design/index.html)
- [小程序开发教程](https://developers.weixin.qq.com/miniprogram/dev/)
- [小程序框架](https://developers.weixin.qq.com/miniprogram/dev/framework/MINA.html)
- [小程序组件](https://developers.weixin.qq.com/miniprogram/dev/component/)
- [小程序 API](https://developers.weixin.qq.com/miniprogram/dev/api/)
- [小程序开发者工具](https://developers.weixin.qq.com/miniprogram/dev/devtools/devtools.html)

## 文件

在微信小程序中有app.js,app.json,app.wxss分别是脚本文件，配置文件，样式文件。在脚本文件中我们能监听并处理小程序的生命周期函数，声明全局变量。在学习小程序之前你要掌握初步的html+css+javascript的基础知识。小程序起步到现在，越来越多的开发人员为其开发框架以及插件。

《HTML教程》 
《HTML 参考手册》 
《CSS教程》 
《CSS参考手册》 
《javascript教程》 

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

## 文件

```
// 使用 <block/> 控制标签来组织代码
<!--logs.wxml-->
<view class="container log-list">
  <block wx:for="{{logs}}" wx:for-item="log">
    <text class="log-item">{{index + 1}}. {{log}}</text>
  </block>
</view>
```

```
//logs.js
const util = require('../../utils/util.js')

Page({
  data: {
    logs: []
  },
  onLoad: function () {
    this.setData({
      logs: (wx.getStorageSync('logs') || []).map(log => {
        return util.formatTime(new Date(log))
      })
    })
  }
})

```

生命周期，每个活动都有属于它的生命周期

```
onLoad:function(){
},
onReady:function(){
},
onShow:function(){
},

onHide:function(){
},
onUnload:function(){
},
```

> App Launch->App Show->onLoad->onShow->onReady

## 跳转方法

> wx.navigateTo(OBJECT)：说明保留当前页面，跳转到应用内的某个页面，使用wx.navigateBack可以返回到原页面。

> wx.redirectTo(OBJECT)：说明关闭当前页面，跳转到应用内的某个页面。

> wx.switchTab(OBJECT)：说明跳转到 tabBar 页面，并关闭其他所有非 tabBar 页面

> wx.navigateBack(OBJECT)：说明关闭当前页面，返回上一页面或多级页面。可通过 getCurrentPages()) 获取当前的页面栈，决定需要返回几层。

> wx.reLaunch(OBJECT)：说明关闭所有页面，打开到应用内的某个页面。

## 推荐

[微信小程序开发资源精选网址导航](http://www.yimijili.com/xcxwzdh.html)
[微信小程序wepy框架开发资源汇总](https://github.com/aben1188/awesome-wepy)
[微信小程序开发资源汇总](https://github.com/justjavac/awesome-wechat-weapp)

## 组件

- [weui-wxss ★5000+](https://github.com/Tencent/weui-wxss) - 同微信原生视觉体验一致的基础样式库
- [zanui-weapp ★4000+](https://github.com/youzan/zanui-weapp) - 高颜值、好用、易扩展的微信小程序 UI 库
- [wxParse ★3000+](https://github.com/icindy/wxParse) - 微信小程序富文本解析自定义组件，支持 HTML 及 markdown 解析
- [wx-charts ★1000+](https://github.com/xiaolin3303/wx-charts) - 微信小程序图表 charts 组件
- [wux ★1000+](https://github.com/skyvow/wux) - 微信小程序自定义组件
- [wemark ★400+](https://github.com/TooBug/wemark) - 微信小程序 Markdown 渲染库
- [wxapp-img-loader ★400+](https://github.com/o2team/wxapp-img-loader) - 微信小程序图片预加载组件
- [we-cropper ★400+](https://github.com/we-plugin/we-cropper) -  微信小程序图片裁剪工具
- [WeZRender ★300+](https://github.com/guyoung/WeZRender) - 微信小程序 Canvas 开发
- [wx_calendar ★300+](https://github.com/treadpit/wx_calendar) - 小程序日历
- [wxapp ★300+](https://github.com/youzouzou/wxapp) - 微信小程序组件
- [Wa-UI ★200+](https://github.com/liujians/Wa-UI) - 针对微信小程序整合的一套 UI 库
- [wxSearch ★200+](https://github.com/icindy/wxSearch) - 微信小程序优雅的搜索框
- [wx-scrollable-tab-view ★200+](https://github.com/zhongjie-chen/wx-scrollable-tab-view) - 小程序可滑动得 tab-view
- [wetoast ★100+](https://github.com/kiinlam/wetoast) - 微信小程序 toast 增强插件
- [wx-alphabetical-listview ★100+](https://github.com/zhongjie-chen/wx-alphabetical-listview) - 微信小程序带字母滑动的 listview
- [wx-drawer ★100+](https://github.com/zhongjie-chen/wx-drawer) - 小程序模仿 QQ6.0 侧滑菜单
- [wxapp-charts ★100+](https://github.com/hawx1993/wxapp-charts) - 微信小程序图表 charts 组件
- [chartjs-wechat-mini-app ★100+](https://github.com/xiabingwu/chartjs-wechat-mini-app) - chartjs 微信小程序适配
- [wx-promise-request ★100+](https://github.com/JoeZheng2015/wx-promise-request) -  微信小程序请求队列管理库
- [we-swiper ★100+](https://github.com/we-plugin/we-swiper) - 微信小程序触摸内容滑动解决方案
- [wxDraw ★100+](https://github.com/bobiscool/wxDraw) - 微信小程序 2D 动画库
- [citySelect ★100+](https://github.com/chenjinxinlove/citySelect) ★42 - 微信小程序城市选择器
- [WeiXinProject](https://github.com/lidong1665/WeiXinProject) - 微信小程序列表上拉刷新和上拉加载
- [wepy-com-charts](https://github.com/CalvinHong/wepy-com-charts) - 微信小程序 wepy 图表控件
- [wxapp-lock](https://github.com/demi520/wxapp-lock) - 微信小程序手势解锁
- [weapp.socket.io](https://github.com/weapp-socketio/weapp.socket.io) - socket.io 风格的 websocket 类库
- [weapp-polyfill](https://github.com/leancloud/weapp-polyfill) - [w3c 标准 API polyfill
- [wxPromise](https://github.com/youngjuning/wxPromise) - 微信小程序 Promise 库
- [wxMD5](https://github.com/youngjuning/wxMD5) - 微信小程序 MD5 库
- [wxBase64](https://github.com/youngjuning/wxBase64) -  微信小程序base64 库
- [xing-weapp-component](https://github.com/ianho/xing-weapp-component) - 微信小程序基础组件扩展
- [wx-statuslayout](https://github.com/ZzjBeatYou/wx-statuslayout) -  小程序页面状态切换组件
- [minapp-api-promise](https://github.com/bigmeow/minapp-api-promise) - 微信小程序所有 API promise 化
- [minapp-slider-left](https://github.com/bigmeow/minapp-slider-left) - 微信小程序左划删除组件
- [mp_canvas_drawer](https://github.com/kuckboy1994/mp_canvas_drawer) - canvas绘制图片助手，一个json就制作分享朋友圈图片

## Demo

- [EastWorld/wechat-app-mall ★3000+](https://github.com/EastWorld/wechat-app-mall) - 微信小程序商城
- [tumobi/nideshop-mini-program ★2000+](https://github.com/tumobi/nideshop-mini-program) - 基于 Node.js + MySQL 开发的开源微信小程序商城
- [RebeccaHanjw/weapp-wechat-zhihu ★800+](https://github.com/RebeccaHanjw/weapp-wechat-zhihu) - 仿知乎
- [lypeer/wechat-weapp-gank ★600+)](https://github.com/lypeer/wechat-weapp-gank) - Gank 客户端
- [wangmingjob/weapp-weipiao ★300+](https://github.com/wangmingjob/weapp-weipiao) - 微票
- [charleyw/wechat-weapp-redux ★300+](https://github.com/charleyw/wechat-weapp-redux) - Redux 绑定库
- [jectychen/wechat-v2ex ★300+)](https://github.com/jectychen/wechat-v2ex) - V2EX
- [18380435477/WeApp ★300+](https://github.com/18380435477/WeApp) - 仿微信
- [zce/weapp-boilerplate ★300+](https://github.com/zce/weapp-boilerplate) - 微信小程序快速开发骨架
- [bayetech/wechat_mall_applet ★300+](https://github.com/bayetech/wechat_mall_applet) - 电商平台
- [lanshan-studio/wecqupt ★300+](https://github.com/lanshan-studio/wecqupt) - We 重邮
- [myronliu347/wechat-app-zhihudaily ★200+](https://github.com/myronliu347/wechat-app-zhihudaily) - 知乎日报
- [harveyqing/BearDiary ★200+](https://github.com/harveyqing/BearDiary) - 小熊の日记
- [leancloud/leantodo-weapp ★200+](https://github.com/leancloud/leantodo-weapp) - 集成 LeanCloud 实现的 Todo list
- [SuperKieran/weapp-artand ★200+](https://github.com/SuperKieran/weapp-artand) - Artand
- [dongweiming/weapp-zhihulive ★200+](https://github.com/dongweiming/weapp-zhihulive) - 知乎 Live
- [eyasliu/wechat-app-music ★200+](https://github.com/eyasliu/wechat-app-music) - 音乐播放器
- [ahonn/weapp-one ★200+](https://github.com/ahonn/weapp-one) - 仿 ONE
- [giscafer/wechat-weapp-mapdemo ★200+](https://github.com/giscafer/wechat-weapp-mapdemo) - 地图导航、marker标注 （不再维护）
- [hilongjw/weapp-gold ★100+](https://github.com/hilongjw/weapp-gold) - 掘金主页信息流
- [zce/weapp-douban ★100+](https://github.com/zce/weapp-douban) - 豆瓣电影
- [hingsir/weapp-douban-film ★100+](https://github.com/hingsir/weapp-douban-film) - 豆瓣电影
- [kunkun12/weapp](https://github.com/kunkun12/weapp) - 小程序 hello world 尝鲜
- [natee/wxapp-2048 ★100+](https://github.com/natee/wxapp-2048) - 2048 小游戏
- [SeptemberMaples/wechat-weapp-demo ★100+](https://github.com/SeptemberMaples/wechat-weapp-demo) - 购物车
- [hijiangtao/weapp-newsapp](https://github.com/hijiangtao/weapp-newsapp) - 公众号热门文章信息流
- [charleyw/wechat-weapp-redux-todos ★100+](https://github.com/charleyw/wechat-weapp-redux-todos) - 集成 Redux 实现的Todo list
- [kraaas/timer ★100+](https://github.com/kraaas/timer) - 番茄时钟
- [ericzyh/wechat-chat ★100+](https://github.com/ericzyh/wechat-chat) - 聊天室
- [BelinChung/wxapp-hiapp ★100+](https://github.com/BelinChung/wxapp-hiapp) - HiApp
- [hardog/wechat-app-flexlayout ★100+](https://github.com/hardog/wechat-app-flexlayout) - flexlayout
- [dunizb/wxapp-sCalc ★100+](https://github.com/dunizb/wxapp-sCalc) - 简易计算器
- [litt1e-p/weapp-girls ★100+](https://github.com/litt1e-p/weapp-girls) - 豆瓣美女/妹子图
- [liumulin614/BeautifulGirl](https://github.com/liumulin614/BeautifulGirl) - 美女模特
- [romoo/weapp-demo-breadtrip ★100+](https://github.com/romoo/weapp-demo-breadtrip) - 面包旅行
- [zhuweiyou/fetop100 ★100+](https://github.com/zhuweiyou/fetop100) - 前端TOP100
- [vace/wechatapp-news-reader ★100+](https://github.com/vace/wechatapp-news-reader) - 新闻阅读器
- [Symous/WechatApp-BaisiSister](https://github.com/Symous/WechatApp-BaisiSister) - 百思不得姐
- [DengKe1994/weapp-calculator](https://github.com/DengKe1994/weapp-calculator) - IOS 计算器
- [monkindey/wx-github](https://github.com/monkindey/wx-github) - GitHub 简历
- [fluency03/weapp-500px](https://github.com/fluency03/weapp-500px) - 国外摄影社区 500px
- [weapp-film](https://github.com/luuman/weapp-film) - 淘票票
- [xujinyang/CoderCalendar-WeApp](https://github.com/xujinyang/CoderCalendar-WeApp) - 程序员老黄历
- [zhengxiaowai/weapp-github](https://github.com/zhengxiaowai/weapp-github) - github
- [Seahub/PigRaising](https://github.com/SeaHub/PigRaising) - PigRaising
- [brucevanfdm/WeChatMeiZhi](https://github.com/brucevanfdm/WeChatMeiZhi) - 妹子图
- [zhijieeeeee/wechat-app-joke](https://github.com/zhijieeeeee/wechat-app-joke) - 开心一刻
- [uniquexiaobai/wechat-app-githubfeed](https://github.com/uniquexiaobai/wechat-app-githubfeed) - GitHubFeed
- [zce/weapp-todos](https://github.com/zce/weapp-todos) - TODOS 任务清单
- [yaoshanliang/weapp-ssha](https://github.com/yaoshanliang/weapp-ssha) - 企业宣传小程序
- [bruintong/wechat-webapp-douban-movie](https://github.com/bruintong/wechat-webapp-douban-movie) - 豆瓣电影
- [bruintong/wechat-webapp-douban-location](https://github.com/bruintong/wechat-webapp-douban-location) - 豆瓣同城
- [arkilis/weapp-jandan](https://github.com/arkilis/weapp-jandan) - 煎蛋
- [bodekjan/wechat-weather](https://github.com/bodekjan/wechat-weather) - 微信天气
- [jasscia/ChristmasHat](https://github.com/jasscia/ChristmasHat) - 我要圣诞帽
- [yaoshanliang/weapp-jump](https://github.com/yaoshanliang/weapp-jump) - 跳一跳
- [nanwangjkl/sliding_puzzle](https://github.com/nanwangjkl/sliding_puzzle) - 滑块拼图
- [yaoshanliang/weapp-monument-valley](https://github.com/yaoshanliang/weapp-monument-valley) - 纪念碑谷
- [kaiwu/weui-scalajs](https://github.com/kaiwu/weui-scalajs) - 使用Scala.js开发
- [tinajs/tina-hackernews](https://github.com/tinajs/tina-hackernews) - Hacker News 热点
- [mohuishou/scuplus-wechat](https://github.com/mohuishou/scuplus-wechat) - We 川大
- [hankzhuo/wx-v2ex](https://github.com/hankzhuo/wx-v2ex) - v2ex
- [Hongye567/weapp-mark](https://github.com/Hongye567/weapp-mark) - 仿 Mark 影单的微信小程序
- [w1109790800/We-Todo](https://github.com/w1109790800/We-Todo) - 基于LeanCloud的Todo-List
- [jae-jae/weapp-github-trending](https://github.com/jae-jae/weapp-github-trending) - Github今日榜单
- [steedos/mini-vip](https://github.com/steedos/mini-vip) - 华炎微站、微商城

## 从搭建一个微信小程序开始

```
视图容器：视图、滚动视图、Swiper
基础内容：图标、文本、进度条
表单组件：按钮、表单
操作反馈
导航
媒体组件：音频、图片、视频。
地图
画布
```

```
网络：上传下载、WebSocket
数据：数据缓存
位置：获取位置、查看位置
设备：网络状态、系统信息、重力感应、罗盘
界面：设置导航条、导航、动画、 绘图等等
开放接口：登录，包括签名加密，用户信息、 微信支付、模板消息
```

## 用完即走，无需安装和卸载

> 项目分为视图层和逻辑层

```
<view> {{name}} </view>
<button bindtap="changeName"> Click </button>
```

```
Page({
 data:{
  name: '我最帅'
 },
 changName: function(e){
  this.setData({
    name: '我最帅了'
  })
 }
})
```

## MINA 框架文件结构

MINA程序主体 app.js app.json app.wxss
页面 wxml wxss json js

#### app.json

> pages(必须) window tabBar networkTimeout debug

## 参考文档

window
- navigationBarBackgroundColor---背景颜色
- navigationBarTextStyle---标题颜色
- navigationBarTitleText---文字内容
- backgroundColor---背景色
- backgroundTextStyle---仅支持 dark/light
- enablePullDownRefresh---是否开启下拉刷新
- onReachBottomDistanc---页面上拉触底事件触发时距页面底部距离

tabBar
- position为top时，不会显示icon
- 只能最少2个、最多5个

```
color --- 文字颜色
selectedColor --- 中时的颜色
backgroundColor --- 背景色
borderStyle --- 边框的颜色， 仅支持 black/white
list --- 只能最少2个、最多5个
position --- ottom、top

//list
**81px * 81px**
iconPath --- 图片路径
selectedIconPath --- 选中时的图片路径
text --- 文字
pagePath --- 页面路径
```

networkTimeout
```
wx.request
wx.connectSocket
wx.uploadFile
wx.downloadFile
```

debug
```
略
```

page.json
```
//页面的.json只能设置window相关配置项
navigationBarBackgroundColor ---  背景颜色
navigationBarTextStyle --- 标题颜色
navigationBarTitleText --- 标题文字
backgroundColor --- 背景颜色
backgroundTextStyle --- 下拉 仅支持 dark/light
enablePullDownRefresh --- 是否开启下拉刷新
disableScroll --- 设置为true 整体不能上下滚动
```

## App Service

注册程序App()函数 --- object参数

## APP

```
APP({
  onLaunch: function(options) { 
    
  },
  onShow: function(options) {
      
  },
  onHide: function() {
     
  },
  onError: function(msg) {
    
  },
})
```

```
path
query
scene
shareTicket
referrerInfo
referrerInfo.appId
referrerInfo.extraData

1020 列表
1035 菜单
1036 消息卡片
1037 小程序打开小程序
1038 从另外一个小程序返回
1043 模板消息
```

onPageNotFound

```
App({
  onPageNotFound(res) {
    wx.redirectTo({
      url: 'pages/...'
    })
  }
})
```

#### getApp()

#### 注册页面Page --- object 参数

```
data 
onLoad
onReady
onShow
onHide
onUnload
onPullDownRefresh
onReachBottom
onShareAppMessage
onPageScroll
```

```
//index.js
Page({
  data: {
    text: ""
  },
  onLoad: function(options) {
    
  },
  onReady: function() {
    
  },
  onShow: function() {
    
  },
  onHide: function() {
    
  },
  onUnload: function() {
    
  },
  onPullDownRefresh: function() {
   
  },
  onReachBottom: function() {
    
  },
  onShareAppMessage: function () {
   
  },
  onPageScroll: function() {
    
  },
 
  click: function() {
    this.setData({
      text: ''
    })
  },
  
})
```

```
<view>{{array[0].msg}}</view>
Page({
 array: [{msg: '0'},{msg: '1'}]
})
```

```
onLoad --- 页面加载
onShow --- 页面显示
onReady --- 页面初次渲染
onHide --- 页面隐藏
onUnload --- 页面卸载
```

```
onPullDownRefresh: 下拉刷新
onReachBottom: 上拉触底
onPageScroll: 页面滚动
onShareAppMessage: 用户转发
```

#### 事件处理函数

```
<view bindtap = "click"> click </view>
Page({
 click: function(){
  console.log('我最帅')
 }
})
```

> Page.prototype.route 获取到当前页面的路径。

> Page.prototype.setData() 将数据从逻辑层发送到视图,同时改变对应的 this.data 的值。

> setData() 参数格式

```
以 key，value 的形式
```

```
<view>{{text}}</view>
this.setData({
      text: '我最帅'
    })
    
this.setData({
      number: this.data.number
    })
```

#### 页面路由

getCurrentPages()

```
onLoad, onSHow
```

module.exports 对外暴露接口

module.exports.sayHello = sayHello

require(path)将公共代码引入

var com = require('com.js')

INA的视图层由WXML与WXSS编写。

```
<view>{{object.key}} {{array[0]}}</view>
Page({
  data: {
    object: {
      key: 'Hello '
    },
    array: ['我最帅']
  }
})

<view wx:for-items="{{[zero, 1, 2, 3, 4]}}"> {{item}} </view>
Page({
  data: {
    zero: 0
  }
})

<template is="objectCom" data="{{for: a, bar: b}}"></template>
Page({
  data: {
    a: 1,
    b: 2
  }
})

data="{{...obj1, ...obj2, e: 5}}"
Page({
  data: {
    obj1: {
      a: 1,
      b: 2
    },
    obj2: {
      c: 3,
      d: 4
    }
  }
})

data="{{foo, bar}}"
Page({
  data: {
    foo: 'my-foo',
    bar: 'my-bar'
  }
})
```

wx:for index item
```
<view wx:for="{{array}}">
  {{index}}: {{item.message}}
</view>

Page({
  data: {
  
    array: [{
      message: 'foo',
    }, {
      message: 'bar'
    }]
    
  }
})
```

```
<view wx:for="{{array}}" wx:for-index="index" wx:for-item="item">
 {{index}}:{{item.message}}
</view>

wx:for-index
wx:for-item

九九乘法表

<view wx:for="{{[1, 2, 3, 4, 5, 6, 7, 8, 9]}}" wx:for-item="i">
  <view wx:for="{{[1, 2, 3, 4, 5, 6, 7, 8, 9]}}" wx:for-item="j">
    <view wx:if="{{i <= j}}">
      {{i}} * {{j}} = {{i * j}}
    </view>
  </view>
</view>

包含多节点的结果块:
<block wx:for="{{[1,2,3]}}">
 <view> {{index}}: </view>
 <view> {{item}} </view>
</block>
```

wx:key 指定列表中唯一的标识符。

```
wx:if wx:elif wx:else
<view wx:if="{{condition}}">  /view>
<view wx:elif="{{length > 2}}">  </view>
<view wx:else> </view>
```

<block/>不是一个组件，是一个包装元素，不会在页面中做任何渲染，只接受控制属性。

template

```
<template name="name">
 <view>
  <text> {{index}}:{{msg}} </text>
  <text> Time: {{teme}} </text>
 </view>
</template>

<template is="name" data="{{...item}}"/>
Page({
 data: {
  index:0;
  msg: 'this',
  time: '0'
 }
)}

<template name="n">
 <view> </view>
</template>

<block wx:for="{{[ ]}}">
 <template is="{{}}"/>
</block>
```

```
<view id="id" bindtap="bindtap"> </view>

Page({
 bindtap: function(e){
  console.log(e)
 }
})
```

#### 事件

冒泡事件和非冒泡事件

事件会向父节点传递 事件不会向父节点传递

#### 冒泡事件

touchstart move cancel end

tap 手指触摸后马上离开 longtap 超过350ms

#### 非冒泡事件

## key、value的形式的事件绑定

key以bind或catch开头，value是一个字符串

bind绑定不会阻止向上冒泡，catch会哦。
bindtap catchtap 

事件对象 

BaseEvent 础事件 CustomEvent 自定义事件 TouchEvent 触摸事件

#### 引用

> import 和 include

```
<template name="name">
</template>

<import src="item.wxml/>
<template is="item data="{{}}"/>

<!-- index.wxml -->
<include src="header.wxml"/>
<view> body </view>
<include src="footer.wxml"/>
```

```
<wxs module="m">
 var msg="hello";
 
 module.exports.message=msg;
</wxs>

<view> {{m.message}} </view>
```

#### WXS 模块

 .wxs 为后缀名的文件
```
module.exports 对外暴露
每个wxs模块均有 module 对象。

exports:对外共享本模块
module.exports
module.exports.msg
<wxs src="./../tools.wxs" module="tools" />
```

require 函数
```
var tools = require("./tools.wxs");
```

<wxs> 标签
module  src

#### 数据类型

number ： 数值
string ：字符串
boolean：布尔值
object：对象
function：函数
array : 数组
date：日期
regexp：正则
```
toString
toLocaleString
valueOf
toFixed
toExponential
toPrecision

toString
valueOf
charAt
charCodeAt
concat
indexOf
lastIndexOf
localeCompare
match
replace
search
slice
split
substring
toLowerCase
toLocaleLowerCase
toUpperCase
toLocaleUpperCase
trim

toString
valueOf

toString
concat
join
pop
push
reverse
shift
slice
sort
splice
unshift
indexOf
lastIndexOf
every
some
forEach
map
filter
reduce
reduceRight

parse(string):
MAX_VALUE
MIN_VALUE
NEGATIVE_INFINITY
POSITIVE_INFINITY
```

#### 样式导入

@import语句可以导入

## 视图容器

> view---hover-class,hover-start-time,hover-stay-time

```
<view class="section">
<view class="section_title"> flex:direction: row </view>
<view class="flex-wrp" style="flex-direction:row;">
<view class="flex-item bc_green"><view>
</view>
</view>

<view class="section">
<view class="section_title"> flex-direction: column</view>
<view class="flex-wrp" style="flex-direction:column;">
<view class="flex-item bc_green"></view>
</view>
</view>
```

scroll-view

> scroll-x,scroll-y upper-threshold,lower-threshold,

> scroll-top,scroll-left,scroll-inio-view,scroll-with-animation

> enable-back-to-top,bindscrolltoupper,bindscrolltolower,bindscroll

swiper

> indicator-dots indicator-color indicator-active-color autoplay

> current interval duration circular vertical bindchange

movable-view 的可移动区域

> direction inertia out-of-bounds damping friction

cover-view 覆盖在原生组件之上的文本视图

cover-image

## 项目

## 手机跨平台开发技术概述

1. 移动平台技术格局
2. 移动跨平台开发技术及其特点
3. Javascript语言及其最新发展

移动平台的先驱们
- WebOS (HP)
- Symbian (Nokia) 
- BlackBerry (RIM)
- Meego (Intel)
- Bada(Samsung)
- Linux Based (Motorola, Samsung etc)
- Windows Phone

#### 移动平台的当红小生
Android（Google)		
IOS (Apple)  			
Windows Phone (Microsoft)		

苹果重新定义的智能手机。
手机
平板电脑
电视
手表
智能汽车

#### 移动跨平台开发技术及其特点

移动互联网的痛
二分天下的终端格局
各自为政的应用商店
疲于奔命的开发者们
两种开发环境和工具
两套代码维护
两套发布系统
时间、成本、质量

#### 跨平台开发工具
CPT （cross-platform developer tools）
作用
可以使得开发者使用同样的工具在同一组基础代码上创建多个平台的应用
价值
开发大众化：降低跨平台开发的技术门槛
降低沉没成本：一套代码多平台共用

#### 跨平台开发工具功能要求

开发
- 编程语言、IDE、协作开发、软件资产管理

集成
- 本地设备API、云计算API，企业应用集成

构建
- 翻译、转换、编译、打包

发布
- 托管、应用商店提交、促销

管理
- 升级、分析、价格策略、用户服务、数据同步

## Javascript语言及其最新发展

- Javascript的成长
- 1995年5月，Brendan Eich用10天时间写完Javascript，用于Netscape浏览器的页面显示效果
- 1997年，Netscape公司提交给ECMA协会作为标准，由第39号委员会(TC39)，制定 ECMAScript EMCA-262 ，
 - - 1997年 ECMAScript 1.0  
 - - 1998年 ECMAScript 2.0
 - - 1999年 ECMAScript 3.0（现在的大部分教材都是这版本)
 - - 2000年 ECMAScript 4.0 (流产，据说是太激进被拒)
 - - 2009年 ECMAScript 5.0 ES5
 - - 2015年6月 ES6/ES2015正式通过成为国际标准，以后每年一个新版本,浏览器对ES6支持情况 http://kangax.github.io/compat-table/es6/
 - - 2016年6月 ES2016,兼容性支持情况  http://kangax.github.io/compat-table/es2016plus/
2017年6月 ES2017

## 从丑小鸭到白天鹅

Javascript是互联网时代web前端的主力军
GoogleV8引擎成为javascript发展的加速器
Node.js的优秀异步性能使javascript成为全栈开发的首选语言。
自2013年起，javascript连续多年成为github上最活跃的语言，代码贡献量最大，热度最高。
javascipt被评为TOBIE 2014年度语言
移动端浏览器竞争以及Html5标准的发布，使得js成为移动跨平台开发的新宠。

## 手机跨平台开发技术Javascript基础

1. 导论
2. 语法
3. 标准库
4. 面向对象编程
5. 语法专题

#### 概述	

- 什么是javascript语言
 - 为什么要学javascript
 - 开发环境

概述	

- 什么是javascript语言
 - 轻量级的脚本语言
  -不具备开发操作系统的能力，而是只用来编写控制其他大型应用程序的“脚本”
 -嵌入式(embeded) 浏览器/服务器（nodejs）
  - 核心语法不算很多，只能用来做一些数学和逻辑运算
  - 不提供任何与 I/O（输入/输出）相关的 API
- 语法
 - 支持对象模型
 - 基本语法构造+标准库+宿主环境API
- 宿主环境API
 - 浏览器：浏览器操作类、DOM类、Web类
 - 服务器：操作系统管理、文件系统、网络操作










