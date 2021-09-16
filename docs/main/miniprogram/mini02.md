# onShareAppMessage 从分享朋友到分享朋友圈 onShareTimeline, 踩坑之旅

#### <a href="https://developers.weixin.qq.com/community/develop/article/doc/00082e45b549e84b38ba39fa151013">原文链接</a>


> 艳阳高照 和风细雨的日子里, 你是否也为分享朋友圈如何传参而焦虑烦躁? 端起你的枸杞菊花茶, 边喝边看



我们厂也是混微信生态的, 大厂有个风吹草动的, 我们就要立马操练起来!

前端时间分享朋友圈刚发了个beta版, 我们总部的产品大佬, 立马致电远在西部的开发部门, 干! 立马! 明天上线!!! (GNMA!G, 灵魂相同的开发们才能看懂)

还能说点啥呢?

**以上是瞎扯淡, 以下面是干活:**

为你提供方便:

**接口文档**: <https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/share-timeline.html>

**页面问答**: <https://developers.weixin.qq.com/miniprogram/dev/reference/api/Page.html#onShareTimeline>

**限制文档**: <https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/share-timeline.html#%E5%8D%95%E9%A1%B5%E6%A8%A1%E5%BC%8F%E4%B8%8B%E7%9A%84%E9%99%90%E5%88%B6>

文档一定要看, 一遍不行, 再来一遍!

**第一步: 实现分享朋友圈**

前置条件:

![img](https://img-crs.vchangyi.com//goods16309804851620.png)

直接上代码:
![img](https://img-crs.vchangyi.com//goods16309804851721.png)

找一步安卓手机, 扫码立显; 做为一个前端小菜, 我脚的走到这步, 应该木有一丁点儿问题! 如果你实现不出来, 那就回归到田野般的生活中找找赶脚

**第二步: 踩坑**

每次出来个新功能, 实现的道路上总是坑坑洼洼, 我就想问一问, 坐在腾讯大楼喝着菊花枸杞的小伙伴, 程序员何苦为难程序员? (文档写的好一点能si吗?)

大家一直关注的如何传参问题:

传参数方式是酱紫的:

![img](https://img-crs.vchangyi.com//goods16309804851752.png)

代码是酱紫的:

![img](https://img-crs.vchangyi.com//goods16309804851803.png)

接收参数: onLoad(option) , 直接就可以拿到参数对象, 点一点就就出来, 亲测可用.

**第二步: 场景值**

众所周知, 分享的页面, 在朋友圈打开是“单页面模式”, 那就收到以下限制:

![img](https://img-crs.vchangyi.com//goods16309804851934.png)

需要开发且记且珍惜. 可以根据场景值来判断页面来源

![img](https://img-crs.vchangyi.com//goods16309804852015.png)

**未完待续, 有任何问题都可以找留言(包括如何找对象)**

