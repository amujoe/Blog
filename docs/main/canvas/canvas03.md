# canvas基础之扫盲篇


## 文字

canvas 两种方法来渲染文本: **实心文本**、**空心文本**(反正名字我就这么叫, 有人把空心文本叫描边文本, 无所谓, 我不在乎, 气人不)


**实心文本**

`fillText(text, x, y [, maxWidth])`

**空心文本**

`strokeText(text, x, y [, maxWidth])`

* text 是文本的内容
* x, y 为文本原点的位置 (默认原点是左上角)
* maxWidth 设置矩形的宽高

**对齐方式**

`textAlign = value`   value 值: start, end, left, right or center. 默认值是 start。

**基准线**

`textBaseline = value`  value 值: top, hanging, middle, alphabetic, ideographic, bottom。默认值是 alphabetic。

**文本方向**

`direction = value` 文本方向。可能的值包括：ltr, rtl, inherit。默认值是 inherit。

<!-- tabs:start -->

#### ** A HTML **

```html
  <!-- js 有点长, 放在右边  -->
  
  <!-- id 很重要  -->
  <canvas id="mycanvas" width="500" height="500"></canvas>
```


#### ** A JS **

```js
   
   // 预览一下,  对齐方式、基准线、文本方向  一目了然
   
   const ctx = document.getElementById('mycanvas').getContext('2d');
   
   // 画一个线 做对比 start (这里可以忽略)
   ctx.strokeStyle = "rgba(158, 161, 139, 0.9)";
   ctx.strokeRect(0, 0, 500, 500)
   
   ctx.beginPath();
   ctx.moveTo(250, 0);
   ctx.lineTo(250, 500);
   ctx.stroke();
   ctx.closePath();
   
   ctx.beginPath();
   ctx.moveTo(0, 250);
   ctx.lineTo(500, 250);
   ctx.stroke();
   ctx.closePath();
   // 画线完成 end
   
   
   // 描边文本
   ctx.font = "30px serif"
   ctx.strokeText("躲在角落", 370, 480);
   
   // 对齐方式 textAlign:  value
   // value 值: start, end, left, right or center. 默认值是 start
   
   ctx.font = "18px serif";
   ctx.fillText("textAlign = start", 250, 20);
   
   ctx.textAlign = "end"
   ctx.fillText("textAlign = end", 250, 40);
   
   ctx.textAlign = "left"
   ctx.fillText("textAlign = left", 250, 60);
   
   ctx.textAlign = "center"
   ctx.fillText("textAlign = center", 250, 80);
   
   ctx.textAlign = "right"
   ctx.fillText("textAlign = right", 250, 100);
   
  // textBaseline 文本基准线;
  // value 值: top, hanging, middle, alphabetic, ideographic, bottom。默认值是 alphabetic。
   
   ctx.textAlign = "start"
   ctx.font = "14px serif";
   ctx.fillText("baseline", 20, 220);
   
   ctx.font = "18px serif";
   ctx.textBaseline = "top"
   ctx.fillText("top", 5, 250);
   
   ctx.textBaseline = "bottom"
   ctx.fillText("bottom", 5, 250);
   
   ctx.textBaseline = "hanging"
   ctx.fillText("hanging", 80, 250);
   
   ctx.textBaseline = "middle"
   ctx.fillText("middle", 170, 250);
   
   ctx.textBaseline = "alphabetic"
   ctx.fillText("alphabetic", 230, 250);
   
   ctx.textBaseline = "ideographic"
   ctx.fillText("ideographic", 330, 250);
   
   
   // direction 文本方向。可能的值包括：ltr, rtl, inherit。默认值是 inherit。
   ctx.textAlign = "start"
   ctx.textBaseline = "alphabetic"
   ctx.direction = "ltr"
   // ctx.textAlign = "end"
   ctx.fillText("direction = ltr", 250, 400);
   
   ctx.direction = "rtl"
   // ctx.textAlign = "start"
   ctx.fillText("direction = rtl", 250, 420);
   
   ctx.direction = "inherit"
   ctx.textAlign = "start"
   ctx.fillText("default direction = inherit", 250, 440);
   

```

<!-- tabs:end -->


## 矩形

canvas 中分为: 矩形和路径

