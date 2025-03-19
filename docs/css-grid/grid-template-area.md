# grid-template-area

指定命名的网格区域，建立网格中的单元格并为其分配名称


还记得刚才看到这个图嘛？ 



<style>
 .demo-box {
    position: relative;
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


用 grid-template-area 来实现，很简单


```css

/* 父级根据点布局，建立网格，并给每个格子命名 */
 .wrapper-box {
    ...
    grid-template-areas:
    "header  header  header"
    "sidebar1 content content"
    "footer  footer  footer";
    ...
}

/* 子元素 定义名字，便可以填充到指定区域 */
.grid-header {
    grid-area: header;
}
.grid-sidebar {
  grid-area: sidebar1;
}
.grid-content {
    grid-area: content;
}
.grid-footer {
    grid-area: footer;
}
```