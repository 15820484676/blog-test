## 介绍
* 浏览器把document对象放到window上，js用document来操作网页
* 这就是Document Object Model 文档对象模型（DOM），把网页抽象成一个DOM
* 网页其实是一棵树，标签里面的文字也是一个节点

## dom api
* 如果一个元素有id，可以直接用window.idxxx或直接idxxx（如果有全局属性同名了，就不要用这个了）
* document.getElements 获取的是一个伪数组
* document.querySelectorAll 获取的是一个伪数组
* get系列用来兼容IE，现在用query系列
* document.documentElement 获取html元素
* document.head 获取head元素
* document.body 获取body元素
* window 获取窗口 ，窗口不是元素，但是可以用来监听事件
* document.all 获取所有元素,早期是用来检测是否是IE浏览器， <strong>也是第6个falsy值<strong>
* 获取的元素就是一个对象
## dom对象原型链
* ![avatar](https://static.xiedaimala.com/xdml/file/3ac7c224-c23d-491f-84b5-4fabfbeab9b8/2019-10-17-20-36-26.png)
* 每一层的构造函数都会给dom加上一些东西，六层原型
## 节点 元素 
* 使用x.nodeType得到一个数字
* 1 表示元素Element，也叫标签Tag
* 3 表示文本 Text
* 8 表示注释 Comment
* 9 表示Document 
* 11 表示文档片段 DocumentFragment
  
## 节点增删改查
创建节点
* let div1 = document.createElement('div') 创建一个div节点
* let text1 = document.createTextNode('你好') 创建一个文本节点
* div1.appendChild(text1) 往标签里面插入文本，得是节点才行
* 创建了并没有在页面中，还需要把他放到body或者head里面才会生效
* appendChild(节点) 节点同时放到不同节点上时，只会在最后一个节点生效
* 可以用Node.cloneNode(true)克隆节点

删除节点
* div1.parentNode.removeChild(div1)
* div1.remove() 如果被移除了还是可以出现，需要dev1 = null 断开对象指向

修改节点
* div1.id = 'update'
* div1.className = 'red'(会覆盖已有的)
* div1.classList.add('red') 这样不会覆盖
* div1.style.color = 'red'
* div1.style.backgroundColor = 'black' 有-符号的使用大写字母代替
* div1.setAttribute('data-x','test') 添加自定义属性
* div1.getAttribute('data-x')
* div1.dataset.x = 'update'也可以
  

