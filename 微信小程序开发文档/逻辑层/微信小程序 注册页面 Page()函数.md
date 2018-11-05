## 微信小程序 注册页面 Page()函数

## Page
Page() 函数用来注册一个页面。接受一个 object 参数，其指定页面的初始数据、生命周期函数、事件处理函数等。

object 参数说明：

属性	类型	描述
data	Object	页面的初始数据
onLoad	Function	生命周期函数--监听页面加载
onReady	Function	生命周期函数--监听页面初次渲染完成
onShow	Function	生命周期函数--监听页面显示
onHide	Function	生命周期函数--监听页面隐藏
onUnload	Function	生命周期函数--监听页面卸载
onPullDownRefresh	Function	页面相关事件处理函数--监听用户下拉动作
onReachBottom	Function	页面上拉触底事件的处理函数
onShareAppMessage	Function	用户点击右上角转发
onPageScroll	Function	页面滚动触发事件的处理函数
其他	Any	开发者可以添加任意的函数或数据到 object 参数中，在页面的函数中用 this 可以访问


示例代码：
```
//index.js
Page({
  data: {
    text: "This is page data."
  },
  onLoad: function(options) {
    // Do some initialize when page load.
  },
  onReady: function() {
    // Do something when page ready.
  },
  onShow: function() {
    // Do something when page show.
  },
  onHide: function() {
    // Do something when page hide.
  },
  onUnload: function() {
    // Do something when page close.
  },
  onPullDownRefresh: function() {
    // Do something when pull down.
  },
  onReachBottom: function() {
    // Do something when page reach bottom.
  },
  onShareAppMessage: function () {
   // return custom share data when user share.
  },
  onPageScroll: function() {
    // Do something when page scroll
  },
  // Event handler.
  viewTap: function() {
    this.setData({
      text: 'Set some data for updating view.'
    })
  },
  customData: {
    hi: 'MINA'
  }
})
```

初始化数据
初始化数据将作为页面的第一次渲染。data 将会以 JSON 的形式由逻辑层传至渲染层，所以其数据必须是可以转成 JSON 的格式：字符串，数字，布尔值，对象，数组。

渲染层可以通过 WXML 对数据进行绑定。

示例代码：

```
<view>{{text}}</view>
<view>{{array[0].msg}}</view>
Page({
  data: {
    text: 'init data',
    array: [{msg: '1'}, {msg: '2'}]
  }
})
```

生命周期函数
onLoad: 页面加载

一个页面只会调用一次，可以在 onLoad 中获取打开当前页面所调用的 query 参数。
onShow: 页面显示

每次打开页面都会调用一次。
onReady: 页面初次渲染完成

一个页面只会调用一次，代表页面已经准备妥当，可以和视图层进行交互。
对界面的设置如wx.setNavigationBarTitle请在onReady之后设置。详见生命周期
onHide: 页面隐藏

当navigateTo或底部tab切换时调用。
onUnload: 页面卸载

当redirectTo或navigateBack的时候调用。
生命周期的调用以及页面的路由方式详见

## onLoad参数

类型	说明
Object	其他页面打开当前页面所调用的 query 参数。

## 页面相关事件处理函数
onPullDownRefresh: 下拉刷新

监听用户下拉刷新事件。
需要在config的window选项中开启enablePullDownRefresh。
当处理完数据刷新后，wx.stopPullDownRefresh可以停止当前页面的下拉刷新。
onReachBottom: 上拉触底

监听用户下拉触底事件。
onPageScroll: 页面滚动

监听用户滑动页面事件。
参数为 Object，包含以下字段：
字段	类型	说明
scrollTop	Number	页面在垂直方向已滚动的距离（单位px）
onShareAppMessage: 用户转发
只有定义了此事件处理函数，右上角菜单才会显示“转发”按钮
用户点击转发按钮的时候会调用
此事件需要 return 一个 Object，用于自定义转发内容

## 自定义转发字段

字段	说明	默认值
title	转发标题	当前小程序名称
path	转发路径	当前页面 path ，必须是以 / 开头的完整路径


## 示例代码
```
Page({
  onShareAppMessage: function () {
    return {
      title: '自定义转发标题',
      path: '/page/user?id=123'
    }
  }
})
```

## 事件处理函数

除了初始化数据和生命周期函数，Page 中还可以定义一些特殊的函数：事件处理函数。在渲染层可以在组件中加入事件绑定，当达到触发事件时，就会执行 Page 中定义的事件处理函数。

示例代码：
```
<view bindtap="viewTap"> click me </view>
Page({
  viewTap: function() {
    console.log('view tap')
  }
})
```

Page.prototype.route
route 字段可以获取到当前页面的路径。

Page.prototype.setData()
setData 函数用于将数据从逻辑层发送到视图层，同时改变对应的 this.data 的值。

setData() 参数格式
接受一个对象，以 key，value 的形式表示将 this.data 中的 key 对应的值改变成 value。

其中 key 可以非常灵活，以数据路径的形式给出，如 array[2].message，a.b.c.d，并且不需要在 this.data 中预先定义。

注意：

直接修改 this.data 而不调用 this.setData 是无法改变页面的状态的，还会造成数据不一致
单次设置的数据不能超过1024kB，请尽量避免一次设置过多的数据。
示例代码：

```
<!--index.wxml-->
<view>{{text}}</view>
<button bindtap="changeText"> Change normal data </button>
<view>{{num}}</view>
<button bindtap="changeNum"> Change normal num </button>
<view>{{array[0].text}}</view>
<button bindtap="changeItemInArray"> Change Array data </button>
<view>{{object.text}}</view>
<button bindtap="changeItemInObject"> Change Object data </button>
<view>{{newField.text}}</view>
<button bindtap="addNewField"> Add new data </button>

//index.js
Page({
  data: {
    text: 'init data',
    num: 0,
    array: [{text: 'init data'}],
    object: {
      text: 'init data'
    }
  },
  changeText: function() {
    // this.data.text = 'changed data'  // bad, it can not work
    this.setData({
      text: 'changed data'
    })
  },
  changeNum: function() {
    this.data.num = 1
    this.setData({
      num: this.data.num
    })
  },
  changeItemInArray: function() {
    // you can use this way to modify a danamic data path
    this.setData({
      'array[0].text':'changed data'
    })
  },
  changeItemInObject: function(){
    this.setData({
      'object.text': 'changed data'
    });
  },
  addNewField: function() {
    this.setData({
      'newField.text': 'new data'
    })
  }
})
```

以下内容你不需要立马完全弄明白，不过以后它会有帮助。

生命周期
下图说明了 Page 实例的生命周期。

![1](../../image/mina-lifecycle.png)
