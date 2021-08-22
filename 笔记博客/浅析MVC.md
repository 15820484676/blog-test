## 什么是MVC
* MVC是一种设计模式（设计模式：简单的说好用的东西就是设计模式），MVC能够使你的代码更简洁、优美，每个模块都可以写成三个对象，分别是M、V、C。
* M-Model 数据模型，负责操作所有的数据
```javascript
const m = {
  data: {
    n: parseInt(localStorage.getItem('n'))
  },
  create(){},
  delete(){},
  update(data){
    Object.assign(m.data,data) //data有什么属性就放到m.data上
    eventBus.trigger('m:updated')
    localStorage.setItem('n', m.data.n)
  },
  get(){}
}
```

* V-View  视图 负责所有的UI界面
```javascript
const v = {
  el: null,
  html: `
    <div>
      <div class="output">
        <span id="number">{{n}}</span>
      </div>
      <div class="actions">
        <button id="add1">+1</button>
        <button id="minus1">-1</button>
        <button id="mul2">*2</button>
        <button id="divide2">÷2</button>
      </div>
    </div>
  `
,
  init(container) {
    v.el = $(container)
  },
  render(n) {
    if(v.el.children.length !== 0) v.el.empty()
    $(v.html.replace('{{n}}', n))
      .appendTo(v.el)
    }
}
```
* C-Controller 控制器  是连接视图和模型桥梁，处理业务逻辑操作。它处理事件并作出响应。“事件”包括用户的行为和数据 Model 上的改变。
```javascript
const c = {
  init(container) {
    v.init(container)
    v.render(m.data.n) // view = render(data)
    c.autoBindEvents()
    eventBus.on('m:updated', () => {
      v.render(m.data.n)
    })
  },
  events: {
    'click #add1': 'add',
    'click #minus1': 'minus',
    'click #mul2': 'mul',
    'click #divide2': 'div',
  },
  add() {
    m.update({n: m.data.n + 1})
  },
  minus() {
    m.update({n: m.data.n - 1})
  },
  mul() {
    m.update({n: m.data.n * 2})
  },
  div() {
    m.update({n: m.data.n / 2})
  },
  autoBindEvents() {
    for (let key in c.events) {
      const value = c[c.events[key]]
      const spaceIndex = key.indexOf(' ')
      const part1 = key.slice(0, spaceIndex)
      const part2 = key.slice(spaceIndex + 1)
      v.el.on(part1, part2, value)
    }
  }
}
```
## EventBus
* EventBus 又称为事件总线,可以用来进行组件之间的监听和通信。比如说当 Model中的数据发生更新，触发了EventBus上的某个事件，而 Controller 恰好在监听这个事件，当这个事件触发时，Controller 就知道 Model 中的数据发生了更新了，从而做出一些反应.

* EventBus.on（）监听事件
```javascript
eventBus.on('m:updated',()=>{
     v.render(m.data.n)
 })
 ```
* EventBus.trigger（）触发事件
```javascript
eventBus.trigger('m:updated')
```
* EventBus.off（）取消事件
```javascript
eventBus.off('m:updated',()=>{
     v.render(m.data.n)
 })
```
## 表驱动编程

>表驱动方法是一种使你可以在表中查找信息，而不必用逻辑语句（if 或 case）来把他们找出来的方法。事实上，任何信息都可以通过表来挑选。在简单的情况下，逻辑语句往往更简单而且更直接。但随着逻辑链的复杂，表就变得越来越富于吸引力了.
表驱动编程的意义在于逻辑与数据的分离。（类似于事件委托）  
例如：  
```javascript
function translate(term) {
    if (term === '1') {
        return '一'
    } else if (term === '2') {
        return '二'
    } else if (term === '3') {
        return '三'
    } else {
        return '？？？'  
    }
}

// 如果想添加一个新的名词翻译，需要再添加一个if-else逻辑，例如：
function translate(term) {
    if (term === '1') {
        return '一'
    } else if (term === '2') {
        return '二'
    } else if (term === '3') {
        return '三'
    } else if (term === '4') {   
        // 此处添加了一个新的名词翻译
        return '四'
    } else {
        return '？？？'  
    }
}
```
使用表驱动：
```javascript
function translate(term) {
    let terms = {
        '1': '一',
        '2': '二',
        '3': '三'
    }
    return terms[term];
}

// 如果想添加一个新的名词翻译，只需要在terms中添加一个新的表项，不需要修改整个逻辑
function translate(term) {
    let terms = {
        '1': '一',
        '2': '二',
        '3': '三'
        '4': '四'   // 添加一个新的名词翻译
    }
    return terms[term];
}
```

## 模块化
>将一个复杂的程序拆分成多个模块，每个模块负责自己的的功能，然后不同的模块可以组合起来实现一个完整的系统，这则就是模块化。简单来说：就是把一坨代码写在一个文件里，其他文件需要使用的话引入这个文件就可以了。（模块化可以降低代码耦合度，减少重复代码，提高代码重用性，并且在项目结构上更加清晰，便于维护。）