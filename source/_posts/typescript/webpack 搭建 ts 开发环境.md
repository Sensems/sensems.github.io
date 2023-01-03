---
title: webpack 创建简单的 ts 开发环境
date: 2022/3/5 16:55:46
cover: https://s2.loli.net/2023/01/03/yaCgTcBLzJk1672.png
categories:
  - TypeScript
tags:
  - TypeScript
  - 环境搭建
  - webpack
---

# webpack 创建简单的 ts 开发环境

## 前置要求

需要的的 `npm` 插件

>
> 1. webpack ( webpack 本体 )
> 2. webpack-cli ( webpack 的命令行工具 )
> 3. typescript ( typescript 核心代码 )
> 4. ts-loader (typescript 的 webpck 编译模块)
> 5. clean-webpack-plugin ( 打包前清除之前打包的文件夹 )
>



## ts 开发环境目录
![Snipaste_2022-03-05_15-32-16.png](https://s2.loli.net/2023/01/03/XS1lVDEMyifWocg.png)

## tsconfig.json 配置

```json
  {
    "compilerOptions": {

      "module": "ES6",             // 使用的模块规则

      "target": "ES6",             // 编译生成 js 的版本

      "noImplicitAny": true,       // 不允许隐式的 any 类型

      "removeComments": true,      // 删除注释

      "preserveConstEnums": true,  // 保留 const 和 enum 声明

      "strict": true               // 使用严格模式
    },

    // 需要编译的 ts 文件
    "include": [
      "./src/**/*"
    ]
  }
```

## webpack.config.js 配置

### 基本配置

```javascript
  const path = require("path")
  const { CleanWebpackPlugin } = require("clean-webpack-plugin")

  module.exports = {
    // 入口文件
    entry: "./src/index.ts",

    // 打包后的出口文件
    output: {
      // 文件路径
      path: path.resolve(__dirname, "dist"),

      // 文件名
      filename: "bundle.js",
    },
    // 使用的编译模块
    module: {

      // 指定要加载的规则
      rules: [
        {
          // test 是指定规则生效的文件(既对那些文件进行编译), 使用的是正则
          test: /\.ts$/,

          // 要使用的 loader
          use: ['ts-loader'],

          // 排除要编译的文件夹
          exclude: /node_modules/
        }
      ]
    },

    // 用来设置需要引用的模块文件 (这里包括了 ts 和 js) 不设置的话, 引用其他 ts/js 文件会编译报错
    resolve: {
      extensions: ['.ts', '.js']
    },

    // 配置 webpack 插件
    plugins: [
      new CleanWebpackPlugin()
    ],
  }
```

### 使用 html 文件配置

> 前端项目中我们编译完的 js 文件最终会用到 html 文件中. 我们手动创建并引入 js 的话也不是不行, 但是很麻烦, 如果以后要增加一些其他的 js 或者 css 都得重新去手动引入. 这时候就可以用 `webpack` 给我们提供的一个自动引入经过 loader 编译后的文件 html 的插件 `html-webpack-plugin`
>
> `**_npm install -D html-webpack-plugin_**`


在最外层的 `plugins` 中配置

[更多 html-webpack-plugin 的配置信息看这里](https://github.com/jantimon/html-webpack-plugin#configuration)

```javascript
  // 引入插件
  const HtmlWebpackPlugin = require("html-webpack-plugin")

  module.exprots = {
    // 配置 webpack 插件
    plugins: [
      new HtmlWebpackPlugin({
        // 配置 html 模板文件的目录
        template: path.resolve(__dirname, 'public/index.html')
      })
    ],
  }
```

### 使用 webpack-server 实时编译

> 弄好 `html` 自动引入后我们需要打开网页去调试我们的 ts 程序, 按照普通方式来修改一次又要打包一遍, 又要重新刷新一遍网页的话就很麻烦, 这时我们可以用 `webpack-server` 来进行开发服务器部署
>
> `**_npm install -D webpack-server_**`
>
> 安装完后直接在 `package.json` 中进行配置运行命令运行就行了


```json
  {
    "scripts": {
      "dev": "webpack server --mode development"
    }
  }
```

### 配置 babel 来进行浏览器兼容

在日常的开发中我们会经常遇到要兼容低版本浏览器的需要, 这时候为了增加开发效率我们可以用 `**_babel_**` 来将一些 `**_ES6_**` 中的高级属性来转换为低版本浏览器中的兼容属性

需要的开发依赖

>
> 1. @babel/core ( babel 的核心代码 )
> 2. @babel/preset-env ( babel 的兼容库 )
> 3. core-js ( 高级属性的兼容性替代方案 )
>

> `**_npm install -D @babel/core @babel/preset-env core-js_**`


webpack 配置

```javascript

  module.exports = {

    // 使用的编译模块
    module: {
      // 指定要加载的规则
      rules: [
        {
          // test 是指定规则生效的文件(既对那些文件进行编译), 使用的是正则
          test: /\.ts$/,

          // 要使用的 loader
          use: [

            // 配置 babel
            {
              // 指定要用的加载器
              loader: 'babel-loader',

              options: {
                // 设置预定义的环境
                presets: [
                  [
                    "@babel-preset-env",

                    {
                      // 需要兼容的目标浏览器, 根据项目需求填写
                      targets: {
                        "chrome": 95
                      },

                      // 指定的 core 版本
                      "corejs": '3',

                      // 使用 corejs 的方式 "usage" 按需加载
                      "useBuiltIns": "usage"
                    }
                  ]
                ]
              }
            },

            // 由于 webpack 中 rules 是从数组从后往前执行的, 所以 ts-loader 放在后面, 让 ts 先编译为 js 在通过 babel 进行兼容性转换
            'ts-loader'
          ],
        }
      ]
    }
  }
```
