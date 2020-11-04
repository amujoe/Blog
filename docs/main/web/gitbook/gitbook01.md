

#### gitbook 
#### 一个让你轻轻松松搭建电子书的工具

### 初始化



### 插件

 plugins

 在book.json中添加"plugins"和"pluginConfig"字段。

- plugins 配置插件
- pluginConfig 配置插件的属性

 其中"-search"中的 - 符号代表去除默认自带的插件
 Gitbook默认自带有5个插件：

* highlight： 代码高亮
* search： 导航栏查询功能（不支持中文）
* sharing：右上角分享功能
* font-settings：字体设置（最上方的"A"符号）
* livereload：为GitBook实时重新加载


#### back-to-top-button 回到顶部

在book.json中添加以下内容。然后执行gitbook install，或者使用NPM安装npm install gitbook-plugin-chapter-fold，也可以从源码GitHub地址中下载，放到node_modules文件夹里（GitHub地址在进入插件地址右侧的GitHub链接）


####

#### chapter-fold 导航目录折叠
注意: 想要折叠目录, summary.md 必须如下

#### code 代码添加行号&复制按钮
#### copy-code-button 代码复制按钮
#### github 在右上角添加github图标

```
{
    "plugins": [ 
        "github" 
    ],
    "pluginsConfig": {
        "github": {
            "url": "https://github.com/zhangjikai"
        }
    }
}
```

####   splitter 侧边栏宽度可调节

```
{
    "plugins": [
        "splitter"
    ]
}
```
示例:
![avatar](https://upload-images.jianshu.io/upload_images/14946112-b396ef55e6cf299b.gif)



#### tbfed-pagefooter 页面添加页脚（简单的）

```
{
    "plugins": [
       "tbfed-pagefooter"
    ],
    "pluginsConfig": {
        "tbfed-pagefooter": {
            "copyright":"Copyright &copy xxxx.com 2017",
            "modify_label": "该文件修订时间：",
            "modify_format": "YYYY-MM-DD HH:mm:ss"
        }
    }
}
```





#### expandable-chapters 
####
