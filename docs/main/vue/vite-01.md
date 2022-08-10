
# vite


### 官网




## 开始

### 着重强调
```js
Vite 需要 Node.js 版本 >= 12.0.0。
```

### 安装
```
npm create vite@latest

- vanilla：Vanilla JS 是一个快速、轻量级、跨平台的JavaScript框架。
- vue/react：这两个应该不用过多介绍了吧。
- preact：React 的轻量级替代方案。
- lit：Lit 是一个简单的库，用于构建快速、轻量级的 Web 组件。（看了一眼语法，感觉还挺好玩的。）
- svelte：一个不使用 Virtual DOM 的库 —— 真酷。这个库的作者和 Rollup 的作者是同一人。


```


### 依赖
```js
// 这个应该不用说的
npm install
```

### 运行
```js
// 运行
npm run dev
```


## vue-router
### 安装
```
npm install vue-router@4
```
添加完路由依赖以后需要**手动**在src目录下创建一个 router 文件夹，以及在router文件夹内创建一个它的配置文件——index.js，下面是index.js文件内容
``` js
// 路由文件
import { createRouter, createWebHistory } from "vue-router";

import Home from '../views/Home.vue'

const routes = [
    {
        path: '/',
        name: 'Home',
        component: Home
    }
]

const router = createRouter({
    history: createWebHistory(),
    routes
})


router.beforeEach((to,from)=>{
    // if(to.meta.requireAuth) {
    //     let token = localStorage.getItem('auth-system-token');
    //     let isLogin = localStorage.getItem('auth-system-login');
    //     if(!token||!isLogin){
    //         return {
    //             path: '/login'
    //         }
    //     }
    // }
})

export default router;

```

需要注意的是在最新的Vue Router中创建路由和使用历史模式的方法都发生了改变，其余使用方式大致相同。

### 使用
引入的useRoute,useRouter 相当于vue2的 this.$route()，this.$router()

push方法是useRouter()才有的
```js
import { useRouter } from 'vue-router'
const route = useRouter();

// 跳转
const goHomePage = (() => {
    route.push({
        name: "Home"
    })
})
```



## script-setup

在 script-setup 模式下，只需要导入组件即可，编译器会自动识别并启用
在 script-setup 模式下，变量你定义了就可以直接使用
但在 script-setup 模式下，所有数据只是默认隐式 return 给 template 使用，不会暴露到组件外，所以父组件是无法直接通过挂载 ref 变量获取子组件的数据。
在 script-setup 模式下，如果要调用子组件的数据，需要先在子组件显示的暴露出来，才能够正确的拿到，这个操作，就是由 defineExpose 来完成。

```js
<!-- 使用 script-setup 格式 -->
<template>
    <p>{{ msg }}</p>
    <Child />
</template>

<script setup lang="ts">
// 组件，引入了直接使用
import Child from '@cp/Child.vue'

// 定义了直接使用
const msg: string = 'Hello World!';

// 显示暴露的数据，才可以在父组件拿到
defineExpose({
  msg
});
</script>
```



## element-plus
### 安装
```
npm install element-plus --save
```

### 方法一：全部引用
main.ts 中引用

```ts
// main.ts
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'

const app = createApp(App)

app.use(ElementPlus)
app.mount('#app')
```

### 方法二：自动引入
首先你需要安装unplugin-vue-components 和 unplugin-auto-import这两款插件。 <a href="https://element-plus.org/zh-CN/guide/quickstart.html#%E6%8C%89%E9%9C%80%E5%AF%BC%E5%85%A5">官方链接</a>
```js
npm install -D unplugin-vue-components unplugin-auto-import
```
然后把下列代码插入到你的 Vite 或 Webpack 的配置文件中

```js
// vite.config.ts
import { defineConfig } from 'vite'
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'

export default defineConfig({
  // ...
  plugins: [
    // ...
    AutoImport({
      resolvers: [ElementPlusResolver()],
    }),
    Components({
      resolvers: [ElementPlusResolver()],
    }),
  ],
})
```

## axios
### 安装
```js
npm install axios
```

### 配置
新建 axios 文件夹，新建 axios.ts
```js
// axios.ts
import axios from 'axios'

//创建axios的一个实例 
var instance = axios.create({
    // baseURL: import.meta.env.VITE_API_ROOT, //接口统一域名
    timeout: 6000, //设置超时
    headers: {
        'Content-Type': 'application/json;charset=UTF-8;',
    }
})


//请求拦截器 
instance.interceptors.request.use((config: any) => {
    // 每次发送请求之前判断是否存在token，如果存在，则统一在http请求的header都加上token，不用每次请求都手动添加了
    const token = window.localStorage.getItem('token');
    token && (config.headers.Authorization = token)
    //若请求方式为post，则将data参数转为JSON字符串
    if (config.method === 'POST') {
        config.data = JSON.stringify(config.data);
    }
    return config;
}, (error) =>
    // 对请求错误做些什么
    Promise.reject(error));

    
//响应拦截器
instance.interceptors.response.use((response) => {
    //响应成功
    console.log('响应成功');
    return response.data;
}, (error) => {
    console.log(error)
    //响应错误
    if (error.response && error.response.status) {
        const status = error.response.status
        console.log(status);
        return Promise.reject(error);
    }
    return Promise.reject(error);
});
export default instance;
```

### 二次封装
在 axios 文件夹，新建 index.ts
```js
import instance from "./axios"

/**
 * 封装的通用方法
 * @param {String} method  请求的方法：get、post、delete、put
 * @param {String} url     请求的url:
 * @param {Object} data    请求的参数
 * @param {Object} config  请求的配置
 * @returns {Promise}     返回一个promise对象，其实就相当于axios请求数据的返回值
 */
const http = async ({
    method,
    url,
    data,
    config
}: any): Promise<any> => {
    method = method.toLowerCase();
    let result = null;
    switch(method) {
        case 'post':
            result = instance.post(url, data, { ...config })
            break;
        case 'get':
            result = instance.get(url, {
                params: data,
                ...config
            })
            break;
        case 'delete':
            result = instance.delete(url, {
                params: data,
                ...config
            })
            break;
        case 'put':
            result = instance.put(url, data, { ...config });
            break;
        default:
            console.error("没有封装对应的请求方式", method);
            break;
    }
    return result;
}
export {
    http
}
```

### 使用
新建 api 文件夹，新建 common.ts 文件
```js
// 这里的引入目录，需要安装你当前的目录引用
import { http } from "../plugins/axios/Index";

export default {
  /** 登录 */
  login(data: any) {
    return http({
      url: "/admin/login",
      method: "post",
      data
    })
  },
  /** 退出登录 */
  logout(data?: any) {
    return http({
      url: "gw-scrm/gw-scrm/admin/logout",
      method: "post",
      data
    })
  },
};

```