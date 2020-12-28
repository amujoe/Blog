# 一分钟入门之 HelloWorld


实现 canvas 入门之灵魂篇 HelloWorld 的步骤:

1. **html 的标签**

   ```html
   <!-- id 很重要, 宽高如果不设置, 会默认 300*150px -->
   <canvas id="mycanvas" width="150" height="150"></canvas>
   ```

2. **js**

   ```js
   <script>
     const ctx = document.getElementById('mycanvas').getContext('2d');
     
     ctx.font = "32px serif";
     ctx.fillText("Hello world", 10, 50);
   </script>
   ```

3. **找一个浏览器打开**

