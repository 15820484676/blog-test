## webpack是干嘛的？
* 转译代码 把ES6转为ES5,SCSS转为CSS
* 构建
* 代码压缩
* 代码分析

### 安装webpack
```javascript
//本地安装webpack
yarn add webpack@4 webpack-cli@3 --dev

//本地安装的可以在目录下使用命令
./node_modules/.bin/webpack

//也可以使用npx webpack运行，如果不能用就用上面那种
运行后会在目录下生成dict目录，里面会有main.js文件，文件里面就是自己写的js被转译后的代码
```
### 解决warning
新建一个webpack.config.js,在里面写如下配置
```javascript
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './foo.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'foo.bundle.js',
    
  },
};
//mode用来切换开发模式的，也可以设置成production,设置后转译的代码里面就没有注释介绍，是生产用的
```

### 理解文件的hash的用途（配置文件）
* entry: 入口，用来设置需要转译的js文件
* output：出口，用来设置转译后保存的文件
* filename : '[name].[contenthash].js'，使用这个设置后，编译后的文件名由hash串组成
* 可以在package.json里面加上如下代码,然后直接执行yarn build就行了
```json
{
	"scripts":{
		"build":"rm -rf dist && webpack"
	},
  "devDependencies": {
    "webpack": "4",
    "webpack-cli": "3"
  }
}
```
### HTTP缓存
* 浏览器加载某个页面的时候，页面有许多配套的js，css之类的，如果每次都重新从服务器获取会很耗费时间，那么就由服务器返回一个响应头Cache-Control,设置缓存时间，那么下次加载页面的时候，请求的文件名还是没变的话，就不需要请求服务器了，直接从本地磁盘读取，就变得很快。
* 首页不能做缓存，因为要获取更新的js css文件


### 编译HTML
```javascript
var HtmlWebpackPlugin = require('html-webpack-plugin')
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './foo.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'foo.bundle.js',
  },
  plugins:[new HtmlWebpackPlugin({
      title:'My App',//可以在模板文件里面使用<%= htmlWebpackPlugin.options.title %>来引用这个title
      filename: 'assets/admin.html',//生成的文件名
      template: 'src/assets/index.html'//用这个模板来生成html
  })]
};

```
* yarn build 如果报错了，应该是html-webpack-plugin的版本不对，安装对应的版本即可
### 编译CSS
```javascript
var HtmlWebpackPlugin = require('html-webpack-plugin')
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    filename: '[name].[contenthash].js',
  },
  plugins:[new HtmlWebpackPlugin(
	  {
      title:'My App',
      template: 'src/assets/index.html'
  }
  )],
  module: {
    rules: [
      { test: /\.css$/, use: ['style-loader','css-loader'] },//css-loader的作用是把css内容读到js里面，style-loader的作用是把css-loader读到的东西放到style标签里面

    ],
  },
};
```

### 使用两个config文件


### loader和plugin
* webpack通过babel-loader把js转译成宁外一个js文件
* webpack通过html-webpack-plugin把0个或多个html放在一个html文件里面 
* webpack通过style-loader和css-loader把css放在一个style标签里面
* webpack通过MiniCssExtractPlugin把多个css放在一个css文件里面
* loader是一个文件对应一个文件
* plugin是把多个文件合并到一个文件

解释+举例:
> loader是加载器用来加载各种资源文件的，plugin是插件，用来扩展webpack功能的。  
> 比如babel-loader是用来加载js的，它可以把js变成低版本浏览器支持的js,css-loader和 style-loader是用来加载css的，可以把它变成页面中的style标签。
> html-webpack-plugin plugin是用来生成html文件的，MiniCssExtractPlugin是用来抽取css代码，把它变成一个css文件的

### 引入scss/less/stylus  高级css
* 三个没什么区别
* 要先安装sass-loader、less-loader、less、stylus、stylus-loader和dart-sass
```javascript
 module: {
          rules: [
            //普通css需要的loader
            { test: /\.css$/, use: ["style-loader", "css-loader"] },
            //scss需要的loader
            {
              test: /\.scss$/,
              use: [
                "style-loader",
                "css-loader",
                {
                  loader: "sass-loader",
                  options: { implementation: require("dart-sass") },
                },
              ],
            },
            //less需要的loader
            {test: /\.less$/,use:["style-loader","css-loader","less-loader"]},
            //stylus需要的loader
            {test: /\.styl$/,use:["style-loader","css-loader","stylus-loader"]}
          ],
        }
```

### 引入图片

* 先安装file-loader,它的作用是把文件变成文件路径
```javascript
import css from './test.css'
import './test.scss'
import './test.less'
import './test.styl'
//png只是一个路径，这是loader决定的
import png from './yl.png'


const div = document.getElementById('app')
div.innerHTML = ` <img src="${png}" alt="">`

 module: {
          rules: [
            //普通css需要的loader
            { test: /\.css$/, use: ["style-loader", "css-loader"] },
            //scss需要的loader
            {
              test: /\.scss$/,
              use: [
                "style-loader",
                "css-loader",
                {
                  loader: "sass-loader",
                  options: { implementation: require("dart-sass") },
                },
              ],
            },
            //less需要的loader
            {test: /\.less$/,use:["style-loader","css-loader","less-loader"]},
            //stylus需要的loader
            {test: /\.styl$/,use:["style-loader","css-loader","stylus-loader"]},
            //图片需要的loader,
            {test: /\.(png|gif|svg|jpg)$/,use:["file-loader"]}
          ],
        }
```
### 懒加载

```javascript
const button = document.createElement("button");
      button.innerText = "懒加载";
      document.body.appendChild(button);
      button.onclick = (params) => {
        const promise = import("./lazy.js");
        promise.then(
          (module) => {
            const fn = module.default;
            fn();
          },
          () => {
            console.log("懒加载出错了");
          }
        );
      };
```
### 部署git/gitee
这是git的一个问题解决：[这是链接](https://blog.csdn.net/weixin_42436131/article/details/100043976)