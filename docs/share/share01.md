# if 你的姿势对 else 就会闪到腰

*****

## if else
当指定条件为真，if 语句会执行一段语句。如果条件为假，则执行另一段语句。<a target = "blank"  href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/if...else">MDN 文档地址</a>

``` javascript
 // 判断颜色
 if(color === "green"){
    console.log("green")
 } else if(color === "red") {
    console.log("red")
 } else if(color === "blue") {
    console.log("blue")
 } else {
    color.log("unknown color")
 }
 ```


## switch case
switch 语句评估一个表达式，将表达式的值与case子句匹配，并执行与该情况相关联的语句。<a target = "blank"  href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/switch">MDN 文档地址</a>

``` javascript

 switch(color) {
    case "green":
        console.log("green")
        break;
    case "red":
        console.log("red")
        break;
    case "blue":
        console.log("blue")
        break;
    default:
        console.log("unknown color")
        break;
 }

```

## 对比区别
|        |  if else   | switch case  |
|  ----  |  :----  | :----  |
|  优点  | 灵活，使用场景多  | 当分支较多时，用switch的效率是很高的 |
|  缺点  | 1.必须遍历所以得可能值 <br> 2.嵌套太多时，可读性差  | 只能处理case为常量的情况 |


## 使用
1. 判断的值是区间，只能用 if
2. 判断值少数的几个数字，字符，字符串, 使用 switch 比较简单清晰


## 总结
if 比 switch 用途更广泛；在少数情况下，用 switch 比 if 更有效，代码更清晰
