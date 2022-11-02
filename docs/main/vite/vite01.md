
## vite 搭建基础流程

Vite 需要 Node.js 版本 14.18+，16+。然而，有些模板需要依赖更高的 Node 版本才能正常运行，当你的包管理器发出警告时，请注意升级你的 Node 版本

### 安装 vite 
```js
// 安装最新的 vite

// npm
$ npm create vite@latest

// yarn
$ yarn create vite

// pnpm
$ pnpm create vite
```

### 构建一个 Vite + Vue 项目：
```sh
# npm 6.x
npm create vite@latest my-vue-app --template vue
npm create vite@latest my-vue-app --template vue-ts

# npm 7+, extra double-dash is needed:
npm create vite@latest my-vue-app -- --template vue

# yarn
yarn create vite my-vue-app --template vue

# pnpm
pnpm create vite my-vue-app --template vue
```


### 安装依赖，然后跑起来
手甩起，脚抬高，一二一，一二一，一二三  四

```js
// 君莫急，一步一步操作
cd my-vue-app
npm install
npm run dev
```


## vue-router 
### 安装 router

```js
// npm
npm install vue-router@4

// yarn
yarn add vue-router@4
```

### 配置 router
第一步： 路由文件 /router/index.ts
```js
// 路由文件
import { createRouter, createWebHistory } from "vue-router";

import Home from '@/views/Home.vue'
import About from '@/views/About.vue'

const routes = [
    {
        path: '/',
        name: 'Home',
        component: Home
    },
    {
        path: '/a',
        name: 'Home',
        component: Home
    },
    {
        path: '/b',
        name: 'About',
        component: About
    }
]

const router = createRouter({
    history: createWebHistory(),
    routes
})

router.beforeEach((to,from)=>{
   console.log("beforeEach -to", to, from)
})

router.afterEach((to,from)=>{
   console.log("afterEach -to", to, from)
})

export default router;

```

第二步：main.ts 注入

```js

import { createApp } from 'vue'
import './style.css'
import App from './App.vue'
import Router from './router/index.js'

const app = createApp(App)
app.use(Router)
app.mount('#app')

```

是不是报错了？ @/views/Home.vue 不存在？ 那是没有新建文件呀！

...此处忽略新建文件夹的过程...

什么？新建了页面也报错？ 那是因为没有配置路径别名，继续往下看


## alias @
配置路径别名
### 1.安装依赖
```js
npm install @types/node -D
```
### 2. 在 vite.config.ts 中增加配置

```js

import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import { resolve } from 'path'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: {
      '@': resolve(__dirname, './src')
    }
  }
})
```

### 3. 配置 tsconfig.json
```js
{
  "compilerOptions": {
    ...
    "baseUrl": "./",
    "paths": {
	    "@/*": ["src/*"]
    }
  }
}
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