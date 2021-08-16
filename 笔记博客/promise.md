## 异步和同步
* 如果能直接拿到结果就是同步 
* 举例：排队取号这个过程，拿到号才会走，中间可能花费一定的时间
* 如果不能直接拿到结果的就是异步
* 举例：比如出去吃饭，去拿个号需要要等到叫号才能吃饭，这时候可以出去逛街，等叫号到了再吃饭
* 每隔一段时间问下到号没有，这是轮询
* 也可以扫码微信通知你到号没有，这是回调
## ajax的异步
```javascript
const req = new XMLHttpRequest()
req.open('GET','/index.html')
req.onreadystatechange = ()=>{
    if(req.readyState ===4 && req.status ===200){
        let result = JSON.parse(res.response)
    }
}
req.send()
//这里会打印出''
console.log(result)
setTimeout(()=>{
    //2s后打印出响应
    console.log(result)
},2000)
```
* 如果直接打印结果是空的，因为ajax是异步的，等内容下载完毕后，浏览器回头调用（callback）onreadystatechange()方法
* 写给别人用的函数，就是回调
```javascript
//这就是回调函数,把f1函数传给f2去调用
function f1(){
    console.log('callback')
}

function f2(fn){
    console.log('这是调用')
    fn()
}
f2(f1)
```
* 异步任务经常会使用回调函数，但是不一定必须要使用回调函数
* 如何知道一个函数是异步还是同步函数
  1. setTimeout
  2. AJAX
  3. addEventListener
  4. 如果函数的返回值处于这三个东西内部，那么这个函数就是异步函数
* ajax也可以设置成同步的

## 异步总结
异步任务不能直接拿到结果，需要我们传一个回调函数给异步任务，异步任务完成时调用回调函数，回调的时候把结果作为参数传给回到函数

## 异步任务失败和成功
* 回调函数接受两个参数 callback(error,success)
* 写两个回调，或者放到一个对象里面
* 但是也有缺点
   1. 不规范
   2. 容易出现回调地狱（回调函数里面嵌套多层回调函数）
   3. 很难进行错误处理

## promise（面试考点）
 
```javascript
//ajax回到
ajax('get','/index.html',{success(res){},fail(req,status){}})
//promise 第一个参数就是success,第二个参数是fail
//ajax()返回了一个promise对象，对象上有then方法
ajax('get','/index.html').then(res=>{},req=>{})

//改造ajax返回promise,需要返回promise对象，直接把原来的函数体放在一个回调函数里面
ajax = (method,url,options)=>{
    return new Promise((resolve,reject)=>{
        const req = new XMLHttpRequest()
        req.open(method,url)
        req.onreadystatechange = ()=>{
        if(req.readyState ===4 ){
            if(req.status< 400){
                resolve.call(null,req.response)
            }else if(request.status >=400){
                reject.call(null,req)
            }
        }
    }
    req.send()
    })
}
```
### promise的用途
1. 可以处理异步任务
2. 可以将异步操作队列化，按照期望的顺序执行，返回符合预期的结果，解决回调地狱的问题

### 如何创建一个promise
return new Promise((resolve,reject)=>{}) 
### 如何使用Promise.prototype.then
Promise对象只有三种状态:  
1. 异步操作“未完成”（pending）
2. 异步操作“已完成”（resolved，又称fulfilled）
3. 异步操作“失败”（rejected）  

then()方法返回一个Promise。它最多需要有两个参数：Promise 的成功和失败情况的回调函数。当Promise变成fulfilled状态时回调用onFulfilled函数，当状态变成rejected时会电泳onRejected函数，状态由pending状态变成fulfilled或者rejected，改变后就不变成其它状态了
语法：
```javascript
p.then(onFulfilled[, onRejected]);

p.then(value => {
  // fulfillment
}, reason => {
  // rejection
});
```
### 如何使用Promise.all
Promise.all() 方法接收一个promise的iterable类型（注：Array，Map，Set都属于ES6的iterable类型）的输入，并且只返回一个Promise实例， 输入的所有promise的resolve回调的结果是一个数组。这个Promise的resolve回调执行是在所有输入的promise的resolve回调都结束，或者输入的iterable里没有promise了的时候。它的reject回调执行时机是：只要任何一个输入的promise的reject回调执行或者输入不合法的promise就会立即抛出错误，并且reject的是第一个抛出的错误信息。如果参数中包含非 promise 值，这些值将被忽略，但仍然会被放在返回数组中（如果 promise 完成的话）：
```javascript
var p1 = Promise.resolve(3);
var p2 = 1337;
var p3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'foo');
});

Promise.all([p1, p2, p3]).then(values => {
  console.log(values); // [3, 1337, "foo"]
});
```
### 如何使用 Promise.race
promise.race也是传入一个数组，但是与promise.all不同的是，race只返回跑的快的值，也就是说result返回比较快执行的那个。但是跑的慢的那个还是会执行下去。
```javascript

var p1 = new Promise(function (resolve) {
   setTimeout(function () {
       console.log(1);
       resolve("第一个promise");
   }, 3000);
});
 
var p2 = new Promise(function (resolve) {
   setTimeout(function () {
       console.log(2);
       resolve("第二个promise");
   }, 1000);
});
 
Promise.race([p1, p2]).then(function (result) {
   console.log(result); 
//打印出：
//2
//第二个promise
//1
```

## axios
* JSON自动处理
* 请求拦截器
* 响应拦截器
* 可以生产不同实例（复杂场景）
## 同源
域名、协议、端口相同，也就是在同一个域里
## 跨域
什么是跨域：  
a页面想获取b页面资源，如果a、b页面的协议、域名、端口、子域名不同，所进行的访问行动都是跨域的，而浏览器为了安全问题一般都限制了跨域访问，也就是不允许跨域请求资源。注意：跨域限制访问，其实是浏览器的限制。

1. CORS
2. JSONP IE不支持cors，用JSONP
3. 还有postMessage、websockt、nginx反向代理等等..

### CORS
1. 浏览器发送跨域请求
2. 服务器端收到一个跨域请求后，在响应头中添加Access-Control-Allow-Origin 发送响应
3. 浏览器收到响应后，查看响应头是否设置了Access-Control-Allow-Origin:请求源域名或者*;
4. 如果当前域已经得到授权，则将结果返回给JavaScript。否则浏览器忽略此次响应(会在控制台打印出跨域提示)。

### JSONP是什么？面试回答
1. 当前浏览器不支持cors，我们必须使用另外一种方式来跨域，于是我们要请求一个js文件，js文件里面会执行一个回调函数，回调函数的里面有需要的数据 这就是JSONP 
  * 通过script标签引入一个js文件，这个js文件载入成功后会执行我们在url参数中指定的函数，并且会把我们需要的json数据作为参数传入。所以jsonp是需要服务器端的页面进行相应的配合的。（即用javascript动态加载一个script文件，同时定义一个callback函数给script执行而已。）
2. 回调的名字是什么呢？
  * 回调函数是一个随机数，以callback为参数的形式传给后端，后端会把函数执行返回给我们
  * 优点是什么：支持IE，跨域
  * 确定是什么：由于它是script标签，拿不到像ajax那样的请求状态，也不知道相应的头之类的，只能发送get不支持post(为什么？因为script不支持post)

## 前端的理解
前端主要是负责B端和C端的用户界面制作和跟后端进行数据交互，让用户能自由操作应用或网站。
前端相当于是使用者和后台的一个桥梁，用户使用前端可以方便的和后台进行数据交互。所以前端
需要了解用户的交互体验，又要和后端打交道，还得会点后端知识。