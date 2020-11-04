# miniprogram 小程序之单页面自定义导航栏



## 写在开始

自定义导航栏一直都是一个刚需,  相信微信也是在我们抱怨声中, 下定决心开放这一功能.

全局自定义导航栏, 不多说. 心累

今天的主角是:   单页面自定义导航栏



## 弄(neng)就完了

配置方法,  我这里对比着说:



全局自定义导航栏配置:    

> 版本要求:
>
> ​    调试基础库>=1.9.0
>
> ​    微信客户端>=6.6.0
>
> 操作:
>
> ​    app.json   window 增加 "navigationStyle":"custom"，所有页面导航栏就消失了



单页面自定义导航栏配置:  

> 版本要求:   
>
> ​    调试基础库>=2.4.3
>
> ​    微信客户端版本>=7.0.0
>
>  操作:   
>
> ​    自定义的页面.json 配置 "navigationStyle":"custom",  当前页的导航栏就消失了



**请注意**

> 请注意: 微信自然是考虑到兼容问题,  如果版本不够新(为什么会有不升级微信的人呢? 值得反思), 就会展示默认的导航栏, 所以  "navigationBarTitleText": "我最帅",   还是要设置的, 在判断是低版本的时候, 也要把自定义的隐藏哦.
>
> 切记! 不要忽视低版本用户, 可能你老板就在内哦



是不是很简单?  

是不是很高兴?

是不是觉得就这么搞定了?

有木有发现页面滚动的时候, wifi 图标、时间、电量等状态栏都压在页面上了. 丑不丑?  你这样弄(neng) , 设计妹子愿意吗?

刘海屏也是风靡一时, 有木有照顾到刘海屏手机的用户勒?   不考虑? 如果你女朋友就是刘海屏呢? 不撕烂你的嘴



## 追求完美

我们都是有追求的猿类, 自然是要照顾设计妹子感受, 也好安抚刘海屏客户的情绪

> 这里是重点: 
>
> [wx.getSystemInfoSync()](https://links.jianshu.com/go?to=https%3A%2F%2Fdevelopers.weixin.qq.com%2Fminiprogram%2Fdev%2Fapi%2Fwx.getSystemInfoSync.html%3Fsearch-key%3Dwx.getSystemInfoSync)  客户获取到手机到型号、系统、**微信版本**、**基础库版本**、以及**手机状态栏高度**
>
> *微信版本、基础库版本 为了判断是否支持单页面自定义设置导航*
>
> *手机状态栏高度  为了兼容刘海屏手机*

到这里, 所有招数都已经传授完毕, 能修行到什么地步, 还要看你内功高不高了,



## 高人请转身, 菜鸟继续蹲

以下就是代码思路了, 请收起你们的搬砖.

1. 设置配置文件

2. 自定义导航栏组件

3. app.js 获取手机型号, 判断是否展示自定义菜单,  并兼容刘海屏,

4. 当前页显示隐藏自定义导航栏

5. 效果展示

   ​

1.  当前页面json 设置配置文件

![img](https://upload-images.jianshu.io/upload_images/2319334-18b51e538fee821f.png)

2. 自定义导航栏组件

wxml

![img](https://upload-images.jianshu.io/upload_images/2319334-3857c705601f89fb.png)

js

![img](https://upload-images.jianshu.io/upload_images/2319334-241854b8a996e31b.png)

3. app.js 获取手机型号, 判断是否展示自定义菜单,  并兼容刘海屏,

![img](https://upload-images.jianshu.io/upload_images/2319334-5f1391919ff4720c.png)

4. 当前页显示隐藏自定义导航栏

wxml

![img](https://upload-images.jianshu.io/upload_images/2319334-d6c43b52b98495ce.png)

js

![img](https://upload-images.jianshu.io/upload_images/2319334-3c7dd20df3afeea0.png)



5. 效果展示

​    此处有个二维码