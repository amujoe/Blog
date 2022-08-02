# 你真的会 return 吗？

### 是不是我想用 return 的时候就 return ？

return语句终止函数的执行，并返回一个指定的值给函数调用者


## return
return语句终止函数的执行，并返回一个指定的值给函数调用者。<a target = "blank"  href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/return">MDN 文档地址</a>

```js

// return 怎么用？ 看着代码熟悉吗？  你品 细品
function getSkyColor() {
   if(...) {
      // 01
      return "red"
   } else {
      // 02
      return "black"
   }
   // 03
   return "gray"
}

// 1 2 3 三个点，你觉得哪些没必要？ 

// 有同学说平时都不写 return
function goHome(url) {
   // 走你
   window.location.href = url
}

/**
* 问题来了，我平时方法里都没有写 return，返回的是什么？ 
* A：不返回
* B：返回函数本身
* C：返回 false
* D：返回 undefined
* 
* 你猜？ 答对有奖，我不会告诉你是 D 的
*/

```

## 总结
retrun true； 返回正确的处理结果。

return false；分会错误的处理结果，终止处理。

return；把控制权返回给页面。
