# grid-template

简写！类似于 background；

能把 grid-template-area、grid-template-rows、grid-template-columns 缩写在一起；


```css

/* grid-template-rows / grid-template-columns values */
grid-template: repeat(4, 60px) / repeat(5, 80px) 60px;

```


<style>
    .grid-box {
        width: 400px;
        display: grid;
        grid-template: repeat(4, 60px) / repeat(5, 80px) 60px;
        gap: 10px;
    }
    .grid-item {
        border: 1px solid #666;
        border-radius: 10px;
    }
</style>
<!-- 底层表格 -->
<div class="grid-box">
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
    <div class="grid-item"></div>
</div>

```css
    /* 
     grid-template: 
    "a a a a" 行高
    "b c c c" 行高
    "b c c c" 行高
    "d d d d" 行高 / 列宽 列宽;
        */
    grid-template: 
    "a a a a" 60px
    "b c c c" 80px
    "b c c c" 80px
    "d d d d" 80px / 60px 1fr;
```

<style>
    .grid-box02 {
        width: 400px;
        display: grid;
        grid-template: 
        "a a a a" 60px
        "b c c c" 80px
        "b c c c" 80px
        "d d d d" 80px / 60px 1fr;
        gap: 10px;
    }
    .item {
        border: 1px solid #666;
        border-radius: 10px;
    }
    .item01 {
        grid-area: a;
    }
    .item02 {
        grid-area: b;
    }
    .item03 {
        grid-area: c;
    }
    .item04 {
        grid-area: d;
    }
</style>
<!-- 底层表格 -->
<div class="grid-box02">
    <div class="item item01"></div>
    <div class="item item02"></div>
    <div class="item item03"></div>
    <div class="item item04"></div>
</div>