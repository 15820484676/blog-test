# HTML常用标签

## a标签
```html
<a href="" target=""></a>
```
### a标签的href属性
网址：

https://google.com  
http://google.com  
//google.com 最好用这种，他会自动重定向到正确的地址  

路径：  
如果写的是路径/a/b/c，那么以当前开启的服务的目录为根目录

伪协议：  
主要用来执行一段javascript代码  
```html
<a href="javascript:alert(11111111111);">这是javascript方式</a>
<a href="javascript:;">这是点击a标签没反应</a>这种是用来实现一些特殊的需求
<a href="javascript:alert(11111111111);">这是javascript方式</a>
<a href="javascript:;">这是点击a标签没反应</a>
<a href="#p1">这是锚点的作用</a>
<a href="mailto:1044045168@qq.com">这是发送邮件</a>
<a href="tel:15820484676">这是打电话</a>
```
### a的target属性  
_blank:新建一个页面打开  
_top: 有多个iframe时，再顶级窗口打开页面  
_parent: 在当前连接上一层页面打开  
_self:在当前页面打开，默认就是self  
target = "xxx"时，打开的窗口就是xxx window.name也可以看到   
iframe现在几乎不用了  

## table标签 表格标签
如果不写tbody浏览器会默认加上tbody
thead
tbody
tfoot
三个顺序写错了浏览器会纠正
th 表示表头
tr 表示一行
td 表格数据


## img标签 图片标签
会发出一个get请求，展示一张图片  
属性：  
src 图片地址  
alt 图片加载失败时展示的字  
width height 如果同时用了会让图片变形，一般只写一个  
事件：  
onload:加载成功时执行  
onerror:加载失败时执行  

img{max-width : 100%}这样会让图片变响应式的 


## form标签 表单标签
会发送get或post请求，刷新页面  
要有一个type="submit"的提交按钮  
input 和 button 提交的区别：input不能有其它标签,button可以有其它的标签  

属性：  
action: 请求地址  
method:请求方式；GET  POST  
autocomplete:自动填充 off on   
target:提交到哪个页面刷新  

事件：
onsubmit 触发提交动作

## 其它感想
标签很多，主要用的就那些，不会的可以查看文档，mdn 标签 
