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
- kaiwu/weui-scalajs](https://github.com/kaiwu/weui-scalajs) - 使用Scala.js开发
- [tinajs/tina-hackernews](https://github.com/tinajs/tina-hackernews) - Hacker News 热点
- [mohuishou/scuplus-wechat](https://github.com/mohuishou/scuplus-wechat) - We 川大
- [hankzhuo/wx-v2ex](https://github.com/hankzhuo/wx-v2ex) - v2ex
- [Hongye567/weapp-mark](https://github.com/Hongye567/weapp-mark) - 仿 Mark 影单的微信小程序
- [w1109790800/We-Todo](https://github.com/w1109790800/We-Todo) - 基于LeanCloud的Todo-List
- [jae-jae/weapp-github-trending](https://github.com/jae-jae/weapp-github-trending) - Github今日榜单
- [steedos/mini-vip](https://github.com/steedos/mini-vip) - 华炎微站、微商城


















