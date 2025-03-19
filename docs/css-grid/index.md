# Grid (网格)


<style>
    .box-one{
        width: 60px;
        height: 60px;
        border: 1px solid #666;
    }
    .box-four{
        position: relative;
        width: 120px;
        height: 120px;
        border: 1px solid #666;
        margin: 20px 0;
    }
    .box-four::before {
        position: absolute;
        content: " ";
        left: 0;
        top: 50%;
        width: 100%;
        height: 1px;
        background: #999;
    }
    .box-four::after {
        position: absolute;
        content: " ";
        left: 50%;
        top: 0;
        width: 1px;
        height: 120px;
        background: #999;
    }

    .grid-box {
        width: 400px;
        display: grid;
        grid-template-columns: repeat(4, 60px);
        grid-template-rows: repeat(4, 60px);
        /* margin: 20px auto; */
        grid-gap: 10px;
        /* column-gap: 20px; */
        /* row-gap: 10px; */
    }
    .grid-item {
        width: 60px;
        height: 60px;
        border: 1px solid #666;
        /* border-radius: 10px; */
    }
</style>
<div class="box-one"></div>

格子你肯定知道吧，像不像你每天搬的砖

<div class="box-four"></div>

田字格，四四方方一座城； 你写过中国字, 就肯定用过田字格的本子；没写过？ 那你应该是生在日狗的地方了，请你出去

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
</div>

grid 在四方格的基础上，无限延伸，而且可以有间隙;

说到这，你应该对 grid 有一定的感觉了哈；

*在一个容器里，画一些有间隙的格子，做为底层坐标*



<style>
 .demo-box {
    position: relative;
 }
 .wrapper-box {
    position: absolute;
    left: 0;
    top: 0;
    display: grid;
    grid-gap: 10px;
    grid-template-columns: 60px 130px 60px;
    grid-template-rows: 60px 200px 60px;
    grid-template-areas:
    "header  header  header"
    "sidebar1 content content"
    "footer  footer  footer";
    background-color: #fff;
    color: #444;
    /* background: url(../image/grid.png) repeat left top/400px auto; */
    opacity: 0.5;
}
.box {
  background-color: #6F9292;
    /* background: #c5c5c5!important; */
  color: #fff;
  border-radius: 5px;
  padding: 10px;
  font-size: 20px;
}

.header {
    grid-area: header;
    background: #4E7B7B;
}
.grid-sidebar {
  grid-area: sidebar1;
  background: #6F9292;
}

.grid-content {
    grid-area: content;
    background: #A5BCBC;
}


.footer {
    grid-area: footer;
    background: #336868;
}

</style>

<div class="demo-box">
    <!-- layout 布局 -->
    <div class="wrapper-box">
        <div class="box header">Header</div>
        <div class="box grid-sidebar">Sidebar</div>
        <div class="box grid-content">Content</div>
        <div class="box footer">Footer</div>
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

做为一个前端，你应该很了解这个布局；你是用定位实现的？还是用flex布局实现的？


##### 废话止步于此，下面是我学习的节奏

很多人和我一样，一看w3c、MDN的手册，就头大；学习前端，还是要从手边开始，从经常用到的下手，从随意一写就能出效果的属性下手； 下面是我给大家整理的，双手奉上

* [grid-template-rows](/css-grid/grid-template-rows.md)
* [grid-template-columns](/css-grid/grid-template-columns.md)
* [grid-grp](/css-grid/grid-grp.md)
* [grid-area](/css-grid/grid-area.md)