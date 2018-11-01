## 微信小程序框架逻辑层(App Service)

## 逻辑层(App Service)
小程序开发框架的逻辑层是由JavaScript编写。

逻辑层将数据进行处理后发送给视图层，同时接受视图层的事件反馈。在 JavaScript 的基础上，我们做了一些修改，以方便地开发小程序。

增加 App 和 Page 方法，进行程序和页面的注册。
提供丰富的 API，如扫一扫，支付等微信特有能力。
每个页面有独立的作用域，并提供模块化能力。
由于框架并非运行在浏览器中，所以 JavaScript 在 web 中一些能力都无法使用，如 document，window 等。
开发者写的所有代码最终将会打包成一份 JavaScript，并在小程序启动的时候运行，直到小程序销毁。类似 ServiceWorker，所以逻辑层也称之为 App Service。
