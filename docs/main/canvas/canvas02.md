# 一分钟入门之 HelloWorld


实现一个canvas的两个要素

1. html 的标签

   ```html
   <!-- id 很重要, 也不知道为什么都喜欢起名为 mycanvas -->
   <canvas id="mycanvas"></canvas>
   ```

2. js 

   ```js
   <script>
     const ctx = document.getElementById('mycanvas').getContext('2d');
     
     ctx.font = "32px serif";
     ctx.fillText("Hello world", 10, 50);
   </script>
   ```

3. 找一个浏览器打开

