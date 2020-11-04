# wx.requestSubscribeMessage 小程序模版消息升级为订阅消息



> 在这个寒冷的冬日里, 你是否也因小程序模版消息升级为订阅消息而苦逼? 端起你的枸杞菊花茶, 边喝边看



还要从那不久前的炎炎夏日说起, 一位苦逼的前端小妹, 为了加模版消息,熬了好几个加班夜, 动了几十个页面, 修改了几百个按钮, 终于把模版消息都全面埋雷, 不留任何死角.

也就过了才 1 2 3 4 5个月吧, 订阅消息一出. 我们的前端小妹, 那脸色、那眼神、我至今找不到一个合适的词语来形容(主要是笔者词穷)

下面还是主要来说说订阅消息吧, 不然对不起读者.



升级第一步:
**注意订阅消息是有最低版本库要求的** (**这个主要是需要产品和客户同步, 不是所有人都能订阅哦**)

> 注意：iOS客户端7.0.6版本、Android客户端7.0.7版本之后的一次性订阅/长期订阅才支持多个模板消息，iOS客户端7.0.5版本、Android客户端7.0.6版本之前的一次订阅只支持一个模板消息



升级第二步:
**干就完了**

> 官方 api 地址: <https://developers.weixin.qq.com/miniprogram/dev/api/open-api/subscribe-message/wx.requestSubscribeMessage.html>



![](https://mmbiz.qpic.cn/mmbiz_png/ScjMzsiaicOvba2Luv90zKicvhDudjyafLZsXInY3EcyHf83niasNlgK5UfmvhEFIPYQtLicQaxDnXQuyfb8fiaFdhaw/0?wx_fmt=png)

**撸起袖子就是干**

小手一抖, 代码全有
![img](https://mmbiz.qpic.cn/mmbiz_png/ScjMzsiaicOvba2Luv90zKicvhDudjyafLZnuHbRVicXAfvHyXPumicSBhzPr76VKAOeE24V6GxK6x0hF38s1yE2uDA/0?wx_fmt=png)

屏幕一点, 效果立显
![img](https://mmbiz.qpic.cn/mmbiz_png/ScjMzsiaicOvba2Luv90zKicvhDudjyafLZrdNOF4kSKhwrt6shqtIOR1MgcLicr4RanNwNy2KKqo8LqOibgmOjkp6w/0?wx_fmt=png)

友情提示:

> 1. 这里 tmplIds 用的是订阅消息 id 哦, 不要搞错咯
> 2. 这里必须是在手机上才能看到效果哦
> 3. 每次弹框, 只能配置最多 3 个订阅消息哦
> 4. 如果勾选了: “总是保持以上选择, 不再询问” , 真的就是“此生不复相见哦”, 删除了小程序也不管用哦
> 5. 由于弹出的 3 个订阅消息, 是可以单独勾选, 就会出现如果某 1 个配置的已经“总是保持以上选择, 不再询问”. 那么弹框只会显示其他两个哦, 属于正常情况. 不要以为是哪里错了哈. 并且返回的结果还是 3 个(不要晕哈, 说的啰嗦, 其实不难理解)

小框框弹出来了, 返回也很顺利拿到了, 抿一口手边的枸杞菊花茶, 是不是很舒服?

**上面说到了, “总是保持以上选择, 不再询问” , 就是“此生不复相见哦”, 那么如果之前手贱, 点了拒绝. 那如何才能重新订阅呢?** 小生也是研究了的:

操作步骤: 右上角点点点, 》 设置 》订阅消息
效果一目了然

![img](https://mmbiz.qpic.cn/mmbiz_png/ScjMzsiaicOvba2Luv90zKicvhDudjyafLZ1ROXX814ycSxDIsVFtm3eGHJCFzqHBPiapI6p8gMuuzibH1h0WetfFUg/0?wx_fmt=png)

前方高能:
**设置里的订阅消息, 它此生的标签是 “总是保持以上选择, 不再询问”, 不管是你允许还是拒绝, 都不会在弹框里再看到**

写在最后
提一个更苦逼的事情, **记得把之前为获取 formid 而写的代码, 统统删掉**

写在最最后
给不给点赞? 不点我下一篇还问

未完待续…

**以下是补充哦, 持续关注订阅消息**

一: **一个模版, 在首页勾选了“总是保持以上选择, 不再询问”按钮. 在别的页面也将不会有弹框**. 你懂的, 在产品角度这个是很重要、很关键的交互需求

二: **同意次数是可以累计的.** 也就是说, 一个模版, 客户A点击了 10 次允许发送消息. 那我们就可以给他发 10 次模版消息提醒

三: **一次拒绝, 是不会清除之前同意所累计的次数的** 这个是针对有网友说: “点一次同意, 再点击一次拒绝,是收不到消息的”. 实践证明: 点一次同意, 就能发一次消息, 后面点击拒绝, 不影响之前点击同意的

四: 有网友问: ”一个弹框有三个模版, 全都勾选并同意. 可以发几条消息? “ 很明显是**三个模版每个可以发一次**. 这个也是验证了的

干活!! 是不是满满的都是干活!



[原文地址](https://developers.weixin.qq.com/community/develop/article/doc/000060b0950b80340b990c9c856413?jumpto=comment&commentid=000e62a6898f00989d1ba31f4560)

