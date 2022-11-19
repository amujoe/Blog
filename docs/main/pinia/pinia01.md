# 初识 Pinia


[官网地址](https://pinia.vuejs.org/)

[中文手册](https://baimingxuan.net/pinia-doc-cn/guide/introduction.html#%E4%BB%8B%E7%BB%8D)


******

## 为什么大家叫它 菠萝 

Pinia(发音为/piːnjʌ/，就像英语中的“peenya”)是最接近piña(西班牙语中的 “菠萝pineapple”)的一个有效的包名。事实上，菠萝是一群单独的花朵结合在一起，形成了多个果实的一种水果。与Stores类似，每个store都是独立生成的，但他们最终都是连接在一起的。菠萝也是一种原产于南美洲的美味热带水果。



## Pinia API与Vuex ≤ 4有很大差异
- mutations不再存在。它们经常被认为非常啰嗦。它们最初带来了devtools的集成，但这不再是一个问题。

- 无需创建复杂的自定义包装器来支持TypeScript，所有东西都是类型化的，并且API的设计也尽可能利用TS类型推断。

- 无需额外的魔法字符串注入、引入函数和回调，享受自动完成的功能！

- 无需动态添加Stores，默认情况下它们都是动态的，您甚至都不会注意到。

- 注意，您仍然可以在需要时使用Store手动注册，但因为它是自动的，所以您无需担心后续。

- 不再有模块的嵌套结构。您仍然可以通过在另一个store中引入和使用store来隐式嵌套store，但是Pinia在设计上提供了一个扁平的结构，同时仍然支持stores之间的交叉组合方式。你甚至可以有store的循环依赖关系。

- 没有模块的命名空间。鉴于stores的扁平架构，“命名空间”的store与它们的定义方式是固有的，您可以说所有store都有命名空间的。






vuex 的状态流: action -> mutation -> 状态

pinia 有点
- 没有 mutation
- 体积 小
- 支持 devtool
- 支持 vue2 中的辅助函数 mapGetters






## 安装引入
```js
// 安装
npm install pinia
```
```js
// main.ts 引入
import {createPinia} from 'pinia'          //main.js导入
createApp(App).use(createPinia()).mount('#app')  //createPinia()得加上括号
```


## 声明和访问 state
<a href="https://baimingxuan.net/pinia-doc-cn/core/defining-store.html#%E4%BD%BF%E7%94%A8store">原文链接</a>
<br>
是使用defineStore()定义的，需要一个唯一的名称，作为第一个参数传递；是必需的，Pania使用它来将store连接到devtools; 

该函数接收两个参数：
name：一个字符串，必传项，该store的唯一id。
options：一个对象，store的配置项，比如配置store内的数据，修改数据的方法等等。

```js
import { defineStore } from 'pinia'

// useStore could be anything like useUser, useCart
// the first argument is a unique id of the store across your application
export const useStore = defineStore('main', {
  // other options...
})
```


### 一：直接 return 对象
```js

// store/index.ts
export const UserInfo = defineStore("user", {
  // 生命state
  state: () => {
    return {
      name: "joe",
      age: 34
    }
  }
  // 
})

// view/home.vue
import { UserInfo } from "../store/index"

const userInfo = UserInfo(); // 记得是方法，需要（）。就可以使用了
console.log("user", UserInfo);
```


### 二：storeToRefs 将数据转化成响应式的

```js

// store/index.ts
export const UserInfo = defineStore("user", {
  // 生命state
  state: () => ({
    name: "joe",
    age: 34
  })
  // 
})

// view/home.vue

import { storeToRefs } from 'pinia';
import { UserInfo } from "../store/index"

const { name, age } = storeToRefs(UserInfo()); // 记得是方法，需要（）。就可以使用了
console.log("user", UserInfo);

```

## getters 使用
1. 获取自己 state 的值
2. 使用自己 getters 的函数返回值
3. 使用别的 getters 的函数返回值
4. 如何给 getters 传参数


```js

// store/index.ts

  getters: {
    /**
     * 返回 state
     */
    doubleAge(state) {
      return state.age * 2 // 必须要写 return
    },
    /**
     * 使用已有的 getters
     */
    doubleAgePlus() {
      return this.doubleAge + 1;
    },
    /**
     * 给 getters 传参数进来
     */
    doubleAgeParams(state) {
      return (num: number) => {
        return num + state.age
      };
    },
    /**
     * 使用 main 里面的 state
     */
    userMainInfo(state) {
      const main = MainInfo()
      return main.count + state.age;
    }
  }


// view/home.vue  script 
// 直接解构出来
const { name, age, doubleAge } = storeToRefs(UserInfo()); 

// html 就可以使用
<H4>age: {{age}} - doubleAge: {{doubleAge}}</H4>

```




## action 使用
1. action 同步修改 state 的值（同步）
2. action 通过传参数，修改 state 的值（同步）
3. action 支持异步任务

```js

/**
 * action 异步任务
 */
addCount(num: number){
  // 1. action 可以通过 this 直接使用 state 的值
  return this.count 

  // 2. action 可以传参数进来使用
  return this.count += num

  // 3. action 支持异步方法，改变 state 的值
  setTimeout(() => {
    return this.count += num
  }, 2000)
}

```