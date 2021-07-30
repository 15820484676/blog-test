# js函数执行时机

### 函数执行的时机不同，运行结果也不同。
```javascript
//函数没执行，不会打印
let a = 1
function fn() {
    console.log(a)
}

//函数执行，打印1
let a = 1
function fn(){
    console.log(a)
}
fn()

//函数在变量赋值为2后执行，打印出2
let a = 1
function fn(){
    console.log(a)
}
a = 2
fn()

//函数在变量赋值为1后面执行，打印1
let a = 1
function fn(){
    console.log(a)
}
fn()
a = 2
```

### 下面的代码为什么会打印出6个6？  

```javascript
let i = 0
for(i = 0; i<6; i++){
  setTimeout(()=>{
    console.log(i)
  },0)
}
```
* 因为setTimeout函数是一个异步函数，而异步函数的执行时机是在主线程的同步任务执行完了才开始执行，所以当for循环执行完了后，setTimeout函数才执行，而这时候i已经自增到了6，最后就打印6次6
* 同步任务：上一件事情没有完成，继续处理上一件事情，只有上一件事情完成了，才会做下一件事情(就像打lol一样，你还在对局中，突然你朋友叫你跟他双排，你必须得把这局游戏打完了才能和他一起排)
* 异步任务：规划要做一件事情，但是不是当前立马去执行这件事情，需要等一定的时间，这样的话，我们不会等着他执行，而是继续执行下面的操作。
  
### 那要让它打印出0 1 2 3 4 5呢？
```javascript
//for和let的组合可以实现需要的效果
for(let i=0;i<6;i++){
    setTimeout(()=>{
        console.log(a)
    },0)
}
```
### 还有其他方法打印出0 1 2 3 4 5 吗？(在网上找到三种方法)
```javascript
1、用闭包的方式
let i 
for(i = 0; i<6; i++){
  !function(j){
      setTimeout(()=>{
        console.log(j)
      },0)
  }(i)
}

2、利用 setTimeout 的第三个参数,将i传进去
let i
for(i = 0; i<6; i++){
    setTimeout((value)=>{
      console.log(value)
    },0,i)
}

3、利用 const 关键字
let i
for(i = 0; i<6; i++){
    const x = i
    setTimeout(()=>{
      console.log(x)
    })
}
```