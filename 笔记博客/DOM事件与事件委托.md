## 捕获与冒泡
* 2002年，w3c发布标准，文档名为DOM level 2 Events Specification，规定了浏览器应该同时支持两种调用顺序
* 首先按照 爷爷->爸爸->儿子顺序看有没有函数监听
* 然后按儿子->爸爸->爷爷顺序看有没有函数监听
* 有监听函数就调用，并且提供时间信息，没有就跳过
* 从外向内找监听函数，叫事件捕获
* 从内向外找监听函数，叫事件冒泡
* 如果都有监听函数，那不是要调用两次？不是！我们可以自己选择把函数放在捕获还是冒泡阶段

## W3C事件模型
事件绑定API
```javascript
//IE5 冒泡
dom.attachEvent('onclick',fn)
//网景 捕获
dom.addEventListener('click',fn)
//W3C就综合了下，加了个参数选择是否冒泡还是捕获。默认是冒泡bool=falsy 为true是捕获触发
dom.addEventListener('click',fn,bool)
```
* 先捕获再冒泡
* e对象被传给所有的监听函数，事件结束后，e对象就不存在了
e.target 和e.currentTarget的区别
* 比如 div>span{文字}，用户点击了文字，那么e.target就是span e.currentTarget就是div

### 特例
只有一个div被监听的时候，fn分别在捕获和冒泡阶段都监听了click事件，那么谁先监听谁先执行

### 取消冒泡
* 捕获不可以取消，冒泡可以取消
* e.stopPropagation() 中断冒泡，浏览器不再向上走
* 一般用来封装某些独立的组件

### 不可取消冒泡
* 滚动事件就不可以取消冒泡
```javascript
//禁用滚动操作
//浏览器上阻止鼠标滚动
x.addEventListener('wheel',(e)=>{
    e.preventDefault()
})
//隐藏滚动条
::webkit-scrollbar{
    width:0 !important
}
//手机上阻止滚动
x.addEventListener('touchstart',(e)=>{
    e.preventDefault()
})
```
### 自定义事件
* 浏览器自带了100多种事件 MDN查看
```javascript
button1.addEventListener('click',()=>{
    const event = new CustomEvent('yy',{
        detail:{name:'yy',age:18},
        bubbles:true,//可以自动冒泡
        cancelable:false//不可以取消冒泡
    })
    button1.dispatchEvent(event)
})

button1.addEventListener('yy',(e)=>{
    console.log('出发了自定义yy事件')
    console.log(e.detail)
})
```

### 事件委托
* 如果要给100个按钮添加点击事件怎么办？
* 直接监听这100个按钮的祖先，冒泡的时候判断e.target是不是100个按钮中的一个 
* 如果要监听当前不存在的元素的点击事件怎么办？
* 监听祖先，等点击的时候看是不是我想要监听的元素
* 优点是 可以省监听数量，不用写多个监听函数，省内存
* 可以监听动态生成的元素
```javascript
//自己封装一个监听函数
on('click','#div','button',()=>{
    console.log('button被点击了')
})

function on(eventType,element,selector,fn){
    if(!(element instanceof Element)){
        element = document.querySelector(element)
    }
    element.addEventListener(eventType,(e)=>{
        const t = e.target
        if(t.matches(selector)){
            fn(e)
        }
    })
}
```