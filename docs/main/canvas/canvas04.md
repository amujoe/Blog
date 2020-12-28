# canvas 基础之绘制路径

## 绘制路径
图形的基本元素是路径。路径是通过不同颜色和宽度的线段或曲线相连形成的不同形状的点的集合。

绘制路径的步骤:
1. 首先，你需要创建路径起始点
2. 然后你使用画图命令去画出路径
3. 之后你把路径封闭
4. 一旦路径生成，你就能通过描边或填充路径区域来渲染图形

知识点: 

`beginPath()` 新建一条路径，生成之后，图形绘制命令被指向到路径上生成路径

`closePath()` 闭合路径之后图形绘制命令又重新指向到上下文中

`fill()` 通过填充路径的内容区域生成实心的图形; 当你调用fill()函数时, 所有没有闭合的形状都会自动闭合

`stroke()` 通过线条来绘制图形轮廓; 不会自动闭合路径

`moveTo(x, y)` 移动触笔; 将笔触移动到指定的坐标x以及y上. 在画线的时候, 是连续的路径, moveTo()改变笔触, 就可以绘制一些不连续的路径


## 线
这里指的的直线, 用到的方法lineTo()

`lineTo(x, y)` 

* x, y 代表坐标系中直线结束的点
* 开始点和之前的绘制路径有关，之前路径的结束点就是接下来的开始点
* 开始点也可以通过moveTo()函数改变
* 画完线后, fill()可以填充图形, stroke()可以对线进行描边


```js
   
  const ctx = document.getElementById('mycanvas').getContext('2d');
       
  // 画一个填充三角形
  ctx.beginPath();
  ctx.moveTo(25, 25);
  ctx.lineTo(105, 25);
  ctx.lineTo(25, 105);
  ctx.fill();
         
  // 画一个描边三角形
  ctx.beginPath();
  ctx.moveTo(125, 125);
  ctx.lineTo(125, 45);
  ctx.lineTo(45, 125);
  ctx.closePath();
  ctx.stroke();
   
```
