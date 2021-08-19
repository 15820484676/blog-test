## MVC
* MVC是一个设计模式，可以使用MVC来优化代码结构
* 每个模块可以写成三个对象，分别是M V C
* M-Model 数据模型，负责操作所有的数据
* V-View  视图 负责所有的UI界面
* C-Controller 控制器 负责其他的东西

## css js引入
```javascript
import './index.css'
import $ from 'jquery'
```
* import可以自动找到node_modules目录里面下载的js库
* 首先得执行yarn init 和 yarn add jquery 然后就可以在项目中引用jquery了
* package.json里面保存的是项目下载的js库信息
* yarn.lock里面保存的是js库下载的地址信息
* 滚动条的宽度大概是 14-19px

## 样式与行为分离
* 用js给元素添加或修改class，不要用js去操作css

## 抽象思维
### 最小知识原则
* 引入一个模块只需要引入一个js就行了
* js里面包含了html,js里面也引入了需要的css
* 但是这样会在开始的时候页面是空白的，解决方法：可以加上loading动画 、骨架、占位内容。还可以使用SSR技术，比较复杂

### 以不变应万变


### 解耦
* 当多个模块依赖同一个模块的时候，可以在他们中间加一个中间层，让中间层去调用底层模块，其它多个模块去调用中间层
* dom也是把EventBus放在顶层，一层一层继承下来的，所以所有元素都可以绑定监听事件

### EventBus

### 路由
* 相当于一个指路的人