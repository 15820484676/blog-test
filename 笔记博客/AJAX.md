# AJAX
## 简介
* AJAX是浏览器上的功能，不是js上的，是js控制浏览器发送请求
* window.XMLHttpRequest函数

## 创建AJAX 四个步骤
1. 创建HttpRequest对象
2. 调用对象的open方法
3. 监听对象的onload& onerror事件（但是都用onreadystatechange事件）
  * 什么时候会触发onerror事件呢？
4. 调用对象的send方法 
### 一个请求的一生 readyState
* const req = new HttpRequest  state=0
* req.open('GET',url)   state = 1
* req.send()  state = 2
* 得到了响应，第一个信息出现在浏览器的时候  state=3
* 下载完全部的信息的时候 state=4
* AJAX本来就是支持xml的

## JSON javascript标记语言
* json是一门独立的语言，标记语言 不是编程语言
* 支持的六种数据类型
  1. string  只支持双引号
  2. number 只支持科学计数法
  3. bool true和false
  4. null 没有undefined
  5. object 
  6. array
* JSON.parse(request.response) 可以把JSON字符串转换成JS对应的数据，如果不符合JSON语法，会直接抛出一个Error对象，一般用try catch捕获错误
* JSON.stringify() 是JSON.parse的逆运算，可以把JS数据转换成JSON字符串，但是JS的数据类型比JSON多，所以不一定成功，如果失败也会抛出一个Error对象
### 