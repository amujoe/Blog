# grid-area

用于指定一个网格项的大小和位置；

> 语法一  <span style="color: #42b983;">grid-area</span>: grid-row-start / grid-column-start / grid-row-end / grid-column-end （grid-area: 开始行\开始列\结束行\结束列）

> 语法二  <span style="color: #42b983;">grid-area</span>: custom-ident （自定义标识） [在这里理解更容易](/css-grid/grid-template-area.md)

> 重点： 这个属性是给到子元素的，不是给父级的

```css

    /* 只写第一个，代表第3行，第3个 ； 如图1*/
    grid-area: 4

    /* 写了前两个，代表开始于第2行，第2列 ； 如图2 */
    grid-area: 2 / 2

    /* 写了三个， 只识别前两个，第三个是无效; 如图3 */
    grid-area: 3 / 3 / 5

    /* 四个都写，就是开始到结束坐标； 如图4 */
    grid-area: 4 / 1  / 4 / 3

    /* 还可以模仿表格里面的合并单元格，span 3; 意思合并3个格子； 如图5 */
    grid-area: 1 / 2 / 1 / span 3

    /** 如果只写一个, 譬如 3； 3行3列的位置有元素占着，自动分配为3行1列； 如图6； */
     grid-area: 3

    /* 如果行/列都写，则会覆盖展示，如图7 */
     grid-area: 3 / 3；
```

<style>
    .demo-box {
        position: relative;
    }
    .grid-box {
        width: 400px;
        display: grid;
        grid-template-columns: repeat(5, 60px); 
        grid-template-rows: 60px 60px 60px 60px 60px;
        gap: 5px 20px;
    }
    .grid-item {
        /* width: 60px;
        height: 60px; */
        line-height: 60px;
        text-align: center;
        font-size: 18px;
        border: 1px solid #eee;
        border-radius: 10px;
    }
    .position {
        position: absolute;
        left: 0;
        top: 0;
        opacity: 0.5;
    }
    .position .grid-item {
        border-color: red;
    }

    .item01 {
        grid-area: 4
    }

    .item02 {
        grid-area: 2 / 2
    }

    .item03 {
        grid-area: 3 / 3 / 5;
        line-height: 120px;
    }

    .item04 {
        grid-area: 4 / 1  / 4 / 3
    }
    .item05 {
        grid-area: 1 / 2 / 1 / span 3
    }
    .item06 {
        grid-area: 3
    }
    .item07 {
        grid-area: 3 / 3
    }

</style>

<div class="demo-box">
    <!-- layout 布局 -->
    <div class="grid-box position">
        <div class="grid-item item01">1</div>
        <div class="grid-item item02">2</div>
        <div class="grid-item item03">3</div>
        <div class="grid-item item04">4</div>
        <div class="grid-item item05">5</div>
        <div class="grid-item item06">6</div>
        <div class="grid-item item07">7</div>
    </div>
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
</div>

<span style="color: red;">下面是做了一个对比；第三部分是最小单位，第一二部分都是简写；不用被这么多标签所迷惑；</span>

#### grid-area

> 语法  <span style="color: #42b983;">grid-area</span>: grid-row-start / grid-column-start / grid-row-end / grid-column-end （grid-area: 开始行\开始列\结束行\结束列）

#### grid-row / grid-column


> 语法  <span style="color: #42b983;">grid-row </span> : grid-row-start / grid-row-end (开始的行 / 结束的行)


> 语法  <span style="color: #42b983;">grid-column </span> : grid-column-start / grid-column-end (开始的列 / 结束的列)


#### grid-row-start / grid-column-start / grid-row-end / grid-column-end 

属性通过为网格位置贡献一条线、一个跨度或什么都不做（自动）来指定网格项在网格行内的开始/结束位置

> 语法  <span style="color: #42b983;">grid-row-start </span>: auto | integer | span integer   (auto, 数字， span + 数字)

> 语法  <span style="color: #42b983;">grid-row-end </span>: auto | integer | span integer   (auto, 数字， span + 数字)

> 语法  <span style="color: #42b983;">grid-column-start </span>: auto | integer | span integer   (auto, 数字， span + 数字)

> 语法  <span style="color: #42b983;">grid-column-end </span>: auto | integer | span integer   (auto, 数字， span + 数字)
