## 定义函数
四种定义函数方式：
### 具名函数
```javascript
function 函数名(形参1，形参2){
    语句
    return 返回值
}
```
### 匿名函数
let a = function (x,y){return x+y}
* 等号右边叫函数表达式
* 如果函数声明在等号右边，那么作用域就能在等号右边
### 箭头函数
*箭头函数没有this和arguments*
```javascript
//()=>{},如果只有一个参数可以省略括号，只有一条语句可以省略return 
let f1 = x =>x*x
//如果函数体有多条语句要加上大括号和return  
let f1 = (x,y)=>{
    console.log(x)
    return x+y
}
//如果返回的是一个对象，那么可以写成这样
let f1 = x=>({name:yy})
```
### 构造函数(基本没人用)
let f =new Function('x','y','return x+y')
*所有的函数都是由Function构造的*

## 函数的要素
### 函数调用时机
* 函数在调用的时候才执行 
* for和let一起用的时候会加东西

### 作用域
* 每个函数都会创建一个作用域{}
* 就近原则，谁离得近就用谁
* 全局变量
  * 挂在window下的属性
  * 在顶级作用域下定义的变量
* 其它都是局部变量

### 闭包
```javascript
function f1(){
    let a = 1
    function f2(){
        console.log(a)
    }

}
```
* 如果一个函数用到了外部的变量，这个函数加这个变量就叫做闭包
* let a 和f2 组成了闭包

### 形式参数
```javascript
function add(x,y){
    return x+y
}
```
* x,y就是形参，并不是实际的参数
* 调用的时候才会把实际参数赋值给x,y
* 本质是变量的声明
* 就算定义了形参也可以不传

### 返回值
* 只有函数有返回值
* 每个函数都有返回值，没写return，返回值是undefined 

### 调用栈
* js引擎在调用一个函数前，需要把函数所在的环境Push到一个数组里，这个数组叫调用栈，等函数执行完了，就会把环境pop出来，然后return 到之前的环境，继续执行后续代码
* 压栈和弹栈的过程
* 爆栈：压入的栈太多了 

### 函数提升
```javascript
add(1,2)
function add(x,y){
    return x+y
}
```
* 函数永远会到第一行
* 如果用了let声明函数，必须先声明在调用
  
### arguments
```javascript
function fn(){
    console.log(arguments)
    console.log(this)
}
```
* 调用fn的时候就传了arguments
* argument是个伪数组，可以用Array.from()转成数组

如何传this?
* 使用fn.call()
* fn.call(1,2,3,4) 1就是this,2,3,4是arguments
* 如果传的不是对象，js会自动转成对象
* 可以在声明函数的时候加 use strict 来让它不要加东西，那么传的是什么this就是什么
* js在每个函数里加了this
```javascript
let person = {
    name:'yy',
    sayHi(){
        console.log(this.name)
    }
}
person.sayHi()相当于 person.sayHi(person)
```
函数两种调用方法：
1. person.sayHi()
2. person.sayHi.call(person)//手动传this的值
person.sayHi.call(undefined,1,2)//指定this为undefined  

绑定this：
* 使用.bind可以让this不被改变
```javascript
function f1(p1,p2){
    console.log(this,p1,p2)
}
let f2 = f1.bind({name:'frank'})//f2就是f1绑定了this之后的新函数
f2() //等价于f1.call({name:'frank'})

//其它参数
let f3 = f1.bind({name:'frank'},'hi')
f3()//等价于f1.call({name:'frank'},'hi')
```
### 箭头函数没有this和arguments

### 立即执行函数
* 声明一个匿名函数直接调用
```javascript
!function(){
    let a = 1
    console.log(a)
}
```