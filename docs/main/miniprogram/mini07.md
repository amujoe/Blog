# 终究还是原生的味道更醇

没有故事，没有背景

### 优点
- 官方文档清晰明了，更接近手机服务的底层逻辑
- 使用原生开发可以紧随官方的版本，更新响应速度快，让项目达到最优状态。

### 划重点
只做单平台的小程序，原生无疑是最优的选择，但如果同时开发多平台小程序，uni-app 是你不错的选择；立马关闭网页，再见，不送；


### 原生开发需要注意什么？

- 目录及分包
- 环境配置
- 接口封装
- 基础方法预制
- 自定义 tabbar
- 预制组件


### 文件目录
目录结构的设计很重要，前期设计好，后期无烦恼；尤其是多人协作，一旦动工，在设计就会走很多弯路； 下面是我们新项目的目录设计

``` js
|- apis               //  接口函数
|- behaviors          // 存放behaviors （mixins）
|- components         // 只存放公共UI组件与业务组件，私有组件放在自己的目录下
|- libs               // 静态文件
|- pages              // 存放 Tabbar 页面及公共基础页面
  |- login            // 基础页面
  |- home             // tabbar 页面
  |- my               // tabbar 页面
|- styles             // 全局样式和原子样式，以及封装后的 css-animation
  |- base.scss
  |- animation //包含动画类
|- subpackages        // 分包组件
  |- other
    |- activity
|- utils              // 存放工具函数
  |- common-login            // 登陆
  |- common-user             // 获取用户信息
  |- common-request          // 接口
  |- date.js          // 时间转换
  |- debounce.js      // 防多触
  |- tips.js          // 提示框
  |- tools.js         // 工具箱（深拷贝，判断是否为空，判断是否相等，找最大值）

```

### 环境配置
小程序原生的缺点就是没有加入环境的配置；现在开发项目，谁还没有几个环境呀！dev环境、test环境、uat环境、最后才是prod环境； 没有个环境配置还真不好用；

自己想到的一个解决方案，先把**文件目录**修改一下；再增加**配置文件** + **配置文件模版**；
```js
|- src
  |- apis
  |- behaviors
  |- components
  |- config
    |- env.js      // 配置文件
  |- ...
|- env.config.js      // 配置文件模版
|- project.config.json
|- project.private.config.json
|- README.md
```

**重点是配置文件模版：env.config.js**；里面做了两件事：
- 一：更改 env.js 里面域名信息
- 二：更新 project.config.json 里面 appid 信息

具体见下面代码：
```js
const fs = require('fs'); // 引入nodejs fs文件模块
// 写文件
const writeFile = (path, data) => {
  // process.cwd()方法是流程模块的内置应用程序编程接口，用于获取node.js流程的当前工作目录。
  fs.writeFile(`${process.cwd()}${path}`, data, (err) => {
    if (err) throw err;
  });
};
// 配置信息
const CONFIG = {
  // 测试环境
  dev: {
    NODE_ENV: 'develop',
    BASE_URL: 'https://m-test.amujoe.com',
    API_ROOT: '/shop/v1/',
    imgHost: 'https://test-img.amujoe.com/',
    APPID: 'wx6a13c02ba549'
  },
  test: {
    NODE_ENV: 'test',
    BASE_URL: 'https://mufe-test.amujoe.com',
    API_ROOT: '/shop/v1/',
    imgHost: 'https://test-img.amujoe.com/',
    APPID: 'wx6a13c02ba550'
  },
  prod: {
    NODE_ENV: 'prod',
    BASE_URL: 'https://mufe-test.amujoe.com',
    API_ROOT: '/shop/v1/',
    imgHost: 'https://test-img.amujoe.com/',
    APPID: 'wx6a13c02ba551'
  }
};
// 获取命令行参数
const cliArgs = process.argv.splice(2);
const env = cliArgs[0].slice(2);

const item = CONFIG[env];

// 更新env.js
let configString = '';
Object.keys(item).forEach(key => {
  configString += `module.exports.${key} = '${item[key]}';\n`;
});
writeFile('/src/config/env.js', configString);

// 修改project.config.json里面的appid
fs.readFile(`${process.cwd()}/project.config.json`, (err, data) => {
  if (err) throw err;
  const _data = JSON.parse(data.toString());
  _data.appid = item.APPID;
  writeFile('/project.config.json', JSON.stringify(_data, null, 2));
});
```

然后再给 package.json 加上命令行；就可以随意切换咯 `npm run dev`， `npm run test`

```js
"scripts": {
    "dev": "node env.config.js --dev",
    "test": "node env.config.js --test",
    "prod": "node env.config.js --prod",
    ...
},
```

### 接口封装

这里代码有点多，就不复制粘贴了；主要是思想，思想通了，不论是管理后台还是小程序，都能轻松拿下；

需要完成的点：
- 把业务接口全部统一管理在 apis
- 接口封装在 common-request.js 里
- 登录、获取用户信息等调用频繁的接口，需要做公告处理
- 配置 header 头的 token；token 失效后需要重新登录；
- 全局处理 loading
- 统一处理报错
- 超时后，重复请求 3 次

具体代码实现，条条道路通罗马，如果真遇到没路可走，那就联系我吧，欢迎一起讨论学习

### 基础方法预制


