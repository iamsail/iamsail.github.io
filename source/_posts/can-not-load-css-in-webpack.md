---
title: webpack加载不了样式
date: 2017-05-17 00:08:30
categories: webpack
---

今天碰到一个问题,花费了很久的时间,最后在[肖神](https://blog.xgy666.cn/)和[garychang](http://garychang.cn/)的帮助下解决了。

** 问题是打开localhost:8080没有加载出样式 **

***************************

因为我的项目目录结构不对,也就是index.html放的位置不对。

当然这只是表象。

以下面这个目录结构为例子进行讲解

**********************

### ** 项目目录结构 **

```
online-talk
        app
            config.json
            main.css
            main.js
            Greeter.js

        node_modules
             略

        public
            bundle.js
            index.html

        package.json

        postcss.config.js

        webpack.config.js

```
***********************

可以看到public/index.html

```

 <!doctype html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <title>online-talk</title>
            </head>
            <body>
            <!--<div id='root'>-->
            <!--</div>-->
            <script src="bundle.js"></script>
            </body>
            </html>

```

通过public/index.html来加载bundle.js

*************************

其实默认情况下index.html是需要放在项目根目录下的,也就是<code>online-talk</code>

那如何让index.html在public下呢

** 需要在devserver中设置<code>contentBase: "./public"</code> **

devserver作为webpack配置选项中的一项，具有以下配置选项

<code>contentBase</code>

** 默认webpack-dev-server会为根文件夹提供本地服务器，如果想为另外一个目录下的文件提供本地服务器，应该在这里设置其所在目录（本例设置到“public"目录）**

<code>port</code>

设置默认监听端口，如果省略，默认为”8080“

<code>inline</code>

设置为true，当源文件改变时会自动刷新页面

<code>colors</code>

设置为true，使终端输出的文件为彩色的

<code>historyApiFallback</code>

在开发单页应用时非常有用，它依赖于HTML5 history API，如果设置为true，所有的跳转将指向index.html


**************************

然而仅仅是设置** <code>contentBase: "./public"</code> **,执行<code>npm start</code>,依然没有样式

** 因为启动脚本中也需要配置目录 **
** 因为启动脚本中也需要配置目录 **
** 因为启动脚本中也需要配置目录 **

    "scripts": {
        "start": "webpack-dev-server --inline --content-base public/ --history-api-fallback"
      },

**************************

最后附上配置文件,也算是备份

#### ** webpack.config.js **

```

    var path = require('path');
    var webpack = require('webpack');
    var autoprefixer = require('autoprefixer');

    module.exports = {
        devtool: 'eval-source-map',//配置生成Source Maps,选择合适的选项
        entry:  __dirname + "/app/main.js",//已多次提及的唯一入口文件
        output: {
            path: __dirname + "/public",//打包后的文件存放的地方
            filename: "bundle.js"//打包后输出文件的文件名
        },

        module: {//在配置文件里添加JSON loader
            loaders: [
                {
                    test: /\.json$/,
                    loader: "json-loader"
                },
                {
                    test: /\.js$/,
                    exclude: /node_modules/,
                    loader: "babel-loader",
                    query: {
                        presets: ['es2015']
                    }
                },
                {
                    test: /\.css$/,
                    loader: 'style-loader!css-loader!postcss-loader'//添加对样式表的处理
                    //loader: ['style-loader','css-loader','postcss-loader']//添加对样式表的处理
                }
            ]
        },

        plugins: [
            new webpack.LoaderOptionsPlugin({
                options: {
                    postcss: function () {
                        return [precss, autoprefixer];
                    },
                    devServer: {
                        contentBase: "./public", //本地服务器所加载的页面所在的目录
                        port: "8080",
                        colors: true, //终端中输出结果为彩色
                        historyApiFallback: true, //不跳转
                        inline: true //实时刷新
                    }
                }
            })
        ]
    }
```

#### ** package.json **

```

    {
      "name": "online-talk",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": {
        "start": "webpack-dev-server --inline --content-base public/ --history-api-fallback"
      },
      "author": "",
      "license": "ISC",
      "devDependencies": {
        "autoprefixer": "^7.1.0",
        "babel-core": "^6.24.1",
        "babel-loader": "^7.0.0",
        "babel-preset-es2015": "^6.24.1",
        "css-loader": "^0.28.1",
        "json-loader": "^0.5.4",
        "postcss-loader": "^2.0.5",
        "style-loader": "^0.17.0",
        "webpack": "^2.5.1",
        "webpack-dev-server": "^2.4.5"
      },
      "dependencies": {
        "ws": "^2.3.1"
      }
    }

```

*******************************

#### ** 参考 **

- [关于WEBPACK DEV SERVER](https://segmentfault.com/q/1010000004957130)

