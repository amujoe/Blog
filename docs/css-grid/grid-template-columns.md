# grid-template-columns （列）

该属性是基于 网格列 的维度，去定义网格线的名称和网格轨道的尺寸大小


> 语法  <span style="color: #42b983;">grid-template-columns: none | length | percentage | flex | max-content | min-content | minmax(min, max) | auto </span>


- <b style="color: #42b983;">none</b>: 这个关键字表示不明确的网格。所有的列和其大小都将由grid-auto-columns 属性隐式的指定。
- <b style="color: #42b983;">length</b>: 非负值的长度大小。
- <b style="color: #42b983;">percentage</b>: 非负值且相对于网格容器的 <percentage>。如果网格容器的尺寸大小依赖网格轨道的大小（比如 inline-grid），则百分比值将被视为 auto。 为了遵守网格的百分比，网格轨道本身定义的大小，将自动被调整为相对网格容器大小，并且是以最小量将网格轨道调整到最终的大小。
- <b style="color: #42b983;">flex</b>：非负值，用单位 fr 来定义网格轨道大小的弹性系数。每个定义了 <flex> 的网格轨道会按比例分配剩余的可用空间。当外层用一个 minmax() 表示时，它将是一个自动最小值（即 minmax(auto, <flex>)）。

- <b style="color: #42b983;">max-content</b>：是一个用来表示以网格项的最大的内容来占据网格轨道的关键字。

- <b style="color: #42b983;">min-content</b>：是一个用来表示以网格项的最大的最小内容来占据网格轨道的关键字。

- <b style="color: #42b983;">minmax(min, max)</b>：
是一个来定义大小范围的属性，大于等于 min 值，并且小于等于 max 值。如果 max 值小于 min 值，则该值会被视为 min 值。最大值可以设置为网格轨道系数值 flex ，但最小值则不行。

- <b style="color: #42b983;">auto</b>：如果该网格轨道为最大时，该属性等同于 max-content，为最小时，则等同于 min-content。



```css
    /* 重复4个， 每个60px; */
    grid-template-columns: repeat(4, 60px); 

    /* minmax, 空间够大时候，会占据最大空间； 不够大时候，被挤压到最小空间 */
    grid-template-columns: 60px minmax(60px, 100px) 60px 100px 60px;
    grid-template-columns: 60px minmax(60px, 100px) 60px 100px 60px 60px;

    /* flex， 根据比例缩放 */
    grid-template-columns: 1fr 2fr 3fr 1fr;

```


<style>
    .grid-box {
        width: 400px;
        display: grid;
        /* 重复4个， 每个60px; */
        grid-template-columns: repeat(4, 60px); 

        /* minmax, 空间够大时候，会占据最大空间； 不够大时候，被挤压到最小空间 */
        grid-template-columns: 60px minmax(60px, 100px) 60px 100px 60px;
        grid-template-columns: 60px minmax(60px, 100px) 60px 100px 60px 60px;

        /* flex， 根据比例缩放 */
        /* grid-template-columns: 1fr 2fr 3fr 1fr; */
        grid-gap: 10px;
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

[点击查看完整demo](https://codepen.io/joe-amu/pen/mydXXpB)

<iframe height="300" style="width: 100%;" scrolling="no" title="Untitled" src="https://codepen.io/joe-amu/embed/mydXXpB?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/joe-amu/pen/mydXXpB">
  Untitled</a> by joe amu (<a href="https://codepen.io/joe-amu">@joe-amu</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>