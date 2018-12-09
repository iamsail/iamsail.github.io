---
title: 一些webpack相关配置文件
date: 2017-05-16 14:34:17
categories: webpack
---

本文仅为作者记录一些配置文件,不具有教程意义.

** 工具更新太快蛋疼 **

************************

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

### ** 文件内容 **

#### ** postcss.config.js **

```
    module.exports = {};
```

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
                    //loader: 'style-loader!css-loader?modules!postcss-loader'//添加对样式表的处理
                    loader: ['style-loader','css-loader','postcss-loader']//添加对样式表的处理
                },
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
                        colors: true, //终端中输出结果为彩色
                        historyApiFallback: true, //不跳转
                        inline: true //实时刷新
                    }
                }
            })
        ]
    }
```

#### ** public/index.html **

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

#### ** package.json **

```
    {
      "name": "online-talk",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": {
        "start": "webpack"
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
      }
    }
```

#### ** app/config.json **

```
    {
        "greetText": "Hello JSON"
    }
```

#### ** app/main.js **

```
    require('./main.css');//使用require导入css文件
    document.write(12345);
    let config = require('./config.json');
    document.write(config.greetText);
```

#### ** app/main.css **

```
    html {
        box-sizing: border-box;
        -ms-text-size-adjust: 100%;
        -webkit-text-size-adjust: 100%;
    }

    *, *:before, *:after {
        box-sizing: inherit;
    }

    body {
        margin: 0;
        font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
    }

    h1, h2, h3, h4, h5, h6, p, ul {
        margin: 0;
        padding: 0;
    }
```

*************************

#### ** 参考 **

- [webpack2](http://www.css88.com/doc/webpack2/)
- [No PostCSS Config found with build:prod #604](https://github.com/akveo/ng2-admin/issues/604)
- [关于webpack 使用postcss的问题](https://segmentfault.com/q/1010000006987956/a-1020000006995647)
- [入门 Webpack，看这篇就够了](https://segmentfault.com/a/1190000006178770)

