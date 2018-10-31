如何获取微信小程序用户openid？

获取微信OpenId
先获取code
再通过code获取auth token，从auth token中取出openid给前台
微信端一定不要忘记设定网页账号中的授权回调页面域名


流程图如下:

![结构展示](https://raw.githubusercontent.com/huangguangda/Wechat_small_program_Share/master/1479955923950610.png)

![图片1](/1479955923950610.png)