# canvas基础之扫盲篇


## 文字

canvas 两种方法来渲染文本: **实心文本**、**空心文本**(反正名字我就这么叫, 有人把空心文本叫描边文本, 无所谓, 我不在乎, 气人不)


**实心文本**

`fillText(text, x, y [, maxWidth])`

**空心文本**

`strokeText(text, x, y [, maxWidth])`


**对齐方式**

`textAlign = value`   value 值: start, end, left, right or center. 默认值是 start。

**基准线**

`textBaseline = value`  value 值: top, hanging, middle, alphabetic, ideographic, bottom。默认值是 alphabetic。

**文本方向**

`direction = value` 文本方向。可能的值包括：ltr, rtl, inherit。默认值是 inherit。

<!-- tabs:start -->

#### ** A HTML **

```html
   <!-- id 很重要 -->
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

canvas 矩形和路径

`fillRect(x, y, width, height)`  绘制一个填充矩形

`strokeRect(x, y, width, height)`  绘制一个描边矩形

`clearRect(x, y, width, height)`  清楚一个矩形区域. 形象的说就是一个矩形橡皮擦


<!-- tabs:start -->

#### ** B HTML **

```html
   <!-- id 很重要 -->
   <canvas id="mycanvas" width="500" height="500"></canvas>
```


#### ** B JS **

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

<!-- tabs:end -->

## 圆形

## 图片



