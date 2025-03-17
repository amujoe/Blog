# 这里说些什么呢？


## Grid 动态示例（支持点击调整列数）

<style>
 .grid-box {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-gap: 10px;
  background-color: #fff;
  color: #444;
}

.grid-item {
  background-color: #444;
  color: #fff;
  border-radius: 5px;
  padding: 20px;
  font-size: 150%;
}

</style>

<div class="grid-box">
  <div class="grid-item grid01">A</div>
  <div class="grid-item grid02">B</div>
  <div class="grid-item grid03">C</div>
  <div class="grid-item grid04">D</div>
  <div class="grid-item grid05">E</div>
  <div class="grid-item grid06">F</div>
</div>

<script>
  function changeGrid() {
    document.getElementById("grid").style.gridTemplateColumns = "repeat(4, 1fr)";
  }
</script>

<iframe height="300" style="width: 100%;" scrolling="no" 
src="https://codepen.io/joe-amu/pen/xbxYGpO" frameborder="no" 
loading="lazy" allowtransparency="true" allowfullscreen="true">
</iframe>
