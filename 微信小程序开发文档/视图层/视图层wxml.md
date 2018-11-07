## 微信小程序框架视图层(View)

视图层
MINA的视图层由WXML与WXSS编写。
将逻辑层的数据反应成视图，同时将视图层的事件发送给逻辑层。
WXML(WeiXin Markup language)用于描述页面的结构。
WXSS(WeiXin Style Sheet)用于描述页面的样式。
组件(Component)是视图的基本组成单元。


WXML
WXML(WeiXin Markup Language)是框架设计的一套标签语言，结合基础组件、事件系统，可以构建出页面的结构。

用以下一些简单的例子来看看WXML具有什么能力：

数据绑定
```
<!--wxml-->
<view> {{message}} </view>
// page.js
Page({
  data: {
    message: 'Hello MINA!'
  }
})
```
列表渲染
```
<!--wxml-->
<view wx:for-items="{{array}}"> {{item}} </view>
// page.js
Page({
  data: {
    array: [1, 2, 3, 4, 5]
  }
})
```
条件渲染
```
<!--wxml-->
<view wx:if="{{view == 'WEBVIEW'}}"> WEBVIEW </view>
<view wx:elif="{{view == 'APP'}}"> APP </view>
<view wx:else="{{view == 'MINA'}}"> MINA </view>
// page.js
Page({
  data: {
    view: 'MINA'
  }
})
```
模板
```
<!--wxml-->
<template name="staffName">
  <view>
    FirstName: {{firstName}}, LastName: {{lastName}}
  </view>
</template>

<template is="staffName" data="{{...staffA}}"></template>
<template is="staffName" data="{{...staffB}}"></template>
<template is="staffName" data="{{...staffC}}"></template>
// page.js
Page({
  data: {
    staffA: {firstName: 'Hulk', lastName: 'Hu'},
    staffB: {firstName: 'Shang', lastName: 'You'},
    staffC: {firstName: 'Gideon', lastName: 'Lin'}
  }
})
```
事件
```
<view bindtap="add"> {{count}} </view>
Page({
  data: {
    count: 1
  },
  add: function(e) {
    this.setData({
      count: this.data.count + 1
    })
  }
})
```
具体的能力以及使用方式在以下章节查看：

数据绑定、列表渲染、条件渲染、模板、事件、引用