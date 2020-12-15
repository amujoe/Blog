# new Date(date)  在 mac 自带浏览器 safari 报错: Invalid date in safari



### 问题描述:

`new Date("2020-12-15 00:00:00") `   时候,  mac 自带浏览器 safari  报错: Invalid date in safari



### 解析原因:

我们经常用的时间格式:  `yyyy-MM-dd HH:mm:ss `.  这是一种标准. 然而 safari 并不支持(不要问为什么). 

safari 支持的格式有: 

```js
MM-dd-yyyy

yyyy/MM/dd 

MM/dd/yyyy 

MMMM dd

yyyy MMM dd

yyyy，

```

所以我们在用 `new Date("2020-12-15 00:00:00"`  直接报错



### 解决方案:

最简单的就是:

```js
let date =  new Date("2020-12-15 00:00:00".replace(/-/g, "/"))
```

当然也可以使用一些时间处理库，比如 :date-fns   moments.js 等. 