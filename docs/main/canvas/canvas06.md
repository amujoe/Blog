
# canvas动画之动画





想要一个元素动起来, 在 canvas 里面要用到, 清除、保存、重绘等

先来了解一下:

`ctx.clearRect(x, y, width, height)` 清楚画板

如果没有参数, 则清空画板里的所有内容, 如果有参数, 则清空制定区域内的



`ctx.save()` 保存画板的内容

任何情况下, 每当save()方法被调用后, 当前的状态就被推送到栈中保存。一个绘画状态包括：

* 当前应用的变形（即移动，旋转和缩放，见下）
* 以及下面这些属性：strokeStyle, fillStyle, globalAlpha, lineWidth, lineCap, lineJoin, miterLimit, lineDashOffset, shadowOffsetX, shadowOffsetY, shadowBlur, shadowColor, globalCompositeOperation, font, textAlign, textBaseline, direction, imageSmoothingEnabled


`ctx.restore()`  恢复画板里保存的内容

每一次调用 restore 方法，上一个保存的状态就从栈中弹出，所有设定都恢复。


有了上面这个肯定是不够的, 还需要定时去操作, 就会用到以下知识点:

`setInterval(function, delay)` 当设定好间隔时间后, 

`setTimeout(function, delay)`

`requestAnimationFrame(callback)` 告诉浏览器你希望执行一个动画，并在重绘之前，请求浏览器执行一个特定的函数来更新动画。



```js

  // 动画: 一个正方形
   const ctx = document.getElementById('mycanvas').getContext('2d');
   
   let canvasW = 100;
   let canvasH = 100;
   let x = 0;
   let y = 0;
   let direction = "t";  // 顶:t 右:r, 下: b, 左: l
   
   
   function drawT() {
     console.log("direction = ", direction);
      // 画一个填充三角形
      if (direction == 't') {
        if (x >= canvasW - 1) {
          direction = 'r';
          return;
        }
        x ++;
      }
      
      if (direction == 'r') {
        y ++;
        if (y >= canvasH) {
          direction = 'b';
          return;
        }
      }
      
      if (direction == 'b') {
        x --;
        if (x <= 1) {
          direction = 'l';
          return;
        }
      }
      
      if (direction == 'l') {
        y --;
        if (y <= 1) {
          direction = 'l';
          return;
        }
      }
      
      ctx.beginPath();
      ctx.moveTo(x, y);
      ctx.lineTo(x + 1, y);
      ctx.strokeStyle = "rgba(158, 161, 139, 0.9)";
      ctx.stroke();
   }
   
   
   function loop() {
     console.log("loop", x, y);
     
     drawT();
     if (x > -1 && y > -1) {
        window.requestAnimationFrame(loop);
     }
   }
   // 启用
   window.requestAnimationFrame(loop);
        
```