`fillRect(x, y, width, height)`  绘制一个填充矩形
* x, y 为矩形原点的位置 (默认原点是左上角)
* width,height 设置矩形的宽高

`strokeRect(x, y, width, height)`  绘制一个描边矩形

`clearRect(x, y, width, height)`  清楚一个矩形区域. 形象的说就是一个矩形橡皮擦


```js
   
   // 预览一下  效果更直观
   const ctx = document.getElementById('mycanvas').getContext('2d');
   
   // 画一个描边的
   ctx.strokeStyle = "rgba(158, 161, 139, 0.9)";
   ctx.strokeRect(0, 0, 500, 500)
   
   // 画一个实心的
   ctx.fillStyle = "rgba(53, 255, 64, 0.5)";
   ctx.fillRect(25, 25, 100, 100);
   
   // 再画一个实心的
   ctx.fillStyle = "rgba(252, 61, 50, 0.5)";
   ctx.fillRect(75, 75, 100, 100);
   
   // 然后擦除矩形
   ctx.clearRect(85, 85, 30, 30);
   
```


## 圆
canvas 中分为: 圆形与圆弧


`arc(x, y, radius, startAngle, endAngle, anticlockwise)`  画一个以（x,y）为圆心的以radius为半径的圆弧（圆）

* x, y 为圆心的位置
* radius: 半径
* startAngle 开始的弧度
* endAngle 结束的弧度
* anticlockwise  为一个布尔值, 默认为顺时针. 为true时，是逆时针方向, 否则是顺时针

`arcTo(x1, y1, x2, y2, radius)`  根据给定的控制点和半径画一段圆弧，再以直线连接两个控制点

注意：arc()函数中表示角的单位是弧度，不是角度。角度与弧度的js表达式: 弧度=(Math.PI/180)*角度。

```js
  const ctx = document.getElementById('mycanvas').getContext('2d');
  
  // 画一实心圆
  ctx.beginPath();
  ctx.arc(100, 100, 50, 0, Math.PI * 2, true); // 绘制
  
  // 画一个圆弧
  ctx.moveTo(175, 100);
  ctx.arc(100, 100, 75, 0, Math.PI, true);   // 口(顺时针)
  
  // 描边路径
  ctx.stroke();
  
  // 画一个圆角
  ctx.beginPath();
  ctx.strokeStyle = "rgba(40, 231, 50, 0.9)";
  ctx.moveTo(100, 100);
  ctx.lineTo(200, 100);
  ctx.arcTo(250, 100, 250, 150, 50);
  ctx.lineTo(250, 300);
  ctx.stroke();
  
```

## 图片

* 多用于动态的图像合成
* 浏览器支持的任意格式的外部图片都可以使用

**多种写法**

第一种: 直接写入

`context.drawImage(img,x,y);`

第二种: 设定宽高

`context.drawImage(img,x,y,width,height);`

第三种: 可以裁剪

`context.drawImage(img,sx,sy,swidth,sheight,x,y,width,height);`

| 参数 | 描述 |
|  ----  | ----  |
| img	| 规定要使用的图像、画布或视频。
| sx | 	可选。开始剪切的 x 坐标位置。
| sy	| 可选。开始剪切的 y 坐标位置。
| swidth	| 可选。被剪切图像的宽度。
| height	| 可选。被剪切图像的高度。
| x	| 在画布上放置图像的 x 坐标位置。
| y	| 在画布上放置图像的 y 坐标位置。
| width	| 可选。要使用的图像的宽度。（伸展或缩小图像）
| height	| 可选。要使用的图像的高度。（伸展或缩小图像）

```js

  const ctx = document.getElementById('mycanvas').getContext('2d');
   
  // 内存中先加载，然后当内存加载完毕时，再把内存中的数据填充到我们的 dom元素中
  var img = new Image();
  img.onload = function(){
   
    // 将图片画到canvas上面上去！
    ctx.drawImage(img, 350, 350);
     
    // 设置图像的宽高
    ctx.drawImage(img, 50, 50, 200, 200);
     
    // 裁剪, 然后绘制
    ctx.drawImage(img, 0, 0, 100, 100, 250, 250, 100, 100);
  }
  img.src= "https://alifei05.cfp.cn/creative/vcg/veer/800water/veer-167645584.jpg"

```