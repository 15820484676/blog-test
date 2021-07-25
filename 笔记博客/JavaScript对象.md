## JavaScript对象
> 对象定义：无序的数据集合，键值对的集合  
### 对象的两种语法：
```javascript
1. let obj  = {'name':'peter','age':18}
2. let obj = new Object({'name':'peter','age':18})
```
* new的方式是正规的写法
* Object.keys(obj)可以得到对象的键名数组
* {}方式方便，现在大都是这样写的
* 键名是字符串，可以是任意字符(不要和标识符搞混了)
```javascript
let obj = {
    '':1,
    '__':2,
    '2fefe':true
}
```
* 键的引号可以省略，省略后只能写标识符（*键还是字符串*）
* 属性名可以是一个变量，加了[]会当做变量求值，ES6写法：
```javascript
let a = 'vae'
let obj = {
    [a] :1
}
```
* symbol也能做属性名 
```javascript
let a = Symbol()
let obj = {[a]:1}
```

### 对象的隐藏属性
* JS中的每一个对象都有一个隐藏属性
* 这个属性存储着共有属性组成的对象的地址(也叫原型的地址)，这个共有属性组成的对象就叫做*原型*
* *所有对象原型的原型值为null*

### 删除对象的属性
* 删除属性名和值、删除属性值
```javascript
删除属性值
let obj = {name:'peter',age:18}
obj.name = undefined

删除属性名和值
let obj2 = {name:'peter',age:18}
delete obj.name
```
* 'xxx' in obj ===false 不含属性名，不能查看是否为自身还是原型的属性
* 'xxx' in obj && obj.xxx === undefined 含有属性名，到那时值为undefined
* 不能用 obj.xxx === undefined 断定是否为Obj的属性
### 查看对象的属性

* obj['key']   obj.key obj[key] 中括号语法，点语法，中括号里面是变量先求值 
* Object.keys(obj) 查看对象的所有属性名
* console.dir(obj) 查看自身和共有属性
* obj.__proto__ 查看共有的属性
* <font color=#00ffff size=3>obj.hasOwnProperty('toString') 是判断一个属性是否为自身的属性</font>
* <font color=#00ffff size=3>'name' in obj 是判断一个对象是否有某个属性（不能区分是自身的还是原型的）</font>
* Object.values(obj) 查看对象的所有属性值
* Object.entries(obj) 把对象的属性组成一个二维数组

### 修改对象属性

* obj.name = 'peter' （有就修改，没有就新增）
* obj['name'] = 'peter'
* Object.assign(obj,{p1:1,p2:2})给Obj对象批量赋值
* 无法通过自己新增或修改原型的属性
```javascript
 obj.__proto__.toString = 'xxx' 可以通过__proto__修改原型属性，*不推荐用__proto__*
```
* 要修改原型属性就用 ：window.Object.prototype
* let obj = Object.create(obj2) 以某个对象为原型创建对象