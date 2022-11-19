# 什么是 Composition——API ？

举起放大镜，靠近5厘米，再靠近5厘米, 再靠近...  

*****

### Options-API
首先，先了解一下 Composition——API 的“孪生兄弟” ： Options-API

在vue2中，我们会在一个vue文件中定义methods，computed，watch，data中等等属性和方法，共同处理页面逻辑,我们称这种方式为Options API

```js
// -- Options-API
export default {
   data: {
      one: "我是谁？"，
      two: "我在那？"
   },
   methods: {
      // 我要回家
      goHome() {},
      // 不，你不想回家
      goPlay() {}
   },
   computed: {
      say() {
         return this.one + this.two
      }
   }
}
```

再回过头看
### Composition——API
Composition 翻译：作文、构成、组合方式

Composition-API  翻译：合成API

它是为了实现基于函数的逻辑复用机制而产生的。

Vue核心团队将组件 Composition API 描述为 “一套附加的、基于函数的api”，允许灵活地组合组件逻辑


```js
// -- Composition-API
<script setup lang="ts">

const one = "我是谁？"，
      two ="我在那？"

const goHome = () => {
   // 我要回家
}

const goPlay = () => {
    // 不，你不想回家
}

</script>

```


### 对比
Options-Api： 一个功能往往需要在不同的vue配置项中定义属性和方法，比较分散，项目小还好，清晰明了，但是项目大了后，一个methods中可能包含很多个方法，你往往分不清哪个方法对应着哪个功能

Composition-API 条例清晰,相同的放在相同的地方;但随着组件功能的增大,关联性会大大降低,组件的阅读和理解难度会增加

![对比图](https://pic2.zhimg.com/80/v2-3215832798dad4d85252c140e509f445_1440w.webp)
