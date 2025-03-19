# grid-gap 

用于设置行与列之间的间隙

规范的早期版本将该属性命名为 grid-gap，且为了保持与旧网站的兼容性，浏览器仍然会接受 grid-gap 作为 gap 的别名。


<style>
    .grid-box {
        width: 400px;
        display: grid;
        grid-template-columns: repeat(4, 60px); 
        grid-template-rows: 60px 60px 60px 60px;
        gap: 5px 20px;
    }
    .grid-item {
        width: 60px;
        height: 60px;
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

原谅我无法用过多大语言的形容它，以下是一些写法的例子；一看便懂

``` css

/* 一个 <length> 值 */
gap: 20px;
gap: 1em;
gap: 3vmin;
gap: 0.5cm;

/* 一个 <percentage> 值 */
gap: 16%;
gap: 100%;

/* 两个 <length> 值 */
gap: 20px 10px;
gap: 1em 0.5em;
gap: 3vmin 2vmax;
gap: 0.5cm 2mm;

/* 一个或两个 <percentage> 值 */
gap: 16% 100%;
gap: 21px 82%;

/* calc() 值 */
gap: calc(10% + 20px);
gap: calc(20px + 10%) calc(10% - 5px);

/* 全局值 */
gap: inherit;
gap: initial;
gap: revert;
gap: revert-layer;
gap: unset;

```

####  gap 其实是一种简写；最小的单位是 row-gap 和 column-gap

```css

gap: 20px 10px;

// 等同于 

row-gap: 20px; 
column-gap: 10px

```


就类似 margin 可以拆分四个属性（margin-top, margin-right, margin-bottom, margin-left )来写, 这样更容易理解他们的关系； 他们的目标是一致的！