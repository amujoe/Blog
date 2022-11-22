# 初识 Pinia


官网地址 [点击查看](https://pinia.vuejs.org/)

一个中文手册 [点击查看](https://baimingxuan.net/pinia-doc-cn/guide/introduction.html#%E4%BB%8B%E7%BB%8D)

另一个中文手册 [点击查看](https://pinia.web3doc.top/introduction.html)

眼花缭乱？再给你看看官方的中文手册 [拿走不谢](https://pinia.vuejs.org/zh/introduction.html)

******

Pinia 起始于 2019 年 11 月左右的一次实验，其目的是设计一个拥有组合式 API 的 Vue 状态管理库。从那时起，我们就倾向于同时支持 Vue 2 和 Vue 3，并且不强制要求开发者使用组合式 API，我们的初心至今没有改变。除了安装和 SSR 两章之外，其余章节中提到的 API 均支持 Vue 2 和 Vue 3。虽然本文档主要是面向 Vue 3 的用户，但在必要时会标注出 Vue 2 的内容，因此 Vue 2 和 Vue 3 的用户都可以阅读本文档。[盗窃于此](https://pinia.vuejs.org/zh/introduction.html)

******

- 从前有一座山，山上有一座庙，庙里有一篇文章叫：目录
  - [为什么叫它 pinia - 菠萝](#为什么叫它Pinia-菠萝)
  - [对比vuex](#对比vuex)
  - [如何安装、引入](#如何安装、引入)
  - [定义Store](#定义Store)
  - [定义State](#定义State)
  - [使用Getter](#使用Getter)
  - [使用Action](#使用Action)

****** 

## 为什么叫它Pinia-菠萝

Pinia(发音为/piːnjʌ/，就像英语中的“peenya”)是最接近piña(西班牙语中的 “菠萝pineapple”)的一个有效的包名。事实上，菠萝是一群单独的花朵结合在一起，形成了多个果实的一种水果。与Stores类似，每个store都是独立生成的，但他们最终都是连接在一起的。菠萝也是一种原产于南美洲的美味热带水果。



## 对比vuex
[看官方文档，得真经](https://pinia.vuejs.org/zh/introduction.html#comparison-with-vuex)



以下是大叔收集的 Pinia 优点，双手奉上：
- Options-API 与 Composition——API 都支持。 - *问题来了，什么是 Options-API、Composition——API ？* [心细如我，点击来看](/share/share03)
- 没有 mutations - *vuex 的状态流: actions -> mutations -> 状态*
- 没有嵌套 - *Pinia 从设计上提供的是一个扁平的结构*
- 支持 TS   -   *天生的，就是傲娇*

- 支持 vue2 中的辅助函数 mapGetters


## 如何安装、引入
官方不一定是最好的，但一定是求生欲最强的。不接受反驳，[不信点进来看](https://pinia.vuejs.org/zh/getting-started.html#installation)

这里有一段意味深长的话：
> 应该在什么时候使用 Store?
>
> 一个 Store 应该包含可以在整个应用中访问的数据。这包括在许多地方使用的数据，例如显示在导航栏中的用户信息，以及需要通过页面保存的数据，例如一个非常复杂的多步骤表单。
>
>另一方面，你应该避免在 Store 中引入那些原本可以在组件中保存的本地数据，例如，一个元素在页面中的可见性。
>
>并非所有的应用都需要访问全局状态，但如果你的应用确实需要一个全局状态，那 Pinia 将使你的开发过程更轻松。


## 定义Store
<a href="https://pinia.vuejs.org/zh/core-concepts/">原文链接</a>
<br>
<br>
Store 是使用 `defineStore()` 定义的，该函数接收两个参数：
<br>
name：一个字符串，必传项，是该 store 的唯一 id。 Pania 使用它来将 store 连接到 devtools; 
<br>
options：一个对象，store的配置项，比如配置store内的数据，修改数据的方法等等。

```js
import { defineStore } from 'pinia'

// useStore could be anything like useUser, useCart
// the first argument is a unique id of the store across your application
export const useStore = defineStore('main', {
  // other options...
})
```

上面说的 Options-API 与 Composition——API 都支持，就在此时用，[上链接](https://pinia.vuejs.org/zh/core-concepts/#option-stores)

## 定义State
`State`是`Store`的数据
<br>
定义`State`有的两种方式: `() => {}` 与 `() => ({})`; 你懂的，问题又来了！ 两种方式区别在哪？[答案自取](/share/share06.md)

```js
/**
 * state 有两种定义方式
 * 一种是：() => { return XXX }
 * 另一种：() => ({})
 *  */ 

// store/index.ts
export const UserInfo = defineStore("user", {
  // 生命state
  // state: () => {
  //   return {
  //     name: "joe",
  //     age: 34
  //   }
  // }
  // 生命state
  state: () => ({
    name: "joe",
    age: 34
  })
})
```

`State` 的使用:

分为 `访问`、`重置`、`变更`、`替换` ，根据[官网](https://pinia.vuejs.org/zh/core-concepts/state.html#accessing-the-state)详细拆解



## 使用Getter

`Getter`是`Store`的计算属性

主要是学习四个点：
1. 如何获取 state 的值
2. 如何使用其他 getter
3. 如何使用别的 store 的 getter
4. 如何给 getter 传参数

以下是一个实践的 demo。 当然
```js
// store/user.ts
import { MainInfo } from "./main"

  getters: {
    /**
     * 1.如何获取 state 的值
     * 答：参数默认为 state
     */
    doubleAge(state) {
      return state.age * 2 // 必须要写 return
    },
    /**
     * 2. 如何使用其他 getter
     * 答：可以用 this 访问到整个 store 实例，通过 this 可以点出来所有 getter
     */
    doubleAgePlus() {
      return this.doubleAge + 1;
    },
    /**
     * 
     * 3. 如何使用别的 store 的 getter
     * 答：想要使用另一个 store 的 getter 的话，那就直接在 getter 内使用就好：
     */
    userMainInfo(state) {
      const main = MainInfo()
      return main.count + state.age;
    }
    /**
     * 4. 如何给 getter 传参数
     * 答：Getter 只是幕后的计算属性，所以不可以向它们传递任何参数。不过，你可以从 getter 返回一个函数，该函数可以接受任意参数：
     */
    doubleAgeParams(state) {
      return (num: number) => {
        return num + state.age
      };
    },
  }

```

## 使用Action
`Action`是`Store`的方法

主要是学习四个点：

1. action 支持传参
2. action 支持异步任务
3. action 可以调用别的 store 里的 action

```js
// store/user.ts
import { MainInfo } from "./main"

  actions: {
    /**
     * 最简单的调用
     */
    addAge() {
      // action 可以通过 this 直接使用 state 的值
      this.age ++
    },
    /**
     * 1.action 支持传参
     */
    addAgeNum(num: number) {
      this.age += num
    },
    /**
     * 2.action 支持异步任务
     */
    addAgeAsync(num:number) {
      setTimeout(() => {
        this.age += num
        }, 2000)
    },
    /**
     * 3.action 可以调用别的 store 里的 action
     */
    useMainAction() {
      const main = MainInfo();
      main.addCount(1)
    }
  }

```

******
## 总结一下

`State`是`Store`的数据，<br>
`Getter`是`Store`的计算属性，<br>
`Action`是`Store`的方法；<br>
这个你理解了，剩下的就很简单


最后，学习的代码链接在此，[双手奉上](https://github.com/amujoe/learn-pinia.git)

