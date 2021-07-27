### 复合版和new版对比
```javascript
function createSquare(width){
    let obj = Object.create(createSquare.squarePrototype)
    obj.width = width
    return obj
}
createSquare.squarePrototype = {
    getArea(){
        return this.width * this.width
    },
    getLength(){
        return this.width*4
    },
    constructor:createSquare
}
let square = createSquare(5)
```
后面被JS之父改造后变得更简单了，但是要用new 关键字来调用
```javascript
//Square是构造函数，给对象添加属性
function Square(width){
    this.width = width
}
//把共有的属性放到原型上
Square.prototype.getArea = function (){
    return this.width * this.width
}
Square.prototype.getLength = function (){
    return this.width *4
}
//直接就用new关键字调用函数
let square = new Square(5)
```

### new X()自动做了四件事
1. 自动创建空对象
2. 自动为空对象关联原型，原型地址指定位X.prototype
3. 自动将空对象作为this关键字运行构造函数
4. 自动return this
### 构造函数
* 构造函数负责给对象本身添加属性
* 构造函数.prototype对象负责保存对象的公用属性
* 构造函数一般用大写开头、名称形式，构造出来的对象首字母一般用小写
* 其它函数一般用动词开头 createSquare()

### 如何确定一个对象的元凶
* let obj = new Object()的原型是Object.prototype
* let arr = new Array()的原型是Array.prototype
* let square = new Square()的原型是Square.prototype
* let fn = new Function()的原型是Function.prototype
* 主要都是new操作做的四件事
* 是谁构造出来的对象，对象的原型就是谁的原型

### 类型和类
类型：  

类型是JS数据的分类，有7种，四基两空一对象
类：  

类是针对于对象的分类，有无数种，常见的有Array Function Date RegExp等

### 数组对象
* js里面数组是一个对象
* 定义一个数组
```javascript
let arr = [1,2,3]
let arr = new Array(1,2,3)//多个参数代表元素
let arr = new Array(3)//一个参数代表长度
```
* 自身的属性下标，'0'/'1'/'2',是字符串不是数字
### 数组对象的公用属性
```javascript
let arr = [1,2,3]
arr.push(5)//把一个元素添加到数组末尾
console.log(arr)// [1,2,3,5]
arr.pop()//把一个元素从数组末尾删除，并返回删除的元素
arr.shift(4)//把一个元素添加到数组开头
console.log(arr)//[4,1,2,3]
arr.unshift()//把数组开头的一个元素删除

arr.join()//把数组内的元素连接成一个字符粗
console.log(arr.join('---'))//1---2---3
```

### 函数对象
```javascript
function fn(x,y){
    return x+y
}
let fn2 = function fn(x,y){
    return x+y
}
let fn = (x,y)=>x+y

let fn = new Function('x','y','return x+y')
```
* 函数对象的自身属性：'name' 'length'
* 公用属性：call apply bind
