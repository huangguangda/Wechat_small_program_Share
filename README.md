# Wechat_small_program_Share
微信小程序分享

## Github 欢迎 Star、Fork

### 如果喜欢，那就点个赞吧！❤️ 

## 微信小程序分享

对于微信小程序的注册和普通软件的使用，不做说明(开发文档有简易教程，带你走进微信小程序开发大门)，这里只是记录下微信小程序中的代码使用(API的调用)，瞄准官方开发文档一步一步的学会使用，并掌握微信小程序。

#### 点击跳转：[小程序开发文档](https://developers.weixin.qq.com/miniprogram/dev/)

## 微信小程序官方地址

   1：[官方工具：](https://mp.weixin.qq.com/debug/wxadoc/dev/devtools/download.html?t=201714)
   
   2：[简易教程：](https://mp.weixin.qq.com/debug/wxadoc/dev/)
   
   3：[设计指南：](https://mp.weixin.qq.com/debug/wxadoc/design/index.html)
   
   4：[运营规范：](https://mp.weixin.qq.com/debug/wxadoc/product/index.html)
   
   5：[接入指南：](https://mp.weixin.qq.com/debug/wxadoc/introduction/index.html)
   
   6：[支付文档：](https://pay.weixin.qq.com/wiki/doc/api/wxa/wxa_api.php?chapter=7_3&index=1)
   
   7：[客服消息：](https://mp.weixin.qq.com/debug/wxadoc/introduction/custom.html?t=20161221) 
   
   8：[特殊行业所需资质材料：](https://mp.weixin.qq.com/debug/wxadoc/product/material.html?t=201714)
   
   9：[数据分析：](https://mp.weixin.qq.com/debug/wxadoc/analysis/index.html?t=201714)


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

- Javascript是互联网时代web前端的主力军
- GoogleV8引擎成为javascript发展的加速器
- Node.js的优秀异步性能使javascript成为全栈开发的首选语言。
- 自2013年起，javascript连续多年成为github上最活跃的语言，代码贡献量最大，热度最高。
- javascipt被评为TOBIE 2014年度语言
- 移动端浏览器竞争以及Html5标准的发布，使得js成为移动跨平台开发的新宠。

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

## 语法

基本语法
数据类型
数值
字符串
对象
数组
函数
运算符
数据类型转换
错误处理机制
编程风格

#### 基本语法

语句
变量
标识符
注释
区块
条件语句
循环语句

```
var a = 1+3;
;;;
1+3;
'abc';
```

#### 变量

1. 变量名区分大小写
2. 如果只是声明变量而没有赋值，则该变量的值是undefined。undefined是一个 JavaScript 关键字，表示“无定义”。
3. JavaScript 是一种动态类型语言，也就是说，变量的类型没有限制，变量可以随时更改类型。
4. 变量提升
5. JavaScript 引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行地运行。这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提升（hoisting）

```
var a,b;
var a=1;
a='hello';
```

#### 标识符（英数字）

- 大小写敏感

- 第一个字符，可以是任意 Unicode 字母（包括英文字母和其他语言的字母），以及美元符号（$）和下划线（_）。

- 第二个字符及后面的字符，除了 Unicode 字母、美元符号和下划线，还可以用数字0-9。

- 保留字

JavaScript有一些保留字，不能用作标识符：

```
arguments、break、case、catch、class、const、continue、debugger、default、delete、do、else、enum、eval、export、extends、false、finally、for、function、if、implements、import、in、instanceof、interface、let、new、null、package、private、protected、public、return、static、super、switch、this、throw、true、try、typeof、var、void、while、with、yield。
```

> 注释 单行注释，用//起头 多行注释，放在/*和*/之间。

> 区块 JavaScript 使用大括号，将多个相关的语句组合在一起，称为“区块”（block）。 对于var命令来说，JavaScript 的区块不构成单独的作用域（scope）。

- 基本语法
- 条件语句

```
If else else if
Switch case
```

三元表达式  ?  :

循环语句
- While

循环语句
- do while
- 不管条件是否为真，do...while循环至少运行一次，这是这种结构最大的特点。
- while语句后面的分号注意不要省略。

for

- 初始化表达式（initialize）：确定循环变量的初始值，只在循环开始时执行一次。
- 条件表达式（test）：每轮循环开始时，都要执行这个条件表达式，只有值为真，才继续进行循环。
- 递增表达式（increment）：每轮循环的最后一个操作，通常用来递增循环变量。 

for语句的三个部分（initialize、test、increment），可以省略任何一个，也可以全部省略。

for in：用来循环带有字符串key的对象

for of：ES6里引入的新循环方法。能遍历多种类型数据，包括括数组、Set 和 Map 结构、某些类似数组的对象（比如arguments对象、DOM NodeList 对象）、 Generator 对象以及字符串。

数组内置的foreach方法

```
array=[];
array.forEach({
});
```

#### Break 和 continue

break语句和continue语句都具有跳转作用，可以让代码不按既有的顺序执行。

break语句用于跳出代码块或循环。

continue语句用于立即终止本轮循环，返回循环结构的头部，开始下一轮循环。

#### 数据类型

概述
- typeof运算符
- null和undefined
- 布尔值

#### 七种数据类型

1. 数值（number）：整数和小数
2. 字符串（string）：文本
3. 布尔值（boolean）：即true（真）和false（假）
4. undefined：没有定义
5. null：表示空值
6. 对象（object）：各种值组成的集合。
7. Symbol：表示独一无二的值。

#### 原始数据类型

- 数值，字符串和布尔值
- undefined和null，一般将它们看成两个特殊值。

#### 对象的三种子类型

- 狭义的对象(object)
- 数组(array)
- 函数(function)

#### typeof运算符

typeof运算符:返回一个值的数据类型。

instanceof运算符:用来判断某个构造函数的prototype属性是否存在于另外一个要检测对象的原型链上。 

Object.prototype.toString方法：判断某个对象值属于哪种内置类型。

#### 数值

概述
数值的表示法
数值的进制
特殊数值
与数值相关的全局方法

#### 数值

概述

#### 整数和浮点数

JavaScript 内部，所有数字都是以64位浮点数形式储存，即使整数也是如此。所以，1与1.0是相同的，是同一个数。

#### 数值精度

国际标准 IEEE 754，JavaScript 浮点数的64个二进制位，从最左边开始，是这样组成的。

第1位：符号位，0表示正数，1表示负数

第2位到第12位（共11位）：

指数部分第13位到第64位（共52位）：小数部分（即有效数字）

#### 数值范围

JavaScript 能够表示的数值范围为21024到2-1023（开区间），超出这个范围的数无法表示。

数值的表示法

字面量

35
1.03
科学记数法

数值的进制

十进制：没有前导0的数值。

八进制：有前缀0o或0O的数值，或者有前导0、且只用到0-7的八个阿拉伯数字的数值。

十六进制：有前缀0x或0X的数值。

二进制：有前缀0b或0B的数值

####

特殊数值

#### 正零和负零

JavaScript 内部实际上存在2个0：一个是+0，一个是-0，区别就是64位浮点数表示法的符号位不同。它们是等价的。

唯一有区别的场合是，+0或-0当作分母，返回的值是不相等的。

除以正零得到+Infinity，除以负零得到-Infinity，这两者是不相等的

#### 特殊数值

## NaN

表示“非数字”（Not a Number），主要出现在将字符串解析成数字出错的场合。

0除以0也会得到NaN。

NaN不是独立的数据类型，而是一个特殊数值，它的数据类型依然属于Number，使用typeof运算符可以看得很清楚。

NaN不等于任何值，包括它本身。

NaN在布尔运算时被当作false。

NaN与任何数（包括它自己）的运算，得到的都是NaN。

## Infinity

Infinity表示“无穷”，用来表示两种场景。

一种是一个正的数值太大Infinity，或一个负的数值太小 -Infinity，无法表示。

> 由于数值正向溢出（overflow）、负向溢出（underflow）和被0除，JavaScript 都不报错，而是返回Infinity

所以单纯的数学运算几乎没有可能抛出错误。

Infinity大于一切数值（除了NaN），-Infinity小于一切数值（除了NaN）。

> Infinity与NaN比较，总是返回false。

Infinity与undefined运算 返回的都是NaN

## 与数值相关的全局方法

parseInt():将字符串转为整数。

parseFloat():将一个字符串转为浮点数。

isNaN():判断一个值是否为NaN。

isFinite():某个值是否为正常的数值

## parseInt()

如果字符串头部有空格，空格会被自动去除。

如果parseInt的参数不是字符串，则会先转为字符串再转换。

字符串转为整数的时候，是一个个字符依次转换，如果遇到不能转为数字的字符，就不再进行下去，返回已经转好的部分。

如果字符串的第一个字符不能转化为数字（后面跟着数字的正负号除外），返回NaN。

如果字符串以0x或0X开头，parseInt会将其按照十六进制数解析。

如果字符串以0开头，将其按照10进制解析。

对于那些会自动转为科学计数法的数字，parseInt会将科学计数法的表示方法视为字符串，因此导致一些奇怪的结果。

parseInt方法还可以接受第二个参数（2到36之间），表示被解析的值的进制，返回该值对应的十进制数。

## 字符串

概述

字符串就是零个或多个排在一起的字符，放在单引号或双引号之中。

单引号字符串的内部，可以使用双引号。双引号字符串的内部，可以使用单引号。

如果要在单引号字符串的内部，使用单引号，就必须在内部的单引号前面加上反斜杠，用来转义。双引号字符串内部使用双引号。

如果长字符串必须分成多行，可以在每一行的尾部使用反斜杠。

如果长字符串必须分成多行，可以在每一行的尾部使用反斜杠。

```
转义符
\0 ：null（\u0000）
\b ：后退键（\u0008）
\f ：换页符（\u000C）
\n ：换行符（\u000A）
\r ：回车键（\u000D）
\t ：制表符（\u0009）
\v ：垂直制表符（\u000B）
\‘ ：单引号（\u0027）
\“ ：双引号（\u0022）
\\ ：反斜杠（\u005C）
```

## 对象
- 概述	
- 对象就是一组“键值对”（key-value）的集合，是一种无序的复合数据集合。

1. 上面代码中，大括号就定义了一个对象，它被赋值给变量obj，所以变量obj就指向一个对象。
2. 该对象内部包含两个键值对（又称为两个“成员”），第一个键值对是foo: ‘Hello’，其中foo是“键名”（成员的名称），字符串Hello是“键值”（成员的值）。
3. 键名与键值之间用冒号分隔。
4. 第二个键值对是bar: ‘World’，bar是键名，World是键值。
5. 两个键值对之间用逗号分隔。

## 对象的引用

如果不同的变量名指向同一个对象，那么它们都是这个对象的引用，也就是说指向同一个内存地址。修改其中一个变量，会影响到其他所有变量。

## 表达式还是语句

如果行首是大括号，一律解释为语句（即代码块）。如果要解释为表达式（即对象），必须在大括号前加上圆括号。

这种差异在eval语句（作用是对字符串求值）中反映得最明显

#### 属性的操作

读取属性：有两种方法，一种是使用点运算符，还有一种是使用方括号运算符。

如果使用方括号运算符，键名必须放在引号里面，否则会被当作变量处理。

## 属性的操作

- 属性的赋值
JavaScript 允许属性的“后绑定”，也就是说，你可以在任意时刻新增属性，没必要在定义对象的时候，就定义好属性。
- 查看所有属性
查看一个对象本身的所有属性，可以使用Object.keys方法。
- 删除属性：delete 命令

#### 属性的操作

- In 运算符：用于检查对象是否包含某个属性（注意，检查的是键名，不是键值），如果包含就返回true，否则返回false。

- for…in 循环:遍历一个对象的全部属性。
 1. 它遍历的是对象所有可遍历（enumerable）的属性，会跳过不可遍历的属性。
 2. 它不仅遍历对象自身的属性，还遍历继承的属性。

## With语句

with语句的作用是操作同一个对象的多个属性时，提供一些书写的方便。

## 数组

#### 定义

1. 数组（array）是按次序排列的一组值。每个值的位置都有编号（从0开始），整个数组用方括号表示。
2. 任何类型的数据，都可以放入数组。

数组的本质

本质上，数组属于一种特殊的对象。typeof运算符会返回数组的类型是object。

> length属性：返回数组成员的数量，只要是数组，就一定有length属性。该属性是一个动态的值，等于键名中的最大整数加上1。
> in 运算符：检查某个键名是否存在的运算符in，适用于对象，也适用于数组。

- For in循环和数组的遍历
1. for...in循环不仅可以遍历对象，也可以遍历数组，毕竟数组只是一种特殊对象。
2. for...in不仅会遍历数组所有的数字键，还会遍历非数字键。
- 数组的空位
1. 当数组的某个位置是空元素，即两个逗号之间没有任何值，我们称该数组存在空位（hole）
2. 数组的空位不影响length属性。
3. 数组的空位是可以读取的，返回undefined。

## 函数

概述

函数的属性和方法

函数的作用域

参数

函数的其他知识点

eval命令

#### 函数的作用域

函数外部声明的变量就是全局变量（global variable），它可以在函数内部读取。

在函数内部定义的变量，外部无法读取，称为“局部变量”（local variable）。

#### 函数本身的作用域

函数执行时所在的作用域，是定义时的作用域，而不是调用时所在的作用域。

很容易犯错的一点是，如果函数A调用函数B，却没考虑到函数B不会引用函数A的内部变量。

上面代码将函数x作为参数，传入函数y。但是，函数x是在函数y体外声明的，作用域绑定外层，因此找不到函数y的内部变量a，导致报错。

## 闭包

Javascript的“链式作用域” 结构（chain scope），子对象会一级一级地向上寻找所有父对象的变量。所以，父对象的所有变量，对子对象都是可见的，反之则不成立。

Javascript在函数外部无法访问函数内部声明的变量，只有函数内部的子函数才能读取内部变量，因此可以把闭包简单理解成“定义在一个函数内部的函数”。

闭包可以“记住”诞生的环境，在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。

闭包的最大用处有两个，一个是可以读取函数内部的变量，另一个就是让这些变量始终保持在内存中，即闭包可以使得它诞生环境一直存在。

闭包的内存消耗很大，不能滥用。

## 数据类型转换
Boolean()
除了以下五个值的转换结果为false，其他的值全部为true。
```
undefined
null
-0或+0
NaN
''（空字符串）
```

## 错误处理机制

Error实例对象

原生错误类型

自定义错误

throw语句

try catch结构

finally代码块

#### Error对象属性

message：错误提示信息

name：错误名称（非标准属性）

stack：错误的堆栈（非标准属性）		

## 标准库

Array对象

Number对象

String对象

Math对象

Date对象

RegExp对象

JSON对象

console对象

Object对象

属性描述对象

包装对象

#### Array对象

构造函数

静态方法

实例方法

Array对象

- 静态方法
Array.isArray方法返回一个布尔值，表示参数是否为数组。它可以弥补typeof运算符的不足。

Array对象

实例方法

```
valueOf(),toString()
push(),pop()
shift(),unshift()
join()
concat()
reverse()
slice()
splice()
sort()
map()
forEach()
filter()
some(),every()
reduce(),reduceRight()
indexOf(),lastIndexOf()
```

- 实例方法

valueOf()：valueOf方法是一个所有对象都拥有的方法，表示对该对象求值。

不同对象的valueOf方法不尽一致，数组的valueOf方法返回数组本身。

toString方法也是对象的通用方法，数组的toString方法返回数组的字符串形式。

- 实例方法

push()：push方法用于在数组的末端添加一个或多个元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组。

pop方法用于删除数组的最后一个元素，并返回该元素。注意，该方法会改变原数组。

shift()：用于删除数组的第一个元素，并返回该元素。注意，该方法会改变原数组。

unshift():用于在数组的第一个位置添加元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组。

join():以指定参数作为分隔符，将所有数组成员连接为一个字符串返回。如果不提供参数，默认用逗号分隔。

如果数组成员是undefined或null或空位，会被转成空字符串。

concat():用于多个数组的合并。它将新数组的成员，添加到原数组成员的后部，然后返回一个新数组，原数组不变。

reverse()：用于颠倒排列数组元素，返回改变后的数组。注意，该方法将改变原数组。

slice():用于提取目标数组的一部分，返回一个新数组，原数组不变。

splice():用于删除原数组的一部分成员，并可以在删除的位置添加新的数组成员，返回值是被删除的元素。注意，该方法会改变原数组。

sort():对数组成员进行排序，默认是按照字典顺序排序。排序后，原数组将被改变。

sort方法不是按照大小排序，而是按照字典顺序。也就是说，数值会被先转成字符串，再按照字典顺序进行比较。

map()：将数组的所有成员依次传入参数函数，然后把每一次的执行结果组成一个新数组返回。

map方法课接受一个函数作为参数。该函数调用时，map方法向它传入三个参数：当前成员、当前位置和数组本身。

map方法还可以接受第二个参数，用来绑定回调函数内部的this变量。

如果数组有空位，map方法的回调函数在这个位置不会执行，会跳过数组的空位。

#### Number对象

实例方法

1. toString()：将一个数值转为字符串形式。
2. toString方法可以接受一个参数，表示输出的进制。
3. toString方法只能将十进制的数，转为其他进制的字符串。如果要将其他进制的数，转回十进制，需要使用parseInt方法。

Number对象

自定义方法
> Number.prototype对象上面可以自定义方法，被Number的实例继承。

...

//

## 面向对象编程

面向对象编程概述

This关键字

Prototype对象

Object对象与继承

面向对象编程的模式

面向对象编程概述

对象是什么

构造函数

New命令

Object.create()创建实例对象

#### 面向对象编程概述

#### 对象是什么

面向对象编程（Object Oriented Programming，缩写为 OOP）是目前主流的编程范式。

它将真实世界各种复杂的关系，抽象为一个个对象，然后由对象之间的分工与合作，完成对真实世界的模拟。

每一个对象都是功能中心，具有明确分工，可以完成接受信息、处理数据、发出信息等任务。

对象可以复用，通过继承机制还可以定制。

因此，面向对象编程具有灵活、代码可复用、高度模块化等特点，容易维护和开发，比起由一系列函数或指令组成的传统的过程式编程（procedural programming），更适合多人合作的大型软件项目。

#### 对象是什么
- 对象是单个实物的抽象。

一本书、一辆汽车、一个人都可以是对象，一个数据库、一张网页、一个与远程服务器的连接也可以是对象。当实物被抽象成对象，实物之间的关系就变成了对象之间的关系，从而就可以模拟现实情况，针对对象进行编程。

- 对象是一个容器，封装了属性（property）和方法（method）。

属性是对象的状态，方法是对象的行为（完成某种任务）。

比如，我们可以把动物抽象为animal对象，使用“属性”记录具体是那一种动物，使用“方法”表示动物的某种行为（奔跑、捕猎、休息等等）

## OOP的一些概念

类：定义对象的特征。它是对象的属性和方法的模板定义。对象（或称实例）：类的一个实例。

属性：对象的特征，比如颜色、尺寸等。

方法：对象的行为，比如行走、说话等。

构造函数：对象初始化的瞬间被调用的方法。

继承：子类可以继承父类的特征。例如，猫继承了动物的一般特性。

封装：一种把数据和相关的方法绑定在一起使用的方法。

抽象：结合复杂的继承、方法、属性的对象能够模拟现实的模型。

多态：不同的类可以定义相同的方法或属性。

## This关键字

含义

使用场合

使用注意点

绑定this的方法

#### This关键字

含义

this就是属性或方法“当前”所在的对象。

使用场合

全局环境

全局环境使用this，它指的就是顶层对象window。	

#### Prototype对象

构造函数的缺点

Prototype属性的作用

原型链

constructor属性

instanceOf运算符

## 微信小程序起步

1.微信小程序介绍
2.微信小程序注册
3.编程基础知识
4.小程序架构搭建-从HelloWorld开始
5.图片组件和单击事件-以和弦查询为例

微信小程序的历史

如何访问小程序

小程序与HTML5、APP的比较

小程序与微信公众号的比较

小程序适合哪些应用

小程序开发需要的资质和能力

小程序的注册方法

小程序的开发工具

小程序的上架流程

ES5基础

WXML基础

WXSS基础

Mustache基础

WXS

WXML基础

WXML(WeiXin Markup Language)

WXML(WeiXin Markup Language)是小程序框架设计的一套标签语言，结合小程序的基础组件、事件系统，可以构建出页面的结构。

WXML基础

WXML组件

视图容器

基础内容

表单组件

导航

媒体组件

地图

画布

#### WXML基础
WXML组件
## 视图容器
```
view
scroll-view
swiper
movable-view
cover-view
```
## 基础内容
```
icon
text
rich-text
progress
```

## 表单组件
```
button
checkbox
form
input
label
picker
picker-view
Radio
slider
switch
textarea
```
## 导航
```
navigator
```

## 媒体组件
```
audio
image
video
camera
live-player
live-pusher
```
## 地图
```
map
```
## 画布
```
canvas
```

WXSS基础

WXSS与CSS的异同

WXSS语法

WXSS选择器

WXSS常用属性

## WXSS与CSS的异同

目前支持CSS2，部分支持CSS3

- 扩展了尺寸单位
- 小程序中建议使用rpx作为尺寸单位，所有屏幕，无论大小，宽度均为750rpx，是以iphone6为基准的，

#### 样式导入

使用@import可以导入外联样式表，使用相对路径

存在全局样式和局部样式

app.wxss是全局样式，页面的xxx.wxss是局部样式

## WXSS选择器

类选择器

id选择器

元素选择器

伪元素选择器

## 常用属性

背景属性

边框属性

字体属性

外边距属性

内边距属性

显示属性

颜色属性

Mustache基础

{{表达式}}:表达式求值，转义成html显式

{{{}}}:原样输出不转义html代码

## WXS基础
WXS(WeiXin Script)微信脚本语言
貌似ES6的moulde
可直接使用<wxs>嵌入WXML中

或单独使用.wxs文件，然后在WXML中引入

```
<wxs module="foo">
var h_msg="h";
module.exports={ msg: h_msg,}
</wxs>
<view> {{foo.msg}} </view>

<wxs src="../../l.wxs" module="l"/>
```

####

## 微信小程序目录结构
#### 主体部分
```
app.js  小程序逻辑  必填
app.json  小程序公共设置  必填
app.wxss  小程序公共样式表  非必填
project.config.json 项目配置文件 自动生成 详情
```
#### 页面部分
```
.js  页面逻辑 必填
.wxml   页面结构  必填
.wxss    页面样式表 非必填 
.json    页面配置  非必填
.wxs 微信的javascript模块 非必填
```
描述页面的这四个文件必须具有相同的路径与文件名

pages	设置页面路径

window	设置默认页面的窗口表现

tabBar	设置底部tab表现

networkTimeout设置网络超时时间

debug 设置是否开启debug模式

## Demo
