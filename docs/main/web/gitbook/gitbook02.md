# 如何增加评论




### 有现成的, 就不需要造轮子

[Valine](https://valine.js.org/) 是偶然间看到的一个评论



#### 第一步: 注册leanCloud 账号

1. 注册 [leanCloud](https://leancloud.cn/) 账号,
2. 进入控制台, 创建一个应用
3. 应用创建好以后，进入刚刚创建的应用，选择左下角的 设置>应用 Key, 然后就可以看到你的 APP ID 和 APP Key 了




#### 第二部: gitbook 配置 Valine
1. 配置

```
{
    "plugins": ["valine"],
    "pluginsConfig": {
        "valine": {
            "appId": "your appId", // 这里是第一步你拿到你自己的 appId
            "appKey": "your appKey" // 这里是第一步你拿到你自己的 appKey
        }
    }
}
```

2. 然后 gitbook install
3. gitbook serve 运行一下,  评论已然出现了, 就是这么简单!